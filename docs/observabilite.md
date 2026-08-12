# Observabilité — TicketPulse (Volet 3)

## Journalisation centralisée
Logs structurés (JSON) de chaque microservice, agrégés dans une pile centralisée (ex. ELK ou Grafana Loki), avec un identifiant de corrélation unique par requête pour suivre une transaction à travers tous les services.

## Supervision (monitoring)
Tableaux de bord temps réel (Prometheus + Grafana) sur : débit, latence, taux d'erreur, profondeur des files de messages, occupation des verrous Redis.

## Traçabilité distribuée
Traçage de bout en bout (OpenTelemetry) pour identifier le service responsable d'une latence anormale lors d'une transaction.

## Alertes
Seuils automatiques déclenchant une alerte : p95 > 2 s, taux d'erreur > 1 %, file de messages au-delà d'un seuil critique. Escalade si non résolu dans un délai défini.

## Vérifications de santé (health checks)
Sondes actives sur chaque service pour retirer automatiquement une instance défaillante du répartiteur de charge.