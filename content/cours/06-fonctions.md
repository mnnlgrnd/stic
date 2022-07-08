---
title: "06 - Fonctions"
prev_class: "05-boucles"
next_class: "07-blocs-contextes"
---

## Définition

Une fonction permet de définir un bloc de code **réutilisable** que l'on pourra **appeler** à n'importe quel moment dans le code.

### Signature

Pour pouvoir appeler une fonction, il faut la déclarer en spécifiant :
- Son **type** de retour (`int`, `float`, etc.) ou `void` si elle ne renvoie rien
- Son **nom** ; à utiliser pour appeler la fonction
- Ses **paramètres** ; leur type et leur nom

Le code de cette fonction est à mettre entre accolades `{}` en respectant la syntaxe 

*\<type\> \<nom\>(\<type_p_1\> \<nom_p_1\>, ..., \<type_p_n\> \<nom_p_n\>) { 
   // code
}*

Une fonction peut ne pas avoir de paramètres si on ne met rien dans les parenthèses, mais elles restent obligatoires.

Le type de retour, le nom et le type des paramètres constituent ce qu'on appelle la **signature** d'une fonction. On ne peut pas créer deux fonctions ayant la même signature, le code affichera alors l'erreur `Duplicate method <signature>`.

>ℹ L'ordre dans lequel les fonctions sont définies n'a pas d'importance.

## Appel et exécution

Un **appel** à une fonction consiste à utiliser le nom de la fonction suivi de parenthèses avec, éventuellement, les *valeurs* à passer aux paramètres de cette fonction. 

Il faut obligatoirement appeler la fonction en respectant sa signature ; les valeurs passées doivent correspondre en nombre et en type aux paramètres définis dans la signature de la fonction qu'on appelle. Sinon, le code affichera une erreur du type `The function "<name>" expects parameters like: <signature>`.

Lorsque le programme arrive sur l'appel à la fonction, il exécutera le bloc de code de cette fonction dans un [contexte](cours/07-blocs-contextes) différent dans lequel ne seront disponibles que les variables globales et les paramètres de la fonction.

```java
void foo() {
  println("foo");
}

int bar(int i) {
  return i * 2;
}

void setup() {
  foo(); // Appelle la fonction foo, qui va afficher foo 
  println(bar(1)); // Affiche le résultat de l'appel à bar(1) : 2
}
```

Lorsque l'exécution du code est terminée, la ligne de code suivant celle de l'appel est la prochaine qui sera exécutée.

> ⚠ Pour qu'un code avec des fonctions et appels de fonction soit exécutable en processing, il est obligatoire de mettre les appels de fonction dans une des fonctions de processing (setup, draw, etc.) et pas dans le contexte global.

## Retour de fonction

### Fonctions avec retour

Une fonction qui *retourne* ou *renvoie* une valeur doit avoir défini son type de retour, c'est-à-dire le type de la valeur qu'elle renvoie. Pour qu'une fonction retourne effectivement une valeur, il faut utiliser le mot clé `return` suivi d'une [expression](cours/02-expressions.md), dans la fonction. 

Cette expression sera renvoyée par l'appel à la fonction, et on pourra utiliser des appels à cette fonction dans d'autres expressions.

```java
int foo() {
  return 1;
}

void setup() {
  int i = foo() + 1;
  println(i); // Affiche 2
}
```

Dans le code ci-dessus, on appelle la fonction `foo` qui renvoie une valeur de type `int`. On utilise un appel à cette fonction dans l'expression utilisée pour l'assignation à la variable `i` :

- L'appel à foo est évalué : le code est exécuté et la valeur renvoyée est 1 ; 
- On effectue ensuite la somme de cette valeur et de 1, qui vaut 2, et on assigne ce résultat à la variable `i` qui va donc contenir 2.

Si la fonction contient des branchements conditionnels, il est **obligatoire** que, peu importe la branche exécutée, on atteigne un `return`. En effet, il faut que la fonction renvoie **toujours** une valeur. Dans le cas contraire, le code affichera une erreur du type `This method must return a result of type x`.

