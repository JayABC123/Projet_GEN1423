### TASK-6.1 — Scénarios de test

Les scénarios de test valident la notification d'expiration de réservation
(US-06), en particulier le déclenchement de l'alerte et la cohérence avec
le mécanisme de verrouillage temporaire du siège.

| ID | Type | Scénario | Entrée / Action | Résultat attendu |
|---|---|---|---|---|
| T01-US06 | Fonctionnel | Alerte avant expiration | Un siège m'est réservé, il reste moins d'1 minute avant l'expiration | Une alerte visuelle apparaît sur l'écran de paiement |
| T02-US06 | Fonctionnel | Expiration effective sans paiement | Le délai de 5 minutes s'écoule sans paiement complété | Un message confirme que le siège a été libéré |
| T03-US06 | Fonctionnel | Paiement complété avant l'alerte | Le paiement est finalisé avant que le délai n'approche | Aucune alerte d'expiration n'est déclenchée |
| T04-US06 | Non-fonctionnel | Fiabilité du déclenchement | Répéter le scénario T01-US06 plusieurs fois | L'alerte se déclenche de façon constante, sans faux négatif |

#### Notes
- T02-US06 est directement lié au mécanisme de TTL Redis documenté dans US-04 (TASK-4.3).
- Ce scénario est à faible risque technique mais important pour l'expérience utilisateur lors des ventes flash.