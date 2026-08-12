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

- TASK 1.1 - Modélisation du flux de recherche :
    Ce diagramme montre les interactions entre les différents composants lors d'une recherche.
    Le diagramme de séquence est disponible dans : `architecture/US01-flux-de-recherche.png`

- TASK 1.2 - Conception de l'écran de recherche :
    La maquette Figma montre la page avec laquelle le client interagira sur son ordinateur. Cette page de recherche comprend la page « Explorer » et une page pour les événements préférés, « Favoris ». Sur la page principale, on retrouve les événements en vedette, la barre de recherche avec une section pour les filtres et des icônes de catégorie. La bannière de chaque événement montre son titre, le type d'événement, la ville, le stade ou le lieu de déroulement, la date, le prix de base d'un billet, ainsi que les avis des utilisateurs.
    Lien : `https://www.figma.com/make/Y7OPqnox7n6bIal6D1ur8O/TicketPulse--Community-?fullscreen=1&t=79Qxrs7n4NeDkdFx-1&code-node-id=0-9`
    Capture du site est disponible dans : `architecture/TicketPulse-UI.png`
    
- TASK 1.3 - Estimation de la charge de recherche :
    Cette tâche consiste à estimer la charge de la fonctionnalité de recherche à partir du profil de charge global du système. Cette estimation permet d'identifier les besoins architecturaux, notamment l'utilisation potentielle d'un cache ou d'un moteur de recherche dédié.
    Le fichier contenant l'estimation détaillé est disponible dans : `docs/US_01/US01-Dimensionnement.md`

- TASK 1.4 - Scénario de test :
    Cette tâche consiste à définir des scénarios de test permettant de valider les principaux comportements de la recherche d'événements de TicketPulse, notamment la recherche par mot-clé, les filtres, les recherches sans résultat et les champs vides. Les tests couvrent également les exigences non fonctionnelles liées au temps de réponse inférieur à 2 secondes ainsi que la capacité du système à supporter la charge estimée de 15 000 requêtes/s définie dans la TASK-1.3.
    Le fichier contenant les scénarios de test est disponible dans : `docs/US_01/US01-Scéanarios-testing.md`