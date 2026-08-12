# US_04 - Réservation temporaire du siège

## User Story
En tant que client, je veux réserver temporairement un siège pendant que je complète mon paiement, pour m’assurer que personne d'autre ne puisse l'acheter durant ma transaction.

## Critères d'acceptation
- Vérrouillage du siège :
    Étant donné qu'un siège est disponible,
    Quand je le sélectionne,
    Alors il est verrouillé pendant 5 minutes pour les autres utilisateurs.

- Visibilité pour les autres utilisateurs :
    Étant donné qu'un siège est disponible,
    Quand je le sélectionne,
    Alors il est verrouillé pendant 5 minutes pour les autres utilisateurs.

- Expiration ou annulation de la transaction :
     Étant donné qu'un siège est verrouillé, 
     Quand le paiement est annulé ou que le délai de 5 minutes expire, 
     Alors le siège redevient disponible pour les autres utilisateurs.

- Protection contre la double réservation :
    Étant donné qu'un siège est déjà verrouillé, 
    Quand un autre utilisateur tente de le sélectionner simultanément, 
    Alors le système empêche cette double réservation


## Priorité
Must have

## Story Points
7

## Tâches

- TASK 4.1 - Définir les critères d'acceptation de la réservation :
    Les critères d'acceptation de la réservation sont définis ci-dessus. Cette tâche consiste à les valider et à s'assurer qu'ils couvrent les différents scénarios de verrouillage temporaire, de visibilité pour les autres utilisateurs, d'expiration/annulation et de protection contre la double réservation.

- TASK 4.2 - Conception du diagramme de séquence de réservation :

- TASK 4.3 - Analyse du mécanisme de réservation temporaire :
    Cette tâche consiste à définir le mécanisme de verrouillage temporaire permettant de réserver exclusivement un siège pendant 5 minutes. La solution retenue repose sur un verrou distribué avec expiration automatique (TTL) via Redis, afin de gérer efficacement les accès simultanés et d'éviter les doubles réservations lors des périodes de forte charge.
    Le fichier d'analyse du mécanisme de réservation temporaire est disponible dans : `docs/US_04/US04-Mécanisme-Réservation.md`

- TASK 4.4 - Analyser la concurrence et la double réservation : 
    Cette tâche consiste à analyser les cas de concurrence entre utilisateurs, à définir les règles de priorité et de résolution des conflits, et à vérifier que le système empêche toute double réservation du même siège pendant la période de verrouillage.
    Le fichier d'analyse de la concurrence est disponible dans : `docs/US_04/US04-Analyse-Concurrence.md`

- TASK 4.5 - Définir les scénarios d'erreur : 
    Cette tâche consiste à définir les principaux cas d'erreur liés à la réservation, notamment lorsqu'un siège est déjà verrouillé, lorsque le délai expire ou lorsqu'une réservation est annulée.
    Le fichier contenant les scénarios de test est disponibles dans : `docs/US_04/US04-Scénarios-Test.md`