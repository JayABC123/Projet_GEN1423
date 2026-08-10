### TASK-3.7 — Scénarios de réussite

Les scénarios de test sont basés sur le parcours nominal du paiement de TicketPulse,
depuis la validation du paiement jusqu’à la génération et la réception du billet. Ils
permettent de valider que le paiement est correctement confirmé, que le billet contient
les informations attendues et que son intégrité est respectée.

| ID | Type | Scénario | Entrée / Action | Résultat attendu |
|---|---|---|---|---|
| T06-US04 | Fonctionnel | Paiement réussi de bout en bout | Soumettre un paiement valide | La transaction est confirmée et le siège est définitivement réservé |
| T07-US04 | Fonctionnel | Génération du billet après paiement | Confirmer le paiement | Un billet est généré avec un QR Code unique contenant les bonnes informations de l’événement |
| T08-US04 | Fonctionnel | Réception de la confirmation | Une fois le billet généré, déclencher l’envoi de la confirmation | Un courriel de confirmation est reçu avec le billet en pièce jointe ou un lien vers celui-ci |
| T09-US04 | Fonctionnel | Intégrité des données du billet | Générer un billet et vérifier les données encodées dans le QR Code | Le QR Code encode correctement l’identifiant du billet et les informations attendues sont vérifiables |

#### Notes

- T06-US04 valide le parcours nominal complet du paiement, de la soumission jusqu’à
  la confirmation de la réservation.
- T07-US04 vérifie que la génération du billet est déclenchée après la confirmation
  du paiement et que le QR Code est unique.
- T08-US04 vérifie la réception de la confirmation par le client.
- T09-US04 valide l’intégrité des données présentes dans le billet et dans son QR Code.
- L’ensemble de ces scénarios couvre le parcours de réussite attendu de l’US-04.