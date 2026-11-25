# REPONSES.md — Partie 0 : Mise en place

## Q0.1 — Pourquoi interdit-on de pousser directement sur `main` ? Donnez deux raisons, dont une qui concerne le travail en binôme.

On interdit les pushes directs sur `main` pour protéger la branche principale et éviter d’y intégrer des changements non vérifiés ou qui pourraient casser le projet. Le passage par une Pull Request permet de relire les modifications et de vérifier qu’elles fonctionnent avant de les fusionner.

En binôme, la Pull Request permet à l’autre étudiant de consulter les changements, de les comprendre, de donner son avis et de repérer d’éventuelles erreurs. Cela facilite la collaboration et évite que chacun modifie la branche principale sans contrôle.

## Q0.2 — La collection Bruno est faite de fichiers texte rangés dans le dépôt. Qu'est-ce que cela change pour la relecture d'une Pull Request ?

Comme les requêtes et les tests Bruno sont stockés sous forme de fichiers texte dans le dépôt, ils apparaissent directement dans la Pull Request. Le binôme peut donc relire précisément les URL, les méthodes HTTP, les paramètres, les corps des requêtes et les assertions des tests, voir les différences avec la version précédente et commenter les changements.

La collection est ainsi versionnée avec le code, ce qui rend les tests plus faciles à partager, à relire et à reproduire sur les deux machines.

Q1.1.2 — Résultats observés

Après avoir arrêté catalog-service, j'ai envoyé cinq fois une requête de création de commande depuis Bruno. Les cinq requêtes ont retourné le code HTTP 503 (Service Unavailable).

La première requête a pris 4,62 secondes, tandis que les suivantes ont répondu entre 100 et 201 ms. Cela montre que order-service tente de contacter catalog-service, mais que l'appel échoue puisque le catalogue est indisponible.

### Q1.1 — Catalogue lent

Avec un `readTimeout` de 2 secondes, chaque commande attend au maximum 2 secondes la réponse du catalogue. Si le catalogue est très lent, la requête échoue après ce délai.

Si 200 clients passent des commandes en même temps, les requêtes peuvent toutes attendre ces 2 secondes. Cela mobilise les ressources de `order-service` et peut le surcharger, ralentir les autres requêtes ou provoquer une saturation. Le problème du catalogue peut donc se propager au service de commandes.

### Q1.2 — Image du disjoncteur électrique

Le Circuit Breaker fonctionne comme un disjoncteur électrique : il protège `order-service` en coupant les appels vers `catalog-service` lorsque trop d'erreurs sont détectées. Il évite ainsi de continuer à solliciter un service indisponible et de surcharger les ressources.

Après une période d'attente, le disjoncteur passe en mode semi-ouvert (HALF-OPEN) et autorise quelques appels de test. Si ces appels réussissent, il se referme (CLOSED) et les appels normaux reprennent. Si les tests échouent, il s'ouvre à nouveau (OPEN) et bloque les appels.