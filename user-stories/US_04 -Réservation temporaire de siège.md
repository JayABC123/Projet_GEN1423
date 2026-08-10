# US_04 - Consultation du plan de salle en temps réel

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
