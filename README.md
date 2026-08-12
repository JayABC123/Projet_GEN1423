# TicketPulse - Plateforme de billetterie d'événements en temps réel

### Cours : GEN1423 — Génie Logiciel
### Professeur : Abderrahmane Ben Mimoune
### Équipe : Groupe 5
### Membres :

- Akamah, Kokou Jean-Jacques | AKAK84280601 |  akak21@uqo.ca
- Aka, Andjui Melchisedek Ange-E | AKAA83340701 | akaa25@uqo.ca
- Banaken, Gladys Eméline | BANG71560402 | bang08@uqo.ca

## Description du projet

TicketPulse est une application de billetterie permettant aux utilisateurs de rechercher des événements, consulter les disponibilités, réserver temporairement un siège, effectuer un paiement sécurisé et recevoir un billet électronique avec un QR Code. Le projet met également l'accent sur la performance, la sécurité et la gestion de la concurrence afin de supporter une forte charge d'utilisateurs.

## Structure du dépôt

Le dépôt est organisé de la manière suivante :

- `Librables/` : document des volet 1,2 et 3 contenant les livrables et le bilan de contribution des membres
- `architecture/` : diagrammes et documents liés à l’architecture du système.
- `docs/` : documentation générale et livrables du projet.
- `figma/` : liens et références vers les maquettes Figma.
- `user-stories/` : documentation des User Stories, critères d’acceptation, priorités et Story Points.
- `README.md` : présentation générale du projet et organisation du dépôt.


## Hypthèses clés

Les principales hypothèses retenues pour la conception de TicketPulse sont :

- Une réservation temporaire d’un siège expire après un délai maximal de 5 minutes.
- Un siège peut avoir les états `AVAILABLE`, `HELD` ou `SOLD`.
- Les opérations de consultation sont beaucoup plus fréquentes que les opérations d’écriture.
- Les ventes flash peuvent concentrer une grande partie du trafic sur un même événement.
- Le traitement du paiement est délégué à un fournisseur de paiement externe.
- L’envoi des courriels de confirmation est effectué de manière asynchrone.
- Les plans de salle changent peu et peuvent donc être mis en cache.
- Une réservation temporaire appartient à un seul client ou à une seule session.
- Les opérations critiques de réservation doivent garantir qu’un siège ne puisse jamais être vendu deux fois.

## Contribution de l'équipe
 
La répartition des principales tâches est documentée dans Jira et les 
contributions aux livrables sont également suivies dans GitHub.

Le bilan complet de contribution des membres est disponible dans : `Livrables/Volet 1/Bilan de contribution.md`

### Jean-Jacques Akamah
- US-01 : Recherche d'événement dans l'application.
- US-03 : Paiement sécurisé et génération du billet.
- US-04 : Réservation temporaire de siège.
- Participation au Sprint Planning.
- Participation à l'organisation et au suivi des Sprints.

### Andjui Melchisedek Aka
- US-02 : Consulter un événement.
- US-05 : Consultation du plan de salle en temps réel.
- US-06 : Notification d'expiration de réservation.
- Participation à la documentation et au suivi du projet.

### Gladys Emeline Banaken
- US-07 : Tableau de bord des ventes pour l'administrateur.
- Participation à la documentation et aux activités collaboratives du projet.

Les tâches présentées ci-dessus sont suivies dans Jira et leur état
d'avancement est documenté dans le tableau de projet. Les contributions
aux fichiers et à la documentation sont également traçables dans
l'historique GitHub.
