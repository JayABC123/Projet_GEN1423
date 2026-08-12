# Dimensionnement — TicketPulse

## Hypothèses de base
- Pic : 50 000 req/s pendant les 10 premières minutes, puis décroissance sur 30 minutes
- Taille moyenne d'une requête de recherche : ~2 Ko entrée / ~5 Ko sortie
- Conversion en achat : ~5 % des connexions en vente flash

## Calculs
- **Volume de requêtes en fenêtre critique** : 50 000 req/s × 600 s = 30 000 000 requêtes en 10 minutes
- **Débit réseau en pointe (sortie)** : 50 000 req/s × 5 Ko ≈ 250 Mo/s à absorber par la couche cache/CDN
- **Réservations simultanées estimées** : 5 % de 250 000 utilisateurs connectés ≈ 12 500 tentatives de réservation en quelques minutes
- **QPS moyen hors pointe** : 1000 utilisateurs/jour ≈ 0,01 req/s en moyenne — écart de plusieurs ordres de grandeur avec la pointe, ce qui justifie l'auto-scaling plutôt qu'un provisionnement fixe

## Limites identifiées
- Au-delà de 50 000 req/s soutenu, une couche de limitation (salle d'attente virtuelle) devient nécessaire pour protéger le service Réservation
- Le verrou Redis doit supporter au minimum 12 500 opérations SETNX/seconde en pointe