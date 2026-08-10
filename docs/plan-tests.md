# Plan de tests — TicketPulse (Volet 3)

## Types de tests couverts
- Tests unitaires : logique de calcul du prix, règles de verrouillage de siège, génération du QR code (couverture cible 80 % sur Réservation et Paiement)
- Tests d'intégration : Réservation ↔ Redis, Paiement ↔ passerelle externe (sandbox), API Gateway ↔ tous les services
- Tests de non-régression : exécutés automatiquement dans le pipeline CI
- Tests de charge/performance : simulation de la vente flash
- Tests de sécurité : scan OWASP ZAP + revue manuelle des flux d'authentification et de paiement
- Tests d'acceptation (UAT) : scénarios de bout en bout validés avec le product owner

## Scénarios de tests représentatifs

| Scénario | Étapes clés | Résultat attendu |
|---|---|---|
| Réservation simultanée du même siège | 2 utilisateurs cliquent sur le même siège à < 100 ms d'intervalle | Un seul obtient le verrou ; l'autre reçoit "siège indisponible" immédiatement |
| Expiration du délai de paiement | Un siège est réservé mais le paiement n'est pas complété en 5 min | Le siège redevient disponible automatiquement |
| Paiement refusé | La carte est refusée par le fournisseur | Le siège est libéré immédiatement ; message d'erreur clair |
| Pic de charge (vente flash) | Montée à 50 000 req/s en moins d'une minute | p95 < 2 s ; taux d'erreur < 0,1 % |
| Génération du billet | Paiement confirmé | QR code généré et courriel envoyé en < 30 s |

## Indicateurs de performance (KPI)

| Indicateur | Cible |
|---|---|
| Latence p95 (lecture/recherche) | < 2 s |
| Latence p99 (verrouillage de siège) | < 200 ms |
| Débit soutenu (pointe) | 50 000 req/s pendant 10 min |
| Taux d'erreur | < 0,1 % |
| Délai de finalisation du paiement | < 5 min |