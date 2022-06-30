---
title: "05 - Boucles"
prev_class: "04-alternatives"
next_class: "06-fonctions"
---

## Définition

Une boucle est un *bloc de code* dont l'exécution est **optionnelle** et **répétée** tant que la **condition**, **une [expression](cours/02-expressions.md) booléenne**, est respectée. 

La logique est similaire à celle d'un [branchement conditionnel simple](/cours/04-alternatives.md#branchementsimple), à la différence que dans un branchement conditionnel, on passe à la suite du code lorsqu'on finit l'exécution du bloc optionnel. Dans le cas d'une boucle, après une exécution du bloc optionnel, on revient à la condition qui est alors réévaluée pour éventuellement recommencer l'exécution du bloc de code.

## Boucle `while`

La boucle de base est définie par l'utilisation du mot clé `while` suivi de la condition entre parenthèses et du bloc de code optionnel entre accolades `{}`. La structure est la même que pour le branchement simple `if`.

```java
int i = 0;

while (i < 5) {
  println(i);
  i += 1;
}
```

Le code ci-dessus affichera donc successivement, dans la console :

```bash
0
1
2
3
4
```

Pour qu'une boucle ait du sens, il faut que le code optionnel manipule et change la ou les variables impliquées dans la condition de cette boucle, sans quoi on pourrait créer des boucles "infinies" pour lesquells la condition est toujours vraie car indépendante du code de la boucle.

```java
int i = 0;

while (i < 5) { // i ne change pas et on ne sort jamais de la boucle
  println(i);
}
```


## Boucle `for`

 On utilise régulièrement des boucles pour répéter un certain nombre de fois un même bloc de code, et la condition de cette boucle ne représente donc que le nombre d'itérations voulues. Dans ce cas, il est parfois plus simple d'utiliser une autre boucle, la boucle `for`. Cette boucle se compose de trois parties :
 - L'initialisation d'une variable "compteur". Cette variable peut avoir déjà été déclarée dans le code, ou il peut s'agir d'une nouvelle variable déclarée uniquement dans le contexte de cette boucle
 - Une condition pour continuer à boucler. On veut en général que la variable compteur soit plus petite qu'une *borne* (le nombre de répétitions souhaitées).
 - Une itération, une assignation qui modifie la valeur de la variable compteur pour passer à l'étape suivante.

La boucle est donc de la forme *for (\<initialisation\>; \<condition\>; \<assignation\>) {  }*

```java
// Avec while
int i = 0;
while (i < 5) {
   println(i);
   i++;
}

// La boucle for équivalente
for (int j = 0; j < 5; j++) {
  println(j);
}
```

## Boucles imbriquées

De la même façon qu'on peut mettre des branchements conditionnels `if` dans d'autres branchements, et avoir donc des `if` imbriqués, on peut tout à fait mettre des boucles dans des boucles, des boucles dans des branchements conditionnels, des branchements conditionnels dans des boucles, etc.

```java
int i = 0;
while (i < 3) {
  println(i);
  int j = 0;
  while (j < 3) {
    println(j);
    j++;
  }
  i++;
}
```

Le code ci-dessus affichera donc successivement, dans la console :

```plain
0
0
1
2
1
0
1
2
2
0
1
2
```

## Parcourir des tableaux
Les boucles sont particulièrement utiles lorsque l'on manipule des [tableaux](cours/03-tableaux-matrices). On peut utiliser une boucle pour parcourir tous les éléments du tableau et exécuter un bloc de code similaire pour chaque élément. Le plus simple est alors d'utiliser une boucle `for` qui itère sur chaque position dans le tableau, donc de `0`  à la taille du tableau - 1. Pour rappel, on peut obtenir la taille d'un tableau grâce au champ `length` de ce tableau.

```java
int[] t = new int[] { 1, 2, 3, 4, 5 };

for (int i = 0; i < t.length; i++) {
   println(t[i]);
}
```

Le code ci-dessus parcoure ainsi tous les éléments du tableau et affiche leur valeur dans la console.

En définissant la borne supérieur comme étant la taille `length` du tableau, et non une valeur fixe (dans ce cas-ci on aurait pu mettre 5), le code fonctionnera peu importe la taille effective du tableau que l'on a créé avant la boucle, puisque la vraie taille sera toujours utilisée.

## Parcourir des matrices

Grâce aux boucles imbriquées, il est très facile de parcourir une matrice, un tableau de tableaux. On peut en effet itérer sur les lignes dans une boucle, et sur chaque colonne de cette ligne dans une boucle imbriquée, ou inversément (les colonnes puis les lignes par colonne).

Comme pour un tableau à une dimension, il est plus facile d'utiliser des boucles `for` que des boucles `while`. On choisit en général comme nom de variable compteur `i` pour la première dimension, les lignes, et `j` pour la deuxième, les colonnes. Ces noms sont tout à fait arbitraires et pourraient être changés, mais garder une certaine cohérence de nommage, comme utiliser le même nom pour les variables représentant des indices de ligne et pour celles représentant des indices de colonne, permet de naviguer plus aisément dans son propre code.

```java
int[][] m = new int[][] { 
  { 1, 2, 3 }, 
  { 4, 5, 6 }, 
  { 7, 8, 9 } 
};

int nbLines = m.length;
for (int i = 0; i < nbLines; i++) {
  // i va prendre successivement la position de chaque ligne
  // On récupère le nombre de colonnes dans la ligne i
  int nbColumns = m[i].length;
  for (int j = 0; j < nbColumns; j++) {
  // On affiche la coordonnée (i,j) et la valeur de l'élément correspondant
    println(i, j, m[i][j]);
  }
}
```

Ce code affiche les coordonnées (ligne, colonne) de chaque élément de la matrice et la valeur de cet élément, en commençant par la première ligne et toutes ses colonnes, la deuxième ligne, etc. On verra donc, dans la console :

```plain
0 0 1
0 1 2
0 2 3
1 0 4
1 1 5
1 2 6
2 0 7
2 1 8
2 2 9
```