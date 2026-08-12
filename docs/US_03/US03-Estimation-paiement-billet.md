### US-03 - Estimation de la charge de paiement et de génération du billet 

#### Objectif
Calculer le dimensionnement (QPS et débit) spécifique à la fonctionnalité
de paiement sécurisé et de génération automatique du billet électronique.

#### Hypothèses
Contrairement à la recherche (US-01) et à la réservation (US-04), le
paiement n'est accessible qu'aux utilisateurs ayant déjà réussi à
verrouiller un siège. Le trafic de paiement est donc naturellement
borné par le nombre de réservations réussies, et non par le pic brut
de 50 000 requêtes/s.

En reprenant l'hypothèse posée dans TASK-1.5 (capacité de l'événement
estimée à 20 000 sièges), nous supposons que la quasi-totalité des
utilisateurs ayant réservé un siège complètent leur paiement dans le
délai imparti de 5 minutes (300 secondes), tel que défini par l'exigence
« finalisation du paiement en moins de 5 minutes ».

Nous appliquons également un facteur de sécurité de 2x sur le débit
moyen, afin de tenir compte du fait que les paiements ne se répartissent
pas uniformément dans le temps : une proportion importante des
utilisateurs ayant réservé au tout début de la fenêtre de 10 minutes
tentera de payer rapidement, créant un sous-pic de charge.

Enfin, nous estimons que le trafic total observé sur l'API de paiement
(incluant les requêtes de statut, les tentatives échouées et les
nouvelles tentatives après refus) représente environ 15 % du pic
global de 50 000 requêtes/s, ce qui sert de validation croisée par
rapport à l'estimation basée sur la capacité.

#### Calcul

Approche 1 — basée sur la capacité de l'événement (débit de transactions réussies) :

Débit_moyen_paiement = 20 000 sièges / 300 secondes

Débit_moyen_paiement ≈ 66,7 transactions/s

Débit_pic_paiement = 66,7 x 2 (facteur de sécurité)

Débit_pic_paiement ≈ 133 transactions/s

Approche 2 — basée sur le pourcentage du pic global (validation croisée, inclut retries/statuts) :

QPS_paiement = 50 000 x 0,15

QPS_paiement = 7 500 requêtes/s

Constat : l'écart entre les deux approches (133 transactions réussies/s
vs 7 500 requêtes/s au total) s'explique par le fait que la seconde
inclut l'ensemble du trafic lié au paiement (validation de formulaire,
requêtes de statut, tentatives échouées, actualisations côté client),
alors que la première ne mesure que les transactions effectivement
complétées avec succès.

Débit de génération de billets :

Puisque chaque paiement réussi déclenche la génération d'un billet
(voir SCRUM-23), le débit de génération suit directement le débit de
paiements réussis :

Débit_generation_billets ≈ 133 billets/s en pic

#### Impact architectural
- Le service de paiement doit être capable de traiter environ 7 500
  requêtes/s au total (incluant les validations et tentatives), mais le
  débit réel de transactions financières complétées reste beaucoup plus
  faible (~133/s en pic), ce qui reste largement gérable par une
  passerelle de paiement externe (ex. Stripe) sans risque de goulot
  d'étranglement majeur.
- Le service de génération de billets (architecture asynchrone retenue
  dans SCRUM-23) doit être dimensionné pour absorber au minimum 133
  générations de billets par seconde en période de pointe, avec une file
  de messages capable d'absorber les pics sans perte de message.
- Le facteur de sécurité de 2x appliqué au débit moyen de paiement
  justifie le choix d'une architecture pouvant monter en charge
  horizontalement (ajout de workers de génération de billets) plutôt
  qu'une capacité fixe.

#### Limites et risques associés
- Dépendance à la passerelle de paiement externe : la capacité réelle
  de traitement dépend aussi des limites imposées par le fournisseur de
  paiement tiers (ex. quotas de requêtes par seconde), qui doivent être
  vérifiées contractuellement et ne sont pas sous le contrôle direct du
  système.
- Sous-estimation de la capacité de l'événement :
 si le nombre réel de sièges dépasse notre hypothèse de
  20 000, le débit de paiements et de génération de billets devra être
  révisé à la hausse.
- Accumulation de messages en cas de panne temporaire : si le service
  de génération de billets est temporairement indisponible, les messages
  s'accumulent dans la file ; un débit de rattrapage (catch-up) supérieur
  au débit nominal doit être prévu pour résorber le retard sans dépasser
  le délai raisonnable de réception du billet par le client.