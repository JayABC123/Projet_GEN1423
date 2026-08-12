# Volet 2 - Analyse,conception logicielle et architecture système

## Livrable du volet 2

### Dossier d'architecture

- Le dossier `architecture/` regroupe l'ensemble des livrables de conception 
et d'architecture système du projet TicketPulse, c'est--dire les diagrammes de cas 
d'utilisation et de séquence, choix du style architectural, diagramme 
d'architecture globale, stratégie de données, calculs de dimensionnement, 
ainsi que le tableau des décisions architecturales et des compromis 
retenus.

### Diagrammes

- Cette section regroupe le diagramme de cas d'utilisation et les 
diagrammes de séquence illustrant les principaux scénarios du système 
(recherche d'événement, réservation temporaire de siège, paiement et 
génération du billet).

- Les diagrammes sont disponible dans le dossier `architecture/` dans leur dossier respectif : `architecture/US_0X`

### Les interfaces de l'application

- Les maquettes Figma haute fidélité présentent le parcours utilisateur 
principal de TicketPulse, incluant au minimum les écrans de recherche, 
de sélection de siège, de paiement et de confirmation du billet.

- Le fichier contenant le lien de la maquette est disponible dans : `figma/liens-maquettes.md`

### Calculs de dimensionnement

- Cette section présente l'ensemble des estimations de charge du système 
(QPS, débit, volume de stockage) pour les fonctionnalités critiques de 
recherche, de réservation et de paiement, avec les hypothèses et 
formules justifiées.

- Le fichier globale est disponibles dans : `docs/dimensionnement-globale.md`

- Les autres fichiers sont disponibles dans leur dossier respectif si applicable : `docs/US_0X/FILE.md`

### Tableau des décisions architecturales

- Ce tableau documente les principaux choix techniques retenus pour 
l'architecture de TicketPulse (ex. verrouillage distribué, génération 
asynchrone du billet, mise à jour temps réel du plan de salle) ainsi 
que leur justification.

-Le fichier contenant le tableau des décisions architecturales est disponible dans : `docs/decisions-architecturales.md`


### Tableau des compromis et solutions rejetées

- Ce document recense les alternatives envisagées mais écartées pour 
chaque décision architecturale majeure, avec la justification du rejet 
et le compromis finalement accepté.

- Le fichier contenant le tableau des compromis et solutions rejetées est disponible dans : `Livrables/Volet 2/ Tableau des compromis et solutions rejetées.md`