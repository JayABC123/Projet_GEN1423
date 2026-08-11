# Stratégie de données — TicketPulse

## Modèle et technologies retenues
- **PostgreSQL** pour les données transactionnelles (événements, sièges, réservations, paiements) — cohérence forte requise pour éviter la surréservation
- **Redis** pour le cache de lecture (recherche d'événements) et les verrous temporaires de sièges (TTL 5 min)
- **File de messages (Kafka ou équivalent)** pour découpler les services et lisser les pics (notifications, mise à jour de statistiques)

## Organisation des données
- Table `evenements`, `sieges` (statut : disponible/verrouillé/vendu), `reservations`, `paiements`
- Contrainte d'unicité `(event_id, seat_id)` sur les réservations confirmées — filet de sécurité derrière le verrou applicatif

## Distribution et optimisation
- Réplicas de lecture PostgreSQL pour absorber les requêtes de recherche/consultation sans affecter les écritures critiques (réservation/paiement)
- Cache Redis en façade des lectures fréquentes (liste d'événements, plan de salle)

## Conservation et disponibilité
- Sauvegardes régulières de la base transactionnelle (quotidiennes + réplication)
- Objectifs : RPO (perte maximale tolérée) de 5 minutes, RTO (temps de reprise) de 15 minutes