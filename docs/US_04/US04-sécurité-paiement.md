## TASK-3.3 - Analse de la sécurité du paiement

#### Menaces identifiées
- Interception des données de paiement en transit (attaque man-in-the-middle)
- Rejeu de transaction (replay attack) pour dupliquer un paiement
- Fraude par vol de carte ou usurpation d'identité
- Injection ou manipulation des montants côté client

#### Mécanismes de mitigation
- Chiffrement TLS 1.3 pour toutes les communications
- Délégation du traitement des données de carte à une passerelle de
  paiement certifiée PCI-DSS (ex. Stripe) — l'application ne stocke
  jamais les données de carte brutes
- Génération d'un identifiant de transaction unique (idempotency key)
  pour éviter les doubles soumissions
- Validation des montants exclusivement côté serveur, jamais confiée au client
- Journalisation des tentatives de paiement pour audit et détection
  d'anomalies