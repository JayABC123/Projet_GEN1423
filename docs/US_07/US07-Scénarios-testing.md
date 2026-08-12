# TASK-7.4 — Scénario de test

Les scénarios de test permettent de valider les principaux comportements
du tableau de bord administrateur de TicketPulse. Ils couvrent notamment
l'affichage des statistiques de ventes, leur rafraîchissement et la
cohérence des données présentées.

| ID | Type | Scénario | Entrée / Action | Résultat attendu |
|---|---|---|---|---|
| T01-US07 | Fonctionnel | Consultation du tableau de bord | L'administrateur ouvre le tableau de bord d'un événement | Le nombre de billets vendus, disponibles et le revenu total sont affichés |
| T02-US07 | Fonctionnel | Mise à jour après une vente | Une nouvelle vente est finalisée pendant que le tableau de bord est consulté | Les statistiques sont mises à jour au prochain rafraîchissement |
| T03-US07 | Fonctionnel | Événement sans vente | Consulter le tableau de bord d'un événement n'ayant aucune vente | Le nombre de billets vendus et le revenu total affichés sont égaux à 0 |
| T04-US07 | Sécurité | Accès non autorisé | Un utilisateur non administrateur tente d'accéder au tableau de bord | L'accès au tableau de bord est refusé |
| T05-US07 | Fonctionnel | Calcul du revenu | Consulter un événement comportant plusieurs ventes finalisées | Le revenu total correspond à la somme des ventes finalisées |
| T06-US07 | Non-fonctionnel | Rafraîchissement des données | Laisser le tableau de bord ouvert pendant une période de ventes | Les données sont mises à jour au moins une fois par minute |
| T07-US07 | Charge | Consultation simultanée | Simuler 100 administrateurs consultant simultanément leur tableau de bord | Le système continue de répondre correctement sans perturber les opérations critiques |

## Notes

- T01-US07 valide directement le critère d'acceptation concernant l'affichage
  du nombre de billets vendus, disponibles et du revenu total.
- T06-US07 valide l'exigence de rafraîchissement des statistiques au moins
  une fois par minute.
- T07-US07 utilise l'hypothèse de dimensionnement définie dans TASK-7.3.
- Les tests du tableau de bord ne doivent pas compromettre les performances
  des fonctionnalités critiques de réservation et de paiement.
