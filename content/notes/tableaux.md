---
title: "02 - Tableaux"
---

## Définition

Un **tableau** est une collection ordonnée de variables du même type. On accède a une variable du tableau grâce au nom du tableau et à la position de la variable dans celui-ci.

## Déclaration

On déclare un tableau comme on déclare une [variable](notes/variables#déclaration), à ceci près qu'il faut rajouter l'opérateur `[]` pour indiquer qu'il s'agit d'un tableau. On peut ajouter cet opérateur soit après le **type** de données du tableau, soit après son nom. Il s'agit de déclarations équivalentes.

```java
int[] integers;
```

ou

```java
int integers[];
```

On déclare ici une variable appelée `integers` qui est un tableau de nombres entiers.

## Création

Il existe deux façons de créer un tableau :

- On peut créer un tableau vide en indiquant sa taille, le nombre d'éléments qu'il contient :

```java
int[] integers = new int[6];
```

- On peut créer un tableau en indiquant directement les valeurs qu'il contient :

```java
int[] integers = new int[] { 1, 2, 4, 8, 16, 32 };
```

Dans les deux cas, l'utilisation du mot clé `new` est obligatoire. Ce mot clé indique qu'on crée une nouvelle **référence** et est responsable de l'allocation en mémoire.

>:warning: La taille d'un tableau est fixe et ne peut pas être modifiée après sa création. Si on voulait par exemple ajouter un nouvel élément au tableau, il faudrait en réalité créer un nouveau tableau de plus grande taille.

### Stockage en mémoire

Lorsqu'un programme processing s'exécute, il possède sa propre mémoire dans laquelle seront stockées toutes les variables et tout ce qu'il se déroule dans le programme (appels de fonction, etc.). Cette mémoire se compose de deux parties :

- La mémoire dite statique, le *stack*, qui contient notamment les variables (locales) de type primitif et des **références** vers des données stockées dans le *heap*
- La mémoire dite dynamique, le *heap*, qui contient notamment des tableaux et des objets

<img src="./images/stack_heap.svg"/>

> :warning: Le stockage en mémoire est en réalité plus complexe, l'important ici est de comprendre la différence entre une valeur et une référence. Pour plus de détails sur la gestion de la mémoire lors de l'exécution d'un programme Java, Google est votre ami.

## Manipulation

Une fois un tableau déclaré et créé, on peut accéder à sa taille et aux différents éléments qu'il contient.

### Taille du tableau

La taille d'un tableau est déterminée à sa création et ne peut pas être changée, on peut la récupérer grâce au champ spécial `length` du tableau, de la façon suivante :

```java
int[] integers = new int[] { 1, 2, 3 };
println(integers.length); // Affiche 3
```

### Elements du tableau

Pour accéder à un élément particulier du tableau, il faut utiliser l'opérateur de tableau et l'indice de l'élément après le nom du tableau, par exemple `[1]`.

> :warning: En informatique, on commence à compter à partir de 0. Le premier élément aura donc l'indice 0, le deuxième l'indice 1, ainsi de suite.

Lorsque l'on accède à un élément du tableau, on récupère une variable (celle stockée dans le heap), et on peut donc s'en servir comme tel ; c'est-à-dire lui assigner une valeur, ou l'évaluer dans des expressions.

```java
int[] integers = new int[] { 1, 2, 3 };
println(integers[0]); // Evalue la variable à l'indice 0 dans le tableau et affiche 1
integers[1] = 0; // Assigne la valeur 0 à la variable à l'indice 1 dans le tableau
println(integers[0]); // Evalue la variable à l'indice 1 dans le tableau et affiche 0
println(integers[2]); // Evalue la variable à l'indice 2 dans le tableau et affiche 3
```
