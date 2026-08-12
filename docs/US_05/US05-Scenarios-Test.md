### TASK-5.1 — Scénarios de test

Les scénarios de test valident la consultation du plan de salle en temps
réel (US-05), en particulier la mise à jour dynamique du statut des sièges
et l'exigence de latence d'affichage.

| ID | Type | Scénario | Entrée / Action | Résultat attendu |
|---|---|---|---|---|
| T01-US05 | Fonctionnel | Affichage initial du plan de salle | Accéder à la page de sélection des sièges d'un événement | Le plan s'affiche avec le statut de chaque siège (disponible/verrouillé/vendu) |
| T02-US05 | Fonctionnel | Mise à jour en temps réel | Un autre client verrouille un siège pendant que je consulte le plan | Le statut du siège se met à jour sans rechargement de page |
| T03-US05 | Fonctionnel | Libération d'un siège après expiration | Un siège verrouillé par un autre client expire (délai de 5 min écoulé) | Le siège redevient visuellement disponible sans action de ma part |
| T04-US05 | Non-fonctionnel | Temps d'affichage | Charger le plan de salle en conditions normales | Affichage complet en moins de 2 secondes |
| T05-US05 | Charge | Affichage en pic de charge | Simuler une consultation massive du plan de salle lors d'une vente flash | Le système maintient l'affichage en temps réel sans dégradation majeure |

#### Notes
- T02-US05 et T03-US05 sont directement liés au mécanisme de verrouillage Redis (voir US-04, TASK-4.3).
- T04-US05 et T05-US05 alimentent le plan de validation de la performance du Volet 3.