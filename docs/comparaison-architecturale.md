# Comparaison des styles architecturaux — TicketPulse

## Option A — Monolithique
**Avantages** : simplicité de développement et de déploiement, moins de complexité opérationnelle au départ.
**Inconvénients** : impossible de scaler indépendamment le service de réservation lors des pics ; un incident sur un module peut affecter tout le système ; déploiements plus risqués.

## Option B — Microservices événementiels (retenu)
**Avantages** : scalabilité indépendante par service (ex. scaler uniquement Inventaire/Réservation pendant une vente flash) ; isolation des pannes ; permet d'absorber les pics via une file de messages qui lisse la charge.
**Inconvénients** : complexité opérationnelle plus élevée, nécessite une gestion rigoureuse de la cohérence entre services (pattern Saga).

## Justification du choix
Le profil de charge de TicketPulse (pics de x250 le trafic normal, concentrés sur 10 minutes) rend le style microservices + événementiel nécessaire : c'est le seul qui permet de scaler uniquement les composants critiques (Inventaire, Réservation) sans sur-provisionner l'ensemble du système en permanence, ce qui serait coûteux et inutile 99 % du temps.

## Compromis et solutions rejetées
| Solution envisagée | Raison du rejet |
|---|---|
| Monolithique avec scaling vertical | Ne peut pas absorber un facteur x250 de charge en 10 minutes de façon rentable |
| Base de données unique sans réplicas | Goulot d'étranglement lors des pics de lecture (recherche d'événements) |
| Verrouillage uniquement en base de données (sans cache) | Latence trop élevée sous 50 000 req/s pour respecter le < 2 s |