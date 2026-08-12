### TASK-4.4 — Analyse de la concurrence

#### Scénario critique
Deux clients tentent de sélectionner le même siège au même instant lors
d'une vente flash à forte affluence.

#### Comportement attendu du système
1. Les deux requêtes de verrouillage arrivent quasi simultanément au
   service de réservation.
2. Grâce à l'atomicité de l'opération Redis (SET NX), un seul des deux
   clients obtient effectivement le verrou.
3. Le second client reçoit une réponse immédiate indiquant que le siège
   n'est plus disponible, et le plan de salle est mis à jour pour tous
   les utilisateurs connectés (ex. via WebSocket ou polling).

#### Risque associé
Une latence réseau ou une désynchronisation entre plusieurs instances du
service de réservation (si le système est distribué sur plusieurs
serveurs) pourrait théoriquement créer une fenêtre de "race condition".

#### Mitigation
- Utiliser une seule source de vérité centralisée pour les verrous
  (cluster Redis dédié), garantissant l'atomicité même avec plusieurs
  instances du service de réservation.
- Prévoir une réconciliation automatique en cas d'incohérence détectée
  (ex. tâche de vérification périodique).