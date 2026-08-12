### TASK-4.5 — Définir les scénarios d'erreur
 
Les scénarios de test sont basés sur les principaux cas d’échec du processus de réservation temporaire de siège, notamment la sélection concurrente du même siège, les soumissions en double ou les doubles clics, l’expiration du verrou (TTL) pendant le paiement, la perte de connexion client, ainsi que l’indisponibilité ou la défaillance du service de verrouillage (Redis) ou de la base de données. Ils permettent de valider que le système gère correctement ces erreurs, conserve ou libère l’état de la réservation de façon sûre (TTL de 5 minutes), évite la double réservation et prévient toute incohérence ou perte de disponibilité conduisant à une survente.

## Scénarios d'erreur
 
| ID | Scénario | Entrée / Action | Résultat attendu |
|---|---|---|---|
| T-US02-E01 | Sélection d'un siège déjà verrouillé | Client B sélectionne un siège verrouillé par Client A | Message « siège indisponible », sélection refusée |
| T-US02-E02 | Expiration du verrou pendant le paiement | Client dépasse 5 minutes sans finaliser le paiement | Verrou libéré automatiquement, siège redevient disponible, paiement rejeté si tenté après expiration |
| T-US02-E03 | Perte de connexion du client | Client ferme l'onglet avant paiement | Verrou expire normalement au bout du TTL (pas de blocage permanent du siège) |
| T-US02-E04 | Panne du service de verrouillage (Redis) | Service Redis indisponible | Le système refuse temporairement les nouvelles réservations avec message d'erreur explicite, plutôt que de risquer une survente |
| T-US02-E05 | Tentative de double clic rapide | Client clique plusieurs fois sur « Réserver » | Une seule requête de verrouillage traitée, pas de verrous multiples créés pour le même client |
 
## Notes
- T-US02-E01 et T-US02-E05 valident directement le critère d'acceptation
  « Protection contre la double réservation » défini dans SCRUM-26.
- T-US02-E02 et T-US02-E03 valident le comportement d'expiration du
  verrou (TTL de 5 minutes) documenté dans SCRUM-28.
- T-US02-E04 découle de l'analyse de résilience réalisée dans SCRUM-29 et
  doit être repris dans le plan de reprise après incident du Volet 3.
