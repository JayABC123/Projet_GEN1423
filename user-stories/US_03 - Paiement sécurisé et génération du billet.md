# US_03 - Paiement sécurisé et génération du billet

## User Story
En tant que client, je souhaite payer mon billet de manière sécurisée et recevoir mon billet électronique avec un code QR après mon paiement, afin de pouvoir accéder à l'événement.

## Critères d'acceptation
- Connexion sécurisée :
    Étant donné que je procède au paiement,
    Quand je transmets mes informations de paiement,
    Alors la transaction s'effectue via une connexion sécurisée (HTTPS/TLS).

- Paiement refusé :
    Étant donné que je soumets un paiement,
    Quand la transaction est refusée par le fournisseur de paiement,
    Alors un message d'erreur clair s'affiche et le siège reste réservé jusqu'à l'expiration du délai.

- Délai de finalisation :
    Étant donné que j'ai initié le paiement,
    Quand je confirme la transaction,
    Alors le paiement est finalisé en moins de 5 minutes.

- Protection contre la double facturation :
    Étant donné qu'un siège est verrouillé pour ma transaction,
    Quand le paiement est en cours,
    Alors le système empêche toute double réservation ou double facturation du même siège.

- Génération automatique du billet :
    Étant donné que mon paiement est confirmé,
    Quand la transaction est finalisée,
    Alors un billet électronique avec un code QR est généré automatiquement.

- Envoi de confirmation par courriel :
    Étant donné que mon billet a été généré,
    Quand la transaction est complétée,
    Alors un courriel de confirmation contenant le billet électronique est envoyé à l'utilisateur.

- Échec d'envoi :
    Étant donné que le système tente d'envoyer le courriel de confirmation,
    Quand le service de messagerie est indisponible,
    Alors le système réessaie l'envoi (retry) et le billet reste accessible depuis le profil du client même si le courriel échoue

## Priorité
Must have

## Story Points
5

## Tâches

- TASK 3.1 - Définir les critères d'acceptation du paiement :
    Les critères d'acceptation du paiement sont définis ci-dessus. Cette tâche consiste à les valider et à s'assurer qu'ils couvrent les différents scénarios du processus de paiement, notamment la réussite, le refus, le délai de finalisation et la protection contre la double facturation.

- TASK 3.2 - Modélisation du flux de paiement :
    Ce diagramme montre les interactions entre les différents composants lors d'un paiement.
    Le diagramme de séquence est disponible dans : `architecture/US03-flux-de-paiement.png`

- TASK 3.2 - Analyse de la sécurité du paiement : 
    La tâche consiste à identifier les principales menaces liées au paiement, notamment l'interception des données, le rejeu de transactions, la fraude et la manipulation des montants. Des mécanismes de mitigation sont définis, tels que TLS 1.3, l'utilisation d'une passerelle de paiement PCI-DSS, l'idempotence des transactions, la validation côté serveur et la journalisation des tentatives de paiement.
    Le fichier contenant l'analyse détaillé est disponible dans : `docs/US_03/US03-sécurité-paiement.md`

- TASK 3.3 - Analyse de la sécurité du paiement : 
    La tâche consiste à identifier les principales menaces liées au paiement, notamment l'interception des données, le rejeu de transactions, la fraude et la manipulation des montants. Des mécanismes de mitigation sont définis, tels que TLS 1.3, l'utilisation d'une passerelle de paiement PCI-DSS, l'idempotence des transactions, la validation côté serveur et la journalisation des tentatives de paiement.
    Le fichier contenant l'analyse détaillé est disponible dans : `docs/US_03/US03-sécurité-paiement.md`

- TASK 3.4 - Processus de génération du billet :
    La tâche consiste à modélser le processus complet de génération du billet électronique (QR Code) déclenché après la confirmation du paiement, et documenter le choix technique retenu (génération synchrone vs asynchrone).
    Le fichier contenant l'analyse de la décision architecturale est disponible dans : `docs/US_03/US03-génération-billet.md`
    Lien vers le diagramme de séquence : `architecture/US_03/US03-flux-génération-billet.png`

- TASK 3.5 - Définir la confirmation par courriel :
    Les critères d'acceptation de la confirmation par courriel sont définis ci-dessus. Cette tâche consiste à l'envoi automatique du courriel de confirmation avec le billet électronique et le code QR, ainsi que le mécanisme de réessai en cas d'indisponibilité du service de messagerie et l'accès permanent au billet depuis le profil client si l'envoi échoue.

- TASK 3.6 - Définir les scénarios d'échec :
    Cette tâche consiste à identifier les principaux scénarios d'échec du paiement et de la génération du billet, ainsi que le comportement attendu du système pour chacun.
    Le fichier contenant les scénarios de d'échec est disponible dans : `docs/US_03/US03-Scénarios-échec.md`

- TASK 3.7 - Définir les scénarios de test : 
    Cette tâche consiste à définir les tests permettant de valider le paiement, la génération du billet et du QR Code, ainsi que les différents cas d'échec     identifiés.
    Le fichier contenant les scénarios de test est disponible dans : `docs/US_03/US03-Scénarios-Test.md`