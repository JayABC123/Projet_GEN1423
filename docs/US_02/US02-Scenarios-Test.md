### TASK-2.1 — Scénarios de test

Les scénarios de test valident les comportements de la fonctionnalité US-02
(consultation du détail d'un événement), incluant l'affichage des
informations, la gestion des cas limites, et l'exigence non fonctionnelle
de temps de réponse.

| ID | Type | Scénario | Entrée / Action | Résultat attendu |
|---|---|---|---|---|
| T01-US02 | Fonctionnel | Affichage du détail d'un événement | Cliquer sur un événement depuis les résultats de recherche | La page affiche le lieu, la date, le prix et la disponibilité des sièges |
| T02-US02 | Fonctionnel | Événement complet (aucun siège disponible) | Consulter un événement dont tous les sièges sont vendus | Un message « Complet » est affiché, le bouton de réservation est désactivé |
| T03-US02 | Fonctionnel | Événement inexistant ou supprimé | Accéder à une URL d'événement invalide | Une page d'erreur claire est affichée (pas d'écran vide ou de crash) |
| T04-US02 | Non-fonctionnel | Temps de réponse | Charger la page de détail en conditions normales | Affichage complet en moins de 2 secondes |
| T05-US02 | Fonctionnel | Navigation retour | Depuis le détail, cliquer sur « Retour aux résultats » | L'utilisateur revient à sa recherche précédente avec les filtres conservés |

#### Notes
- T04-US02 valide l'exigence non fonctionnelle de temps de réponse commune à l'ensemble du système.
- T02-US02 est un cas critique lors des ventes flash, où la disponibilité change très rapidement.