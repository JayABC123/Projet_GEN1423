# Registre des risques — TicketPulse

| # | Risque | Catégorie | Probabilité | Impact | Mitigation |
|---|---|---|---|---|---|
| R1 | Surréservation d'un même siège lors d'un pic | Sujet/exigences | Moyenne | Élevé | Verrou distribué + contrainte unique en BD |
| R2 | Panne de la passerelle de paiement externe | Technique | Faible | Élevé | Circuit breaker, file de retry, fournisseur secondaire |
| R3 | Bots/scalpers monopolisant les sièges | Sujet/exigences | Élevée | Moyen | Rate limiting, CAPTCHA, salle d'attente virtuelle |
| R4 | Sous-estimation de la charge réelle (>50k req/s) | Sujet/exigences | Moyenne | Élevé | Auto-scaling, tests de charge réguliers |
| R5 | Répartition inégale du travail dans l'équipe | Organisationnel | Moyenne | Moyen | Suivi hebdomadaire des billets Jira par membre |
| R6 | Contribution Git concentrée en fin de projet | Organisationnel | Moyenne | Élevé | Sprints courts, jalons intermédiaires obligatoires |
| R7 | Incohérence des données entre microservices | Technique | Moyenne | Élevé | Pattern Saga + événements idempotents |
| R8 | Fuite de données de paiement | Sujet/exigences | Faible | Élevé | Tokenisation via prestataire, aucune donnée carte stockée |