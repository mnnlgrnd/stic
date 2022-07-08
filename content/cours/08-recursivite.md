---
title: "08 - Récursivité"
prev_class: "07-blocs-contextes"
next_class: "09-classes"
---

## Définition

On dit de quelque chose qu'elle est *récursive* dès lors qu'elle s'utilise elle-même.

Un exemple de récursivité assez connu est la mise en abîme, où on inclut dans une oeuvre l'oeuvre elle-même :

![[cours/images/recursion.jpeg]]

## Fonction récursive

Une fonction est récursive si, dans le code de cette fonction, on retrouve un (ou plusieurs) appels à cette même fonction. Il s'agit alors de récursivité directe.

```java
void foo() {
  if (random(0, 1) > 0.5) {
    println("Recursive call");
    foo();
  }
}
```

Il est également possible de faire de la récursivité en appelant indirectement une autre fonction qui elle-même, lors de son exécution, appelle la fonction de départ.

```java
void foo() {
  if (random(0, 1) > 0.5) {
    println("Recursive call");
    bar();
  }
}

void bar() {
   foo();
}
```


## Conditions d'arrêt

Quand on définit une fonction récursive, il est impératif que cet appel récursif soit *conditionnel*. En effet, si l'appel récursif était toujours exécuté lors d'un appel à la fonction, on ne sortirait plus jamais du cycle d'appels. On parle alors de *conditions d'arrêt*, qui sont les situations dans lesquelles il ne faut pas/plus faire d'appel récursif. 

Cela peut se traduire concrètement par 
- Un branchement conditionnel dans lequel on fait l'appel récursif ; la condition d'arrêt est alors l'inverse de la condition de ce branchement
- Un branchement conditionnel situé *avant* l'appel récursif dans lequel on fait un `return`

Les conditions d'arrêt portent en général sur les paramètres de la fonction récursive, et chaque appel récursif doit inclure un changement dans la valeur de ces paramètres, de sorte que les conditions d'arrêt puissent avoir un résultat différent selon le [contexte](cours/07-blocs-contextes.md) de l'appel.

```java
void foo() {
  foo(); // Appel inconditionnel, foo() s'appelle sans cesse
}

void bar(int i) {
  if (i > 0) {
    bar(i - 1); // Appel conditionnel avec évolution des paramètres
  }
}
```

Il pourrait aussi s'agir de variables globales, le principal étant que le *contexte* de chaque appel soit différent. S'il était similaire (les variables visibles par le contexte ont la même valeur) et que les conditions portent sur ces variables, on serait dans une situation de récursivité infinie, ce que l'ordinateur ne peut bien entendu pas gérer. Lorsque l'on crée une telle situation, souvent par erreur, le programme renverra une erreur du type `StackOverflowError`.

## Stack d'appels

Comme vu précédemment, un appel de fonction s'exécute dans son propre contexte ; il en va de même pour les appels récursifs. Un appel récursif induit un nouveau contexte "par-dessus", masquant l'existant, celui de l'appel récursif précédant. Lorsque l'on arrive au bout de l'exécution du code d'un appel récursif, on revient au contexte précédent, ainsi de suite, jusqu'à sortir complètement de ce "stack", cet empilement d'appels récursifs et leur contexte. 

Considérons la fonction récursive suivante

```java
void foo(int i) {
  println(i);
  if (i < 3) {
    foo(i + 1);
  }
}
```

Si on appelle initialement la fonction en passant 0 en paramètre : `foo(0)`, l'exécution ressemblera à

<p align="center">
<img src="/stic/images/recursion-dm.svg" class="svg-dark-mode w-50"/>
<img src="/stic/images/recursion-lm.svg" class="svg-light-mode w-50"/>
</p>

Et affichera en console

```plain
0
1
2
3
```

## Construire une solution récursive

Si on construit une solution récursive pour un certain problème, cela signifie qu'il faut parvenir, dans le code de la fonction, à résoudre une *petite* partie de ce problème de sorte qu'il reste un problème similaire mais plus petit, que l'on résoudra via l'appel récursif. Il convient donc d'arriver à définir le problème comme étant un ensemble de sous-problèmes similaires.

Prenons par exemple un problème qui consiste à suivre une série de directions. La fonction récursive va extraire une partie du problème, la première direction à suivre, et la résoudre ; on suit la direction indiquée. Il reste maintenant toutes les autres directions à suivre, mais on peut, pour ce faire, appeler récursivement la fonction. La condition d'arrêt sera ici lorsqu'il n'y a plus de directions à suivre.

```java
void followDirections(int[] directions) { 
  if (directions.length > 0) { 
    int firstDirection = directions[0]; 
    followDirection(firstDirection); 

    int[] remainingDirections = removeFirstElement(directions);
    followDirections(remainingDirections);
  }
} 

void followDirection(int direction) { 
  // TODO 
  println(direction);
} 

int[] removeFirstElement(int[] array) { 
  if (array.length > 0) { 
    int[] newArray = new int[array.length - 1]; 
    for (int i = 1; i < array.length; i++) { 
      newArray[i - 1] = array[i];
    } 
    return newArray;
  } else { 
    return new int[] {};
  }
}
```