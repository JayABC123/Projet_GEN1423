## TASK-4.3 — Mécanisme de verrouillage temporaire

#### Solution retenue
Utilisation d'un verrou distribué avec expiration automatique (TTL),
implémenté via un système de cache en mémoire (ex. Redis), plutôt qu'un
verrou au niveau de la base de données relationnelle.

#### Justification
- Redis permet des opérations atomiques (SETNX / SET avec option NX et
  EX) garantissant qu'un seul client peut acquérir le verrou sur un
  siège donné, même en cas de requêtes simultanées.
- L'expiration automatique (TTL de 300 secondes) évite d'avoir à gérer
  manuellement l'annulation en cas d'abandon du client (fermeture de
  page, perte de connexion).
- Les performances en lecture/écriture de Redis (opérations en mémoire)
  sont largement supérieures à un verrou transactionnel en base de
  données relationnelle, ce qui est critique lors des pics de charge
  (jusqu'à 50 000 requêtes/s selon le profil de charge du sujet).

#### Alternative rejetée
Un verrou pessimiste directement en base de données (ex. `SELECT ... FOR
UPDATE`) a été écarté : il introduirait une contention élevée sur la
base de données principale lors des ventes flash, avec un risque de
ralentissement généralisé du système.