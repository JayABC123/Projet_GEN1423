# Volet 3 - Validation de la qualité

## Livrable du volet 3

### Le plan de tests, et scénarios d’acceptation

- Cette section présente la stratégie de tests de TicketPulse ainsi que 
les scénarios représentatifs validant les critères d'acceptation de 
chaque User Story, couvrant les tests fonctionnels, non fonctionnels et 
d'échec.

- Le fichier du plan de test est disponible dans : `docs/plan-tests.md`

### Le plan de validation de la performance

- Ce document identifie les principaux indicateurs de performance du 
système et propose une démarche de vérification (tests de charge, 
monitoring) permettant de confirmer que les objectifs de performance 
sont atteints.

- Le fichier du plan de validation est disponible dans : `Livrables/Volet 3/Plan de validation de la performance.md`

### Les scénarios de charge et les seuils proposés 

- Cette section détaille les scénarios de charge simulant les pics de 
trafic définis dans le profil de charge du sujet, ainsi que les seuils 
de performance et de disponibilité à respecter.
- Le fichier pour les scénarios de charge est disponible dans leur dossier respectif dans : `docs/US_0X/US_0X-Estimation-X.md`

### L’analyse des menaces et des contrôles de sécurité

- Ce document identifie les principales menaces applicables à TicketPulse 
(ex. interception de paiement, fraude, accès concurrents) et présente 
les mécanismes retenus pour réduire ces risques.

- Le fichier pour l'analyse des menaces est disponible dans : `docs/analyse-securite.md`

### Les scénarios de panne et le plan de reprise

- Cette section présente les scénarios de défaillance envisagés (ex. 
panne du service de verrouillage, indisponibilité de la passerelle de 
paiement) ainsi que la stratégie de reprise après incident associée.

- Le fichier pour les scénarios de panne est disponible dans : `docs/resilience.md`

### Le plan de maintenance et la feuille de route d’évolution

- Ce document présente la stratégie de maintenance du système ainsi que 
les axes d'évolution futurs permettant de faire croître TicketPulse 
tout en limitant les interruptions de service.

- Le fichier du plan de maintenance est disponible dans : `docs/maintenance-evolution.md`