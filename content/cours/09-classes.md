---
title: "09 - Classes"
prev_class: "08-recursivite"
next_class: "10-strings"
---

## Définition

Dans un langage *orienté objet* comme Java, on peut définir des *classes*. Une classe est un *prototype*, une maquette, représentant un concept souvent tiré du monde réel, et qui nous va permettre de plus facilement interagir avec ce concept.

Un *objet* est une instance d'une classe, un cas concret correspondant au prototype défini.

Imaginons par exemple une classe `Human`, chaque personne serait alors une instance de cette classe, une *réalisation* de ce qui définit un humain.

## Structure

### Syntaxe

Pour définir une classe, il faut utiliser le mot clé `class` suivi du nom de la classe. C'est ce nom qui servira de *type* (au même titre que `int`, `float`, etc.) lorsque l'on déclarera une variable contenant une instance de cette classe. 

Il faut ensuite mettre tout ce qui constitue la classe entre accolades.

> ℹ En Java, on nomme habituellement une classe en commençant par une lettre majuscule, ce qui permet de la distinguer de simples variables, qui devraient commencer par une lettre minuscule.

```java
class Human {

  // Définition de la classe

}
```

Une classe est généralement découpée en trois parties : les attributs, le constructeur et les méthodes.

### Attributs
Les *attributs* d'une classe sont des variables que l'on déclare dans cette classe et qui représentent des informations qu'auront toujours des instances de la classe. La valeur de ces variables changera bien entendu d'une instance à l'autre.

Pour notre classe `Human`, on aura par exemple un attribut `hungry` de type booléen, qui indique si une personne a faim.

```java
class Human {

  // Attributs
  boolean hungry;

}
```

### Constructeur
Le *constructeur* est une sorte de fonction particulière qui permet d'instancier un nouvel objet de la classe. Cette "fonction" doit impérativement porter le même nom que la classe, et il ne faut pas définir un type de retour. On peut se dire que c'est parce que la valeur retournée par le constructeur sera toujours du type de la classe.

Le constructeur d'une classe est donc responsable de l'initialisation d'un objet de cette classe, et c'est là qu'on initialise les différents attributs, soit avec une valeur fixe, soit avec une valeur passée en paramètre.

> ℹ On peut aussi initialiser les attributs quand on les déclare, comme pour des variables classiques

Il est possible de définir plusieurs constructeurs tant que chaque constructeur a des paramètres différents ; on définit alors plusieurs façons différentes de créer un nouvel objet.

```java
class Human {

  // Attributs
  boolean hungry;

  // Constructeur par défaut
  Human() {
    hungry = false;
  }

  // Constructeur avec paramètre
  Human(boolean tempHungry) {
    hungry = tempHungry;
  }

}
```

> ℹ Si on ne définit pas explicitement de constructeur, c'est comme si on avait défini un constructeur sans paramètre qui ne fait rien.

### Instance `this`
Les constructeurs paramétrés utilisent en général des paramètres correspondant aux différents attributs, et on aurait tendance à vouloir les nommer de la même façon que les attributs pour savoir facilement à quoi ils correspondent. En ce faisant, on perd cependant la visibilité sur l'attribut du même nom :

```java
class Human {

  // Attributs
  boolean hungry;

  // Constructeur par défaut
  Human() {
    hungry = false;
  }

  // Constructeur avec paramètre
  Human(boolean hungry) {
    // Le nom hungry visible est celui du paramètre !!
    hungry = hungry; // Ne fait rien
  }

}
```

Pour accéder explicitement à un attribut de la classe, on peut utiliser le mot clé `this`. Ce mot clé représente en quelque sorte l'instance de la classe sur laquelle on travaille, même si elle n'existe pas encore. Depuis ce `this`, on peut accéder à tous les attributs et aux méthodes avec la syntaxe this.\<attribut\> ou this.\<méthode\>. On peut ainsi utiliser la variable locale `hungry` pour mettre sa valeur dans l'attribut correspondant de l'instance `this.hungry` :

```java
class Human {

  // Attributs
  boolean hungry;

  // Constructeur par défaut
  Human() {
    hungry = false;
  }

  // Constructeur avec paramètre
  Human(boolean hungry) {
    this.hungry = hungry;
  }

}
```

L'utilisation du `this` n'est pas obligatoire lorsque le nom d'un attribut n'est pas caché par celui d'un paramètre, mais c'est parfois plus facile de l'utiliser pour rendre plus visible que la variable ou la fonction qu'on utilise est définie dans la classe ; qu'il s'agit donc d'un attribut ou d'une méthode.

### Méthodes

Les *méthodes* sont des [fonctions](cours/06-fonctions.md) internes à la classe qui représentent des comportements, des choses qu'il est sensé de faire pour le concept représenté par la classe. Lorsque l'on appelle une méthode d'une classe, comme on appelle une fonction, l'exécution se passe dans un contexte particulier propre à l'instance et dans lequel on a accès à tous les attributs de l'objet (`this`).

Toujours pour notre `Human`, on va définir une méthode `eat`, qui ne renvoie rien, donc `void`, et ne prend aucun paramètre. Cette fonction met à jour l'attribut `hungry` pour lui mettre la valeur `false`, car l'humain n'a plus faim après avoir mangé. 

```java
class Human {

  // Attributs
  boolean hungry;

  // Constructeur par défaut
  Human() {
    hungry = false;
  }

  // Constructeur avec paramètre
  Human(boolean hungry) {
    this.hungry = hungry;
  }

  void eat() {
    println("nom nom nom");
    hungry = false;
  }

}
```

## Objets
### Déclaration
Les *objets* sont des instances d'une classe, et on va les stocker comme on stockerait des valeurs entières, flottantes, etc. : dans des variables. Le *type* d'une variable contenant un objet sera le nom de la classe.

