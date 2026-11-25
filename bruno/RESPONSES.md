# REPONSES.md — Partie 0 : Mise en place

## Q0.1 — Pourquoi interdit-on de pousser directement sur `main` ? Donnez deux raisons, dont une qui concerne le travail en binôme.

On interdit les pushes directs sur `main` pour protéger la branche principale et éviter d’y intégrer des changements non vérifiés ou qui pourraient casser le projet. Le passage par une Pull Request permet de relire les modifications et de vérifier qu’elles fonctionnent avant de les fusionner.

En binôme, la Pull Request permet à l’autre étudiant de consulter les changements, de les comprendre, de donner son avis et de repérer d’éventuelles erreurs. Cela facilite la collaboration et évite que chacun modifie la branche principale sans contrôle.

## Q0.2 — La collection Bruno est faite de fichiers texte rangés dans le dépôt. Qu'est-ce que cela change pour la relecture d'une Pull Request ?

Comme les requêtes et les tests Bruno sont stockés sous forme de fichiers texte dans le dépôt, ils apparaissent directement dans la Pull Request. Le binôme peut donc relire précisément les URL, les méthodes HTTP, les paramètres, les corps des requêtes et les assertions des tests, voir les différences avec la version précédente et commenter les changements.

La collection est ainsi versionnée avec le code, ce qui rend les tests plus faciles à partager, à relire et à reproduire sur les deux machines.