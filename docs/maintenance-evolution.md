# Maintenance et évolution — TicketPulse (Volet 3)

## Déploiement continu
Pipeline CI/CD avec déploiement progressif (canary ou bleu-vert) pour éviter toute interruption pendant les périodes de faible trafic.

## Gestion des versions d'API
Versionnage explicite (/v1, /v2) pour garantir la compatibilité ascendante lors des évolutions futures.

## Plan de sauvegarde et reprise
Sauvegardes régulières de la base de données. Objectifs : RPO (perte de données maximale tolérée) de 5 minutes, RTO (temps de reprise) de 15 minutes.

## Feuille de route d'évolution
- **Phase 1** : MVP web (parcours d'achat complet)
- **Phase 2** : application mobile, paiements alternatifs
- **Phase 3** : déploiement multi-région pour réduire la latence géographique