# Cohérence, disponibilité et résilience — TicketPulse

## Accès concurrents
Double protection contre la surréservation : verrou distribué Redis (SETNX + TTL 5 min) posé dès la sélection du siège, puis contrainte d'unicité en base de données comme dernier rempart transactionnel.

## Erreurs et pannes
- Panne du fournisseur de paiement : circuit breaker + file de retry, basculement vers un fournisseur secondaire si disponible
- Panne d'une instance de service : health checks actifs, retrait automatique du répartiteur de charge

## Pertes ou retards de communication
- Les événements critiques (confirmation de paiement, libération de siège) transitent par une file de messages persistante, garantissant qu'aucun événement n'est perdu même en cas de ralentissement temporaire d'un service consommateur

## Surcharge
- Auto-scaling horizontal des services Recherche et Réservation en fonction du débit entrant
- Salle d'attente virtuelle activée au-delà d'un seuil de requêtes simultanées pour protéger le système

## Reprise après incident
- RPO 5 min / RTO 15 min (voir stratégie de données)
- Tests de bascule (failover) réguliers pour valider la continuité de service