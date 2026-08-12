###  US-04 - Estimation de la charge de réservation de siège 

#### Objectif
Calculer le dimensionnement (QPS) spécifique à la fonctionnalité de
réservation temporaire de siège, incluant les tentatives de verrouillage
concurrentes.

#### Hypothèses
Selon le profil de charge du sujet, le système peut atteindre un pic
global de 50 000 requêtes/s pendant les 10 premières minutes d'une vente
très populaire (rappel du profil de charge global fourni dans l'énoncé).

Nous estimons que 40 % des requêtes en période de pointe concernent
la tentative de réservation (verrouillage) d'un siège. Ce pourcentage est
plus élevé que celui de la recherche (30 %, voir TASK-1.3), car il s'agit
de l'action la plus disputée du système : dès qu'un siège devient
visible, un grand nombre d'utilisateurs tentent de le verrouiller
simultanément, générant à la fois des requêtes réussies et des requêtes
en échec dues à la contention (accès concurrents).

Nous posons également une hypothèse sur la capacité de l'événement,
non fournie dans l'énoncé : nous estimons qu'un événement à forte
demande dispose d'environ 20 000 sièges. Cette hypothèse permet de
distinguer le volume brut de requêtes (tentatives, incluant les échecs)
du volume de réservations effectivement réussies, qui est plafonné par
le nombre de sièges disponibles.

#### Calcul

Volume brut de requêtes (tentatives de verrouillage) :

QPS_reservation = 50 000 x 0,40

QPS_reservation = 20 000 requêtes/s

Réservations effectivement réussies (bornées par la capacité) :

Réservations max = 20 000 sièges (capacité totale de l'événement)

Ces 20 000 réservations réussies se répartissent sur les 10 premières
minutes (600 secondes) d'affluence maximale :

Débit_reservations_reussies = 20 000 / 600

Débit_reservations_reussies ≈ 33,3 réservations réussies/s en moyenne

Constat : le système doit donc absorber un volume de requêtes très
supérieur (20 000 req/s) au nombre de réservations réellement traitées
avec succès (~33 réservations/s), la majorité des requêtes en pic
correspondant à des tentatives échouées sur des sièges déjà verrouillés.

#### Impact architectural
- Le service de verrouillage (Redis) doit être capable de traiter
  jusqu'à 20 000 opérations `SETNX` par seconde, ce qui nécessite un
  cluster Redis avec réplication et partitionnement (sharding) plutôt
  qu'une instance unique.
- Une file d'attente virtuelle (virtual waiting room) en amont du
  service de réservation est recommandée pour lisser les pics de
  connexions simultanées (jusqu'à 250 000 utilisateurs) et éviter de
  submerger le service de verrouillage dès l'ouverture de la vente.
- Le nombre élevé de requêtes en échec (siège déjà pris) doit être traité
  efficacement côté cache, sans jamais solliciter la base de données
  relationnelle pour les tentatives infructueuses, afin d'éviter une
  contention inutile sur la source de vérité principale.

#### Limites et risques associés
- Effet de horde (thundering herd) : au moment précis de l'ouverture
  de la vente, une explosion simultanée de requêtes peut dépasser
  temporairement la capacité du cluster Redis si celui-ci n'est pas
  pré-dimensionné pour absorber le pic initial.
- Sous-estimation de la capacité de l'événement : si le nombre réel
  de sièges dépasse notre hypothèse de 20 000, le débit de réservations
  réussies sera plus élevé que prévu ; le dimensionnement devra être
  révisé à la hausse en conséquence.
- Iniquité d'accès : sans file d'attente virtuelle, les utilisateurs
  avec une latence réseau plus faible pourraient systématiquement
  obtenir un avantage lors des tentatives de verrouillage simultanées.