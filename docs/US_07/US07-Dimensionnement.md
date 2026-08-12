# TASK-7.3 — Estimation de la charge du tableau de bord administrateur

## Objectif

Estimer la charge générée par la consultation et le rafraîchissement du tableau
de bord des ventes afin de vérifier que cette fonctionnalité peut fonctionner
sans affecter les opérations critiques de réservation et de paiement.

## Hypothèse

Le système peut atteindre un pic global de 50 000 requêtes/s pendant les
10 premières minutes d'une vente très populaire.

Contrairement à la recherche, à la consultation des événements ou à la
réservation, le tableau de bord des ventes est uniquement destiné aux
administrateurs. Le nombre d'utilisateurs simultanés de cette fonctionnalité
est donc supposé être beaucoup plus faible.

Nous supposons, pour le dimensionnement, qu'un maximum de 100 administrateurs
consultent simultanément un tableau de bord pendant une période de forte
activité.

Selon les critères d'acceptation de l'US-07, les statistiques doivent être
actualisées au moins une fois par minute.

Cette valeur de 100 administrateurs simultanés constitue une hypothèse de
dimensionnement et devra être validée à partir de données réelles si le
système est déployé en production.

## Calcul

Nombre d'administrateurs simultanés = 100

Fréquence de rafraîchissement = 1 requête/minute

QPS_dashboard = 100 / 60

QPS_dashboard ≈ 1,67 requête/s

La charge directe du tableau de bord reste donc faible comparativement au
pic global de 50 000 requêtes/s.

## Impact architectural

Même si le nombre de requêtes provenant des administrateurs est relativement
faible, les requêtes du tableau de bord peuvent être coûteuses puisqu'elles
nécessitent le calcul de statistiques telles que :

- le nombre de billets vendus ;
- le nombre de billets disponibles ;
- le revenu total généré.

Afin d'éviter d'effectuer des agrégations coûteuses sur les données
transactionnelles à chaque consultation, les statistiques peuvent être
pré-calculées ou mises en cache.

Le tableau de bord peut ensuite récupérer périodiquement ces statistiques,
avec une fréquence compatible avec l'exigence de rafraîchissement d'au moins
une fois par minute.

## Limites et risques associés

Cette approche introduit certaines limites :

- Les statistiques affichées peuvent avoir un léger retard par rapport aux
  transactions réelles.
- Une fréquence de rafraîchissement trop élevée augmenterait inutilement la
  charge du système.
- Les calculs d'agrégation ne doivent pas ralentir les opérations critiques
  de réservation et de paiement.
- Le nombre réel d'administrateurs simultanés pourrait être différent de
  l'hypothèse retenue.
