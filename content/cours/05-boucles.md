---
title: "05 - Boucles"
prev_class: "04-alternatives"
next_class: "06-fonctions"
---

## Définition

Une boucle est un *bloc de code* dont l'exécution est **optionnelle** et **répétée** tant que la **condition**, **une [expression](cours/02-expressions.md) booléenne**, est respectée. 

La logique est similaire à celle d'un [branchement conditionnel simple]({{< relref "cours/04-alternatives.md#branchement-simple" >}}), à la différence que dans un branchement conditionnel, on passe à la suite du code lorsqu'on finit l'exécution du bloc optionnel. Dans le cas d'une boucle, après une exécution du bloc optionnel, on revient à la condition qui est alors réévaluée pour éventuellement recommencer l'exécution du bloc de code.

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

```console
0
1
2
3
4
```

## Boucle `for`