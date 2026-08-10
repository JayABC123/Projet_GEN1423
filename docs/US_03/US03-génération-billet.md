### TASK-3.4 — Concevoir le processus de génération du billet
## Décision architecturale : génération synchrone vs asynchrone
 
| Critère | Génération synchrone | Génération asynchrone (retenue) |
|---|---|---|
| Temps de réponse au client | Bloquant, dépend du temps de génération du QR Code | Réponse immédiate après confirmation du paiement |
| Comportement en pic de charge | Risque de ralentissement de l'API de paiement | Le paiement reste rapide, la génération est traitée en différé |
| Résilience aux pannes | Un échec de génération peut faire échouer tout le paiement | Le paiement est indépendant ; la génération peut être retentée sans impact sur la transaction |
| Complexité | Plus simple à implémenter | Nécessite une file de messages (ex. RabbitMQ, AWS SQS) et un mécanisme de retry |
 
Décision retenue : génération asynchrone, via une file de messages,
afin de ne pas bloquer la confirmation du paiement en cas de pic de
charge (jusqu'à 50 000 requêtes/s selon le profil de charge du sujet) et
de permettre une reprise automatique en cas d'échec temporaire du
service de génération.
 
Compromis accepté : le client ne reçoit pas son billet de façon
instantanée (délai de quelques secondes le temps du traitement
asynchrone), ce qui est jugé acceptable dans le contexte d'un achat de
billet, contrairement à une opération nécessitant une confirmation
immédiate.
 
## Limites et risques associés
 
- Délai de disponibilité du billet : en cas de forte charge sur la
  file de messages, le délai entre le paiement et la réception du billet
  peut s'allonger. Une limite de temps maximale (ex. 30 secondes) devrait
  être définie et surveillée.
- Duplication de génération : un mécanisme d'idempotence est
  nécessaire pour éviter qu'un même évènement "PaiementConfirmé" ne
  génère deux billets en cas de retraitement du message.
- Dépendance à la file de messages : une panne prolongée du service
  de messagerie retarderait la génération de tous les billets en attente ;
  une stratégie de reprise après incident doit être prévue (voir plan de
  reprise du Volet 3).