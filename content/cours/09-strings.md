---
title: "09 - Strings"
prev_class: "08-classes"
next_class: "10-geometrie"
---

## Définition
 Un **string** est un type de données particulier permettant de contenir une chaîne de caractères, du texte. Il ne s'agit pas d'un type primitif comme `int`, `float`, etc. mais d'une [classe](cours/08-classes.md) `String` existante dans le langage Java de base.

Comme toute variable, on déclare un string en indiquant son type, `String`, et le nom de la variable. En Java, une chaîne de caractères est délimitée par des guillemets. Ainsi, toute valeur entre `" "` sera évaluée par processing comme étant du type `String`.

```java
String s = "Hello World!";
println(s); // Affiche Hello World!
```

### Objets et littéraux

Bien que `String` soit une classe, Java permet d'utiliser des littéraux de type `String` : des chaînes de caractères entre guillements `"`. Ces littéraux sont stockés différemment que les objets en mémoire, de façon centrale, de sorte qu'une même chaîne de caractères utilisée plusieurs fois soit un seul littéral en mémoire.

```java
println("abc" == "abc"); // Affiche true
println("abc" == "bcd"); // Affiche false
```

Il est par contre possible de créer explicitement un objet de type `String` via le constructeur en utilisant un littéral en paramètre. Il s'agit alors d'un objet à part entière qui sera stocké dans la mémoire heap, et deux objets `String` qui contiennent la même chaîne de caractères seront différents.

```java
String s1 = "Hello";
String s2 = new String("Hello");
println(s1 == "Hello"); // Affiche true
println(s2 == "Hello"); // Affiche false
```


## Manipulation

### Concaténation

La **concaténation** est une opération qui permet de combiner deux chaînes de caractères via l'opérateur `+`. Les deux chaînes de caractères seront alors mises "bout à bout" pour n'en former qu'une.

```java
String s1 = "Hello ";
String s2 = "World";
String s3 = s1 + s2;
println(s); // Affiche Hello World
```

Comme toute opération simple, on peut l'utiliser plusieurs fois dans une même expression, ce qui permet de construire facilement des chaînes de caractères en combinant des variables de type `String`  et des littéraux.

```java
String s1 = "Hello";
String s2 = "World";
println(s1 + " " + s2 + "!");
```

#### Concaténation avec un autre type

On peut concaténer une chaîne de caractères avec une valeur d'un autre type, cette valeur sera alors convertie automatiquement par processing en une chaîne de caractères correspondant à son contenu.

```java
String s = "Number ";
int i = 5;
println(s + i); // Affiche Number 5
```


### Comparaison

Comme on peut avoir des objets ou des littéraux `String`, et que les comparaisons classiques avec `==` et `!=` ne se comporteront pas forcément de la façon à laquelle on s'attend, comme expliqué plus haut, il est préférable de se servir des méthodes `compareTo` et `equals`.

#### `compareTo`

La méthode `compareTo` disponible sur un `String` permet de comparer la chaîne de caractères de ce `String` avec celle passée en paramètre. La méthode renvoie un nombre entier :
- Positif si le premier `String` est "plus grand" que le second, dans l'ordre croissant
- Négatif si le premier `String` est "plus petit" que le second, dans l'ordre croissant
- 0 si les deux `String` contiennent la même chaîne de caractères.

```java
String abc = "abc";
String bcd = "bcd";
println(abc.compareTo(bcd)); // Affiche -1
println(bcd.compareTo(abc)); // Affiche 1
println(abc.compareTo("abc")); // Affiche 0
```

#### `equals`

La méthode `equals` disponible sur un `String` permet de savoir si ce `String` contient la même chaîne de caractères qu'un autre `String`, utilisé en paramètre. Cette méthode renvoie donc le booléen `true` si les deux `String` contiennent la même chaîne de caractères, ou `false` dans le cas contraire.

```java
String abc = "abc";
String bcd = "bcd";
println(abc.equals(bcd)); // Affiche false
println(abc.equals("abc")); // Affiche true
```

### Fonctions utiles

#### `length`

On peut récupérer la taille d'une chaîne de caractères en appelant la fonction `length` sur cette chaîne de caractères.

```java
String s1 = "Hello";
String s2 = ":D";
println(s1.length()); // Affiche 5
println(s2.length()); // Affiche 2
```

#### `split`

La méthode `split` permet de scinder une chaîne de caractères sur base d'un séparateur, une chaîne de caractères à passer en paramètre. Le `split` renvoie un tableau de `String` correspondant aux différentes parties de la chaîne initiale qui étaient séparées par le séparateur. Par exemple, utiliser `split(" ")` permet de couper une phrase sur les espaces et de récupérer un tableau de mots.

```java
String s = "Hello World!";
String[] parts = s.split(" ");
println(parts.length); // Affiche 2
println(parts[0]); // Affiche Hello
println(parts[1]); // Affiche World!
```

#### `charAt`

La méthode `charAt` permet de récupérer le caractère (type `char`) se trouvant à l'indice passé en paramètre.

```java
String s = "Hello World!";
char h = s.charAt(0);
char d  = s.charAt(10);
println(h); // Affiche H
println(d); // Affiche d
```

#### `substring`

La méthode `substring` permet de récupérer une partie de la chaîne de caractères initiale. On peut appeler cette méthode de deux façons :

- Avec un seul paramètre de type entier, qui est l'indice du caractère à partir duquel on veut la sous-chaîne de caractères, qui ira jusqu'à la fin de la chaîne de caractères initiale
```java
String s = "Hello World!";
String world = s.substring(6);
println(world); // Affiche World!
```
- Avec deux paramètres de type entier ; le premier est toujours l'indice du premier caractère de la sous-chaîne voulue, et le deuxième est l'indice du caractère (non-compris) de fin de la sous-chaîne
```java
String s = "Hello World!";
String hello = s.substring(0, 5);
println(hello); // Affiche Hello
```
