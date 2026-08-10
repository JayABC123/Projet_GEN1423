### TASK-1.4 — Scénario de test
 
Les scénarios de test sont basés sur les éléments de l'interface de recherche
de TicketPulse, notamment la barre de recherche, les filtres par catégorie,
le bouton de filtres avancés et l'affichage des résultats. Ils permettent de
valider les principaux comportements de la fonctionnalité US-01, incluant
les recherches avec résultats, sans résultat, ainsi que les exigences non
fonctionnelles de temps de réponse et de charge établies dans TASK-1.3.
 
| ID | Type | Scénario | Entrée / Action | Résultat attendu |
|---|---|---|---|---|
| T01-US01 | Fonctionnel | Recherche par mot-clé | Saisir « Simple Plan » | Les événements correspondants sont affichés |
| T02-US01 | Fonctionnel | Filtrage par catégorie | Cliquer sur « Concerts » | Seuls les concerts sont affichés |
| T03-US01 | Fonctionnel | Filtrage combiné | Utiliser « Filtres » avec une période et une fourchette de prix | Seuls les événements correspondants sont affichés |
| T04-US01 | Fonctionnel | Recherche sans résultat | Saisir « xyz123 » | « Aucun événement trouvé » est affiché |
| T05-US01 | Fonctionnel | Recherche avec champ vide | Laisser le champ vide et lancer la recherche | Tous les événements sont affichés |
| T06-US01 | Non-fonctionnel | Temps de réponse | Lancer une recherche en conditions normales de charge | Résultats affichés en moins de 2 secondes |
| T07-US01 | Charge | Recherche en pic de charge | Simuler 15 000 requêtes/s sur l'endpoint de recherche (voir TASK-1.3) | Le système maintient un temps de réponse acceptable, sans erreur ni indisponibilité |
 
#### Notes
- T06-US01 et T07-US01 valident les exigences non fonctionnelles de la
  US-01 (temps de réponse inférieur à 2 secondes) et le dimensionnement estimé dans
  TASK-1.3 (15 000 requêtes/s en pic).
- T07-US01 est également référencé dans le plan de validation de la
  performance et les scénarios de charge du Volet 3.
 