Dès que l'on arrive sur une ligne de code `return` lors de l'exécution d'un appel de fonction, l'exécution prend fin ; l'appel à la fonction se termine sur cette valeur retournée et on revient à la ligne de code ayant fait l'appel pour utiliser cette valeur.

### Fonctions `void`

Une fonction définie avec `void` comme "type" de retour est en réalité une fonction qui ne va rien retourner. Les appels à cette fonction ne peuvent donc pas être utilisés dans des expressions car ils ne peuvent pas être évalués. Les appels ne peuvent se faire que comme ligne exécutable simple :

```java
void foo() {
  println("foo");
}

void setup() {
  foo();
}
```

Il est possible d'utiliser le mot clé `return` dans une fonction `void` sans mettre de valeur après ; l'effet du `return` est alors simplement la fin de l'exécution de l'appel.

## Paramètres
### Utilisation
Les paramètres, ou arguments, d'une fonction, sont des variables utilisables dans le code de la fonction et pour lesquelles il faudra passer *une valeur* à chaque fois qu'on appelle la fonction. Le nom des paramètres est arbitraire mais une fonction est plus compréhensible lorsque ses paramètres sont nommés intelligemment.

```java
int square(int i) {
  return i * i;
}

void setup() {
  println(square(0)); // Affiche 0
  println(square(1)); // Affiche 1
  println(square(2)); // Affiche 4
  println(square(3)); // Affiche 9
}
```

On définit une fonction `square` qui va nous permettre de calculer le carré d'un nombre. Ce nombre, *n'importe lequel*, on le représente par le paramètre `i`, de type entier. La fonction calcule ensuite le carré de cette variable, `i * i` et renvoie cette valeur. 

Nous n'avons besoin de valeurs pour ce paramètre que lorsque l'on appelle effectivement la fonction, comme on le fait plus loin : `println(square(2))` par exemple, affiche en console le résultat de l'appel à la fonction `square` où le paramètre `i` vaut 2. L'appel renverra donc le carré de 2 : 4.

### Passage par valeur
Les variables de type primitif envoyées en paramètres à une fonction sont *passées par valeur*. Concrètement, cela signifie que la fonction reçoit une *nouvelle* variable, locale à son propre [contexte](cours/07-blocs-contextes.md), qui contient la valeur passée en paramètre. Si on modifie cette variable, la variable potentiellement utilsée pour réaliser ce passage par valeur ne sera pas impactée.

```java
void setup() {
  int i = 0;
  println(i); // Affiche 0
  foo(i);
  println(i); // Affiche 0
}

void foo(int i) {
  i = 5;
}
```

## Utilités
Une fonction permet de ne définir qu'une seule fois un bout de code qui pourrait apparaître plusieurs fois : c'est ce qu'on appelle la *factorisation*. 

Avant factorisation :

```java
void setup() {
  float a = random(0, 1);
  if (a <= 0.25) {
    a = 0;
  } else if (a <= 0.75) {
    a = 0.5;
  } else {
    a = 1;
  }
  println(a);
  
  float b = random(0, 1);
  if (b <= 0.25) {
    b = 0;
  } else if (b <= 0.75) {
    b = 0.5;
  } else {
    b = 1;
  }
  println(b);
}
```

Après factorisation :

```java
void setup() {
  float a = roundToClosestHalf(random(0, 1));
  println(a);

  float b = roundToClosestHalf(random(0, 1));
  println(b);
}

float roundToClosestHalf(float n) {
  if (n <= 0.25) {
    n = 0;
  } else if (n <= 0.75) {
    n = 0.5;
  } else {
    n = 1;
  }
  return n;
}
```

L'utilisation de fonctions permet également d'améliorer la structure d'un programme, en définissant des fonctions aux responsabilités bien limitées et dont les noms, savamment choisis, peuvent améliorer la lisibilité du code. Comme on le voit plus haut, le nom donné à la fonction permet de comprendre facilement ce que le code fait.