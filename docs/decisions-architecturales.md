# Tableau des décisions architecturales — TicketPulse

| Décision | Justification |
|---|---|
| Microservices + architecture événementielle | Scalabilité indépendante requise pour absorber les pics x250 |
| Verrou Redis (TTL 5 min) + contrainte unique PostgreSQL | Double protection contre la surréservation, faible latence |
| File de messages pour notifications et statistiques | Découplage, lissage de charge, aucune perte d'événement |
| Réplicas de lecture PostgreSQL | Isoler les lectures (recherche) des écritures critiques (réservation) |
| Tokenisation via fournisseur externe pour le paiement | Conformité PCI-DSS sans stocker de données de carte |