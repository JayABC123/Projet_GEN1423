# Tableau des compromis et solutions rejetées

Ce document recense les principales décisions architecturales prises
pour répondre aux User Stories de TicketPulse, les alternatives
envisagées, ainsi que les compromis acceptés et les solutions rejetées.

## Tableau des compromis

| # | Décision retenue | US concernée(s) | Alternative rejetée | Justification du rejet | Compromis accepté |
|---|---|---|---|---|---|
| 1 | Verrou distribué avec TTL (Redis) pour la réservation temporaire | US-04 | Verrou pessimiste en base de données relationnelle (`SELECT ... FOR UPDATE`) | Contention élevée sur la base de données principale lors des ventes flash, ralentissement généralisé | Dépendance additionnelle à un service de cache distribué à maintenir |
| 2 | Génération asynchrone du billet électronique (file de messages) | US-03 | Génération synchrone immédiate après paiement | Bloquerait la réponse au client en cas de pic de charge, risque de ralentir l'API de paiement | Délai de quelques secondes avant réception du billet par le client |
| 3 | Mise à jour du plan de salle via push/WebSocket (temps réel) | US-05 | Rafraîchissement par polling périodique (ex. toutes les 5 secondes) | Le polling introduirait un délai perceptible et une charge réseau inutile en pic de trafic | Complexité accrue de l'infrastructure (gestion des connexions persistantes) |
| 4 | Alerte d'expiration déclenchée côté client à partir d'un minuteur synchronisé avec le TTL serveur | US-06 | Notification poussée par le serveur (push notification) à chaque client | Solution plus simple à implémenter avec un coût d'infrastructure moindre pour un cas d'usage non critique | Risque de léger désynchronisme si l'horloge client dérive (mitigé par synchronisation périodique) |
| 5 | Rafraîchissement du tableau de bord des ventes au moins une fois par minute (quasi temps réel) | US-07 | Rafraîchissement en temps réel strict (push à chaque transaction) | Fonctionnalité réservée aux administrateurs, moins critique que les fonctionnalités client ; un vrai temps réel ajouterait une charge disproportionnée pour peu de valeur ajoutée | Les statistiques affichées peuvent avoir jusqu'à une minute de retard |
| 6 | Cache des plans de salle (peu de changements) | US-05 | Requête base de données à chaque consultation | Les plans de salle changent rarement ; interroger la base à chaque fois gaspillerait des ressources inutilement | Nécessite une invalidation de cache lors des rares mises à jour du plan |
| 7 | Délégation du traitement des paiements à un fournisseur externe (ex. Stripe) | US-03 | Traitement des paiements en interne | Complexité et risques de conformité (PCI-DSS) élevés à gérer en interne, sans bénéfice significatif | Dépendance à un service tiers et à ses limites de débit contractuelles |
| 8 | Priorisation MoSCoW du backlog (US-06 en Should Have, US-07 en Could Have) | Toutes les US | Traiter toutes les US avec la même priorité | Le temps limité du projet (7 jours) exige de concentrer l'effort sur les fonctionnalités critiques du parcours d'achat (US-01 à US-05) | US-06 et US-07 pourraient être partiellement approfondies si le temps le permet, sans compromettre le cœur du système |

## Notes
- Les compromis 1, 2 et 3 concernent des scénarios critiques identifiés
  explicitement dans l'énoncé (survente, disponibilité, cohérence des
  données), et ont donc été traités en priorité avec des solutions plus
  robustes malgré une complexité accrue.
- Les compromis 4 et 5 concernent des fonctionnalités secondaires
  (US-06, US-07), où une solution plus simple a été privilégiée afin de
  concentrer les efforts d'architecture sur le parcours d'achat
  principal (US-01 à US-05).
- Ce tableau complète le tableau des décisions architecturales du Volet
  2 en mettant l'accent spécifiquement sur les alternatives écartées et
  leur justification.