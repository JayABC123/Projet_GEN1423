# US_01 - Recherche d'événements

## User Story
En tant que client, je souhaite rechercher un événement par nom, date ou catégorie afin de trouver rapidement les événements qui m'intéressent.

## Critères d'acceptation
- Recherche par mot-clé :
    Étant donné que je suis sur la page de recherche,
    Quand je saisis un mot-clé correspondant au nom d'un événement,
    Alors les événements correspondants s'affichent.

- Filtre par date et catégorie :
    Étant donné que j'ai effectué une recherche,
    Quand j'applique un filtre de date et/ou de catégorie,
    Alors seuls les événements correspondant à ces critères sont affichés.

- Temps de réponse :
    Étant donné que je lance une recherche,
    Quand le système traite ma requête,
    Alors les résultats s'affichent en moins de 2 secondes.

## Priorité
Must have

## Story Points
3

## Tâches

- TASK-1.1 - Modélisation du flux de recherche :
    Ce diagramme montre les interactions entre les différents composants lors d'une recherche.
    Le diagramme de séquence est disponible dans : `architecture/US01-flux-de-recherche.png`

- TASK-1.2 - Conception de l'écran de recherche :
    La maquette Figma montre la page avec laquelle le client interagira sur son ordinateur. Cette page de recherche comprend la page « Explorer » et une page pour les événements préférés, « Favoris ». Sur la page principale, on retrouve les événements en vedette, la barre de recherche avec une section pour les filtres et des icônes de catégorie. La bannière de chaque événement montre son titre, le type d'événement, la ville, le stade ou le lieu de déroulement, la date, le prix de base d'un billet, ainsi que les avis des utilisateurs.
    Lien : `https://wasp-dark-76166397.figma.site/`
    Capture du site ce trouve dans : `architecture/US01-flux-de-recherche.png`
    
