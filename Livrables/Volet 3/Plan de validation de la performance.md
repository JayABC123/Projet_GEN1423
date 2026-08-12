# Plan de validation de la performance

Ce document identifie les principaux indicateurs de performance de
TicketPulse et propose une démarche de vérification permettant de
confirmer que les objectifs de performance définis dans les User
Stories sont atteints.

## 1. Indicateurs de performance identifiés

| ID | Indicateur | Source (US) | Seuil cible |
|---|---|---|---|
| P-01 | Temps de réponse de la recherche d'événements | US-01 | < 2 secondes |
| P-02 | Temps d'affichage des détails d'un événement | US-02 | < 2 secondes |
| P-03 | Délai de finalisation du paiement | US-03 | < 5 minutes |
| P-04 | Durée du verrouillage temporaire d'un siège | US-04 | 5 minutes (TTL) |
| P-05 | Fraîcheur de l'affichage du plan de salle en temps réel | US-05 | Mise à jour immédiate (< quelques secondes) |
| P-06 | Délai d'émission de l'alerte d'expiration de réservation | US-06 | Alerte déclenchée à 1 minute avant expiration |
| P-07 | Fréquence de rafraîchissement du tableau de bord des ventes | US-07 | Au moins une fois par minute |
| P-08 | Débit du système en pic de vente flash | Profil de charge global | 50 000 requêtes/s pendant les 10 premières minutes |
| P-09 | Capacité de connexions simultanées | Profil de charge global | 250 000 utilisateurs connectés simultanément |

## 2. Démarche de vérification par indicateur

### P-01 / P-02 — Temps de réponse (recherche et consultation)
- Méthode : tests de performance automatisés (ex. k6, JMeter) simulant
  des requêtes de recherche et de consultation en charge croissante.
- Critère de succès : 95e percentile du temps de réponse sous 2
  secondes, même à charge nominale (1 000 utilisateurs actifs/jour).

### P-03 — Délai de paiement
- Méthode : test de bout en bout mesurant le temps entre la
  soumission du paiement et la confirmation reçue par le client.
- Critère de succès : 100 % des transactions confirmées ou rejetées
  en moins de 5 minutes.

### P-04 — Durée du verrouillage
- Méthode : test d'intégration vérifiant que le TTL Redis expire
  précisément après 300 secondes et libère automatiquement le siège.
- Critère de succès : aucun verrou ne persiste au-delà de 5 minutes
  ± quelques secondes de marge technique.

### P-05 — Fraîcheur du plan de salle
- Méthode : test manuel et automatisé simulant deux clients
  simultanés ; vérifier que la mise à jour du statut d'un siège
  (verrouillé par un client) est visible par l'autre client dans un
  délai raisonnable (quelques secondes).
- Critère de succès : propagation de l'état du siège perçue comme
  quasi instantanée par l'utilisateur.

### P-06 — Alerte d'expiration
- Méthode : test fonctionnel déclenchant une réservation puis
  vérifiant l'apparition de l'alerte visuelle exactement à la minute
  précédant l'expiration.
- Critère de succès : alerte affichée dans la fenêtre de 60 ± 5
  secondes avant expiration.

### P-07 — Rafraîchissement du tableau de bord
- Méthode : test de bout en bout simulant une nouvelle vente et
  mesurant le délai avant mise à jour des statistiques affichées à
  l'administrateur.
- Critère de succès : les chiffres affichés reflètent les ventes
  finalisées au maximum une minute après la transaction.

### P-08 / P-09 — Débit et connexions simultanées en pic
- Méthode : test de charge (load testing) et test de stress simulant
  une montée progressive jusqu'à 250 000 connexions simultanées et un
  débit de 50 000 requêtes/s, réparti selon les proportions estimées
  dans les calculs de dimensionnement (TASK-1.3, TASK-1.5, TASK-1.6).
- Critère de succès : le système reste disponible (pas de panne
  généralisée) et respecte les seuils P-01 à P-04 même en conditions de
  pic ; dégradation progressive acceptable plutôt que défaillance totale.


## 3. Outils de validation proposés
- Tests de charge/stress : k6, Apache JMeter ou Gatling, pour simuler
  les pics définis dans le profil de charge du sujet.
- Monitoring en continu : outils d'observabilité (ex. Prometheus +
  Grafana) pour mesurer les indicateurs en temps réel pendant les tests
  et en production.
- Tests synthétiques : scripts automatisés exécutés périodiquement
  pour valider en continu les seuils P-01, P-02 et P-05.

## 4. Limites de la démarche
- Les tests de charge simulés ne reproduisent pas parfaitement les
  conditions réseau réelles des utilisateurs finaux (latence variable,
  connexions mobiles).
- La validation du seuil de 250 000 connexions simultanées nécessite une
  infrastructure de test à grande échelle, potentiellement coûteuse à
  reproduire fidèlement en environnement de test.
- Les seuils proposés (ex. 1 minute pour le rafraîchissement du tableau
  de bord) sont des hypothèses raisonnables en l'absence d'exigence
  précise dans l'énoncé et devraient être validés avec les parties
  prenantes dans un contexte réel.