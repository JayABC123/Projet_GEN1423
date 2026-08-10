# Analyse du système — TicketPulse

## Parties prenantes
- Client (acheteur de billets)
- Administrateur (organisateur/gestionnaire d'événements)
- Fournisseur de paiement externe (Stripe ou équivalent)
- Équipe d'exploitation (supervision, maintenance)

## Besoins fonctionnels
- Recherche et consultation d'événements
- Consultation du plan de salle en temps réel
- Réservation temporaire d'un siège
- Paiement sécurisé et génération automatique du billet (QR Code)
- Notification d'expiration de réservation
- Tableau de bord des ventes (admin)

## Besoins non fonctionnels
- Disponibilité élevée durant les ventes flash (jusqu'à 250 000 utilisateurs simultanés)
- Temps de réponse < 2 s pour la majorité des requêtes
- Finalisation du paiement en moins de 5 minutes
- Aucune surréservation de siège, même en accès concurrent élevé
- Sécurité des données de paiement (conformité PCI-DSS)

## Contraintes
- Charge très variable : ~1000 utilisateurs/jour en temps normal, jusqu'à 50 000 req/s en pointe
- Fenêtre critique très courte (10 premières minutes d'une vente flash)
- Intégration obligatoire avec un fournisseur de paiement externe

## Hypothèses retenues (non fournies dans l'énoncé)
- Taille moyenne d'un message de recherche/réservation : ~2 Ko en entrée, ~5 Ko en sortie
- Durée de blocage temporaire d'un siège : 5 minutes (alignée sur la fenêtre de paiement)
- Taux de conversion en vente flash : ~5 % des connexions aboutissent à un achat
- Un seul événement en vente flash à la fois (scénario dimensionnant du pire cas)