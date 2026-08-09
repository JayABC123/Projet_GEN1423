# US_02 - Réservation temporaire de siège

## User Story
En tant que client,
je veux réserver temporairement un siège pendant que je complète mon paiement,
afin de m'assurer que personne d'autre ne puisse l'acheter durant ma transaction.

## Critères d'acceptation
- Verrouillage du siège :
    Étant donné qu'un siège est disponible
    Quand je le sélectionne
    Alors il est verrouillé pendant 5 minutes pour les autres utilisateurs

- Visibilité pour les autres utilisateurs :
    Étant donné qu'un siège est verrouillé par un autre client
    Quand je consulte le plan de salle
    Alors ce siège apparaît comme indisponible

- Expiration ou annulation de la transaction :
    Étant donné qu'un siège est verrouillé
    Quand le paiement est annulé ou que le délai de 5 minutes expire
    Alors le siège redevient disponible pour les autres utilisateurs

- Protection contre la double réservation :
    Étant donné qu'un siège est déjà verrouillé
    Quand un autre utilisateur tente de le sélectionner simultanément
    Alors le système empêche cette double réservation

## Priorité
Must have

## Story Points
8