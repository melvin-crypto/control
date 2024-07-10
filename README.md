# controle-continu-1

## 1. Matières (5 points)

Chaque ligne doit correspondre à une matière. Le nom de la matière doit être la première colonne de chaque ligne du tableau.

```text
Vue.js & TypeScript     | ... | ... | ...
Docker & Docker Compose | ... | ... | ...
TypeScript & Nest.js    | ... | ... | ...
```

L'en-tête du tableau doit correspondre au format suivant.

```text
Matière             | Contrôle Continu #1 | Contrôle Continu #2
--------------------+---------------------+--------------------
Vue.js & TypeScript | 13                  | 14
```

Les matières ne contiennent pas toujours le même nombre de notes. Afficher quand même une colonne vide lorsque c'est approprié.

```text
Matière              | Contrôle Continu #1 | Contrôle Continu #2 | Contrôle Continu #3
---------------------+---------------------+---------------------+--------------------
Vue.js & TypeScript  | 13                  | 14                  |
Docker               | 15                  | 16                  | 17
TypeScript & Nest.js | 18                  | 17                  | 11
```

## 2. Moyennes (5 points)

Afficher la moyenne pour chaque matière, arrondi à 2 chiffres maximum après la virgule.

```text
Matière              | Contrôle Continu #1 | Contrôle Continu #2 | Contrôle Continu #3 | Moyenne
---------------------+---------------------+---------------------+---------------------+--------
Vue.js & TypeScript  | 13                  | 14                  |                     | 12.5
Docker               | 15                  | 16                  | 17                  | 16
TypeScript & Nest.js | 18                  | 17                  | 11                  | 15.33
```

Faire de même pour la moyenne générale.

```text
Matière              | Contrôle Continu #1 | Contrôle Continu #2 | Contrôle Continu #3 | Moyenne
---------------------+---------------------+---------------------+---------------------+--------
Vue.js & TypeScript  | 13                  | 14                  |                     | 12.5
Docker               | 15                  | 16                  | 17                  | 16
TypeScript & Nest.js | 18                  | 17                  | 11                  | 15.33
                                                                 | Moyenne             | 14.61
```

## 3. Analyse visuelle des données (5 points)

Afficher les notes qui sont en dessous de 10 en couleur orange.

Afficher les moyenne qui sont en dessous de 10 en couleur rouge.

Afficher un texte d'aide en fonction de la moyenne générale :
- Si la moyenne est entre 0 et 4, afficher le texte suivant : Des efforts à fournir afin de pouvoir valider l'année.
- Si la moyenne est entre 5 et 9, afficher le texte suivant : Il y a des progrès, mais il reste encore du travail pour atteindre la moyenne.
- Si la moyenne est entre 10 et 14, afficher le texte suivant : Bon travail, mais il est possible d'améliorer encore davantage.
- Si la moyenne est entre 15 et 20, afficher le texte suivant : Excellent travail, continuez ainsi !

## 4. Dynamisme (5 points)

Permettre de supprimer une ligne complètement du tableau visuellement à l'aide d'un bouton de suppression.

```text
Matière              | Contrôle Continu #1 | Contrôle Continu #2 | Contrôle Continu #3 | Moyenne | Actions
---------------------+---------------------+---------------------+---------------------+---------+------------
Vue.js & TypeScript  | 13                  | 14                  |                     | 12.5    | [SUPPRIMER]
Docker               | 15                  | 16                  | 17                  | 16      | [SUPPRIMER]
TypeScript & Nest.js | 18                  | 17                  | 11                  | 15.33   | [SUPPRIMER]
                                                                 | Moyenne             | 14.61
```

Permettre l'ajout de nouvelle notes. Cela doit se faire via un formulaire plus au dessus du tableau.

Le formulaire doit contenir au minimum un champ de texte permettant d'ajouter une nouvelle matière avec des notes à vides.

Pour pouvoir ajouter une note, un bouton doit permettre l'ajout d'un nouveau champ de texte de type nombre avec la note à saisir. Il est possible d'ajouter autant de note que nécessaire.

Un bouton final doit permettre d'ajouter la nouvelle matière ainsi que ses notes au tableau.

Tout le tableau des matières, les moyennes, ainsi que la moyenne générale doit être vérifiée de nouveau lors de cet ajout et doit donc être dynamique.

Il n'y a pas de modification possible pour les notes déjà existantes.
