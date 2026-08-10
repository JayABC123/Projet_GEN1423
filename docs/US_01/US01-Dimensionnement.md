### TASK-1.3 — Estimation de la charge de recherche

#### Objectif
Calculer le dimensionnement (QPS) spécifique à la fonctionnalité
de recherche d'événements.

#### Hypothèse
Selon le profil de charge , le système peut atteindre un pic global de 50 000 requêtes/s pendant les 10 premières minutes d'une vente très populaire. Nous estimons que 30 % de ces requêtes en période de pointe concernent la recherche ou la consultation d'événements, car les utilisateurs sont susceptibles d'effectuer plusieurs recherches et consultations avant de sélectionner un événement et de procéder au paiement. Les 70 % restants sont ainsi réservés aux autres opérations du système, notamment le processus de réservation et de paiement. Ce ratio est cohérent avec les patterns observés sur les plateformes e-commerce et de billetterie, où le trafic de lecture/consultation représente généralement une part importante du trafic total, largement supérieure au trafic d'écriture (paiement, réservation). Une estimation de 30 % dédiée uniquement à la recherche est donc raisonnable, voire conservatrice. Avec un pic global de 50 000 requêtes/s, la charge de recherche estimée est donc de 15 000 requêtes/s. Cette estimation permet de déterminer les besoins architecturaux, notamment l'utilisation potentielle d'un cache ou d'un moteur de recherche dédié.

#### Calcul

QPS_recherche = 50 000 × 0,30

QPS_recherche = 15 000 requêtes/s

#### Impact architectural
Avec une charge estimée à 15 000 requêtes/s pour la recherche,
il est pertinent d'envisager l'utilisation d'un cache (ex. Redis)
et/ou d'un moteur de recherche dédié (ex. Elasticsearch) plutôt
que de faire reposer toutes les recherches sur des requêtes SQL
directes.

#### Limites et risques associés
Cette approche introduit toutefois certaines limites à considérer :
 
- Désynchronisation des données (staleness) : un cache introduit un
  risque de désynchronisation entre les données affichées et l'état réel
  des événements (ex. disponibilité des sièges), particulièrement critique
  lors d'une vente flash où la disponibilité change rapidement. Une
  politique d'expiration courte (TTL) devra être appliquée pour limiter
  ce risque.
- Complexité opérationnelle accrue : l'ajout d'un moteur de recherche
  dédié (Elasticsearch) nécessite un mécanisme de synchronisation avec la
  base de données principale, ce qui ajoute un composant supplémentaire à
  maintenir et à surveiller.
- Coût de mise à l'échelle : en cas de sous-estimation du ratio de 30 %,
  le cache ou le moteur de recherche devra être en mesure de monter en
  charge horizontalement pour absorber un volume de requêtes supérieur aux
  15 000 requêtes/s estimées.