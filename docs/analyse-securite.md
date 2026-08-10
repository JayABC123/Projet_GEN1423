# Analyse de sécurité — TicketPulse (Volet 3)

| Menace | Description | Contrôle proposé |
|---|---|---|
| Bots d'achat massif (scalping) | Scripts automatisés monopolisant les sièges | CAPTCHA, rate limiting par compte/IP, salle d'attente virtuelle |
| Falsification côté client | Manipulation du prix ou du siège dans la requête | Validation systématique côté serveur, jetons signés |
| Fuite de données de paiement | Interception ou stockage non sécurisé des données de carte | Tokenisation via le prestataire, TLS partout, conformité PCI-DSS |
| Déni de service | Surcharge délibérée ou accidentelle | WAF, auto-scaling, rate limiting, CDN en façade |
| Accès non autorisé à l'administration | Compromission d'un compte admin | MFA, RBAC |
| Répudiation d'une transaction | Litige sur un achat | Journalisation d'audit horodatée et immuable |