```java
Human human; // Variable qui contiendra un objet de la classe Human
```

### Création

Les objets, comme les [tableaux](cours/03-tableaux-matrices.md), sont des *références*, et pour créer des références, il faut utiliser le mot clé `new`, ici suivi de l'appel à un constructeur de la classe.

```java
Human human = new Human(); // Constructeur vide
Human anotherHuman = new Human(true); // Constructeur explicite, cet humain a faim
```

### Manipulation

Pour manipuler ou interagir avec un objet, il faut utiliser le `.` après le nom de l'objet, comme si on "entrait" dans ce qu'il contient : ses attributs et ses méthodes. Après le `.`, on peut donc soit mettre le nom d'un attribut, pour en évaluer sa valeur ou le modifier, soit appeler une méthode de l'objet.

```java
Human human = new Human();
println(human.hungry); // Affiche si l'humain a faim -> false par défaut
human.hungry = true; // On met à jour l'attribut;
println(human.hungry); // Affiche true
human.eat(); // Appel de la méthode eat de notre humain
println(human.hungry); // Affiche false
```

> ℹ On préfère en général éviter d'interagir directement avec les attributs d'un objet, mais de passer plutôt par des méthodes, par exemple `human.setHungry(true)`

### `null`

Si on n'initialise pas une variable objet, la référence n'est pas définie et est alors `null`. Cela signifie que la variable ne contient rien. On peut également "supprimer" la valeur contenue dans une variable objet en lui assignant la valeur `null`.

```java
Human human = new Human();
human.eat(); // Affiche nom nom nom
human = null; // Supprime l'humain référencé
```

Lorsque l'on essaie d'interagir avec une variable objet, soit en accédant à un de ses attributs, soit en appelant une méthode, mais que la variable ne contient rien, donc `null`, on aura une erreur du type `NullPointerException`.

## Listes d'objets

Si l'on doit manipuler un grand nombre d'objets du même type, il y a deux solutions possibles :
- Ce nombre est fixe, on peut alors utiliser un tableau ; par exemple `Human[] humans = new Human[10];`
- Ce nombre est variable et est amené à changer (nouveaux éléments, éléments en moins) pendant l'exécution du code. Dans ce cas, on peut utiliser une `ArrayList`, qui représente donc une liste d'éléments de taille variable.

### ArrayList

Pour déclarer une `ArrayList` d'un certain type d'objets, il faut spécifier ce type entre `<>` :

```java
ArrayList<Human> humans = new ArrayList<Human>();
```

On crée ici une liste initialement vide dans laquelle on pourra rajouter des objets.

> ℹ Vous remarquez l'utilisation du mot clé `new` pour la création de la liste ; ArrayList est une *classe* existante en Java.

La manipulation de la liste se fait via l'appel à différentes méthodes sur cette liste :

- `add(object)` qui prend en paramètre un objet du type d'éléments de la liste, et ajoute cet élément "à la fin" de la liste
- `get(i)` qui prend en paramètre l'indice d'un élément, et renvoie l'élément se trouvant à cette place dans la liste
- `remove(i)` qui prend en paramètre l'indice d'un élément et le supprime de la liste
- `size()` qui renvoie le nombre d'éléments que contient la liste

```java
ArrayList<Human> humans = new ArrayList<Human>();
humans.add(new Human(true));
humans.add(new Human());
humans.add(new Human());
println(humans.size()); // Affiche 3
println(humans.get(0).hungry); // Affiche true
humans.get(0).eat();
println(humans.get(0).hungry); // Affiche false
humans.remove(2);
humans.remove(1);
println(humans.size()); // Affiche 1
```

## Utilité

### Structure

Comme pour les fonctions, définir des classes permet souvent de mieux structurer le code et de lui donner plus de "sens" proche du réel. Une classe permet d'isoler du code spécifique à un concept précis, et de ne pas le perdre au milieu du reste.

### Factorisation

Définir une classe permet de simplifier le code lorsqu'on se sert de plusieurs instances d'un même concept car, que l'on utilise des classes ou non, ces concepts sont présents dans le code.

Imaginons par exemple qu'on ait besoin de définir 20 cercles pour les dessiner ; il nous faut leurs coordonnées (x, y) et leur couleur. Sans classe, il faudrait utiliser trois tableaux, un par information liée à un cercle.

```java
int[] circlesX;
int[] circlesY;
color[] circlesColor;

void setup() {
  circlesX = new int[20];
  circlesY = new int[20];
  circlesColor = new color[20];
  
  for (int i = 0; i < 20; i++) {
    circlesX[i] = int(random(0, 100));
    circlesY[i] = int(random(0, 100));
    circlesColor[i] = randomColor();
  }
}

color randomColor() {
 return color(int(random(0, 256)), 
              int(random(0, 256)), 
              int(random(0, 256)));
}
```

En définissant une classe représentant ces cercles, on simplifie le code tout en le rendant plus lisible :

```java
class Circle {
  int x;
  int y;
  color c;

  Circle(int x, int y, color c) {
    this.x = x;
    this.y = y;
    this.c = c;
  }
}

Circle[] circles;

void setup() {
  circles = new Circle[20];
  for (int i = 0; i < 20; i++) {
    circles[i] = new Circle(int(random(0, 100)), 
                            int(random(0, 100)),
                            randomColor());
  }
}

color randomColor() {
 return color(int(random(0, 256)), 
              int(random(0, 256)), 
              int(random(0, 256)));
}
```

> ⚠ Un code plus simple ne veut pas nécessairement dire plus court. Le code est plus simple car il ne faut plus interagir qu'avec un seul tableau, le tableau d'objets, plutôt qu'avec autant de tableaux qu'on aurait d'attributs dans ces objets.