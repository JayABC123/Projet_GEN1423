### TASK-3.6 — Scénarios d’échec

Les scénarios de test sont basés sur les principaux cas d’échec du processus de paiement de
TicketPulse, notamment le refus ou l'indisponibilité de la passerelle de paiement, les doubles
soumissions, ainsi que les erreurs pouvant survenir après la confirmation du paiement. Ils
permettent de valider que le système gère correctement les erreurs, conserve l’état de la
réservation lorsque nécessaire et évite toute perte ou duplication de transaction.

| ID | Type | Scénario | Entrée / Action | Résultat attendu |
|---|---|---|---|---|
| T01-US03 | Fonctionnel | Paiement refusé par la passerelle | Saisir une carte refusée et lancer le paiement | Un message d’erreur est affiché et le siège reste réservé jusqu’à expiration |
| T02-US03 | Fonctionnel | Timeout de la passerelle de paiement | Simuler une passerelle qui ne répond pas dans le délai prévu | La transaction est annulée, le siège est libéré et un message d’erreur clair est affiché |
| T03-US03 | Fonctionnel | Double soumission du paiement | Cliquer plusieurs fois sur « Payer » rapidement | Une seule transaction est traitée grâce à l’utilisation d’une clé d’idempotence |
| T04-US03 | Fonctionnel | Échec de génération du billet après paiement réussi | Confirmer le paiement alors que le service de génération du billet est indisponible | Le paiement est conservé et la génération du billet est réessayée automatiquement, sans perte pour le client |
| T05-US03 | Fonctionnel | Échec d’envoi du courriel de confirmation | Rendre le service de messagerie indisponible après la génération du billet | Le billet reste accessible dans le profil du client malgré l’échec de l’envoi du courriel |

#### Notes

- T01-US03 et T02-US03 valident la gestion des erreurs de paiement et la libération
  appropriée des sièges.
- T03-US03 valide l’idempotence du processus de paiement afin d’éviter les transactions
  ou débits en double.
- T04-US03 et T05-US03 vérifient que les erreurs survenant après le paiement ne causent
  pas de perte pour le client.
- Les scénarios T04-US03 et T05-US03 permettent également de vérifier la résilience
  des services dépendants du processus de paiement.