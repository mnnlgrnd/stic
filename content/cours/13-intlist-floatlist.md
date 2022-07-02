---
title: '13 - IntList et FloatList'
prev_class: '12-dessins-geometrie'
next_class: '14-images-pixels'
---

## Définition

Il est possible de contenir un grand nombre de variables d'un même type dans [tableau](cours/03-tableaux-matrices.md) mais il s'agit d'une structure de données contraignante ; la taille du tableu est *fixe*, déterminée à sa création, et ne pourra pas changer. Si on devait retirer un élément de ce tableau, il faudrait en réalité créer un nouveau tableau de plus petite taille et y mettre les éléments à conserver. Pour des [objets](cours/09-classes.md), on peut utiliser des `ArrayList` qui sont des listes dynamiques, de taille variable donc, et processing propose deux classes similaires pour contenir non pas des objets, mais des variables de type `int` ou `float` ; [`IntList`](https://processing.org/reference/IntList.html) et [`FloatList`](https://processing.org/reference/FloatList.html).

Une [`IntList`](https://processing.org/reference/IntList.html) (resp. [`FloatList`](https://processing.org/reference/FloatList.html)) est donc une liste dynamique contenant des éléments de type `int` (resp. `float`), qui offre les mêmes possibilités qu'un tableau et en plus le fait de pouvoir supprimer des éléments de cette liste.

## Utilisation
> ℹ Les explications suivantes ne mentionneront que les `IntList` mais tout ce qui est dit s'applique de la même façon aux `FloatList`

### Création

Une `IntList` étant une [classe](cours/09-classes.md), on crée une nouvelle liste, un nouvel objet de type `IntList`, grâce au mot clé `new`.

En utilisant le constructeur par défaut, sans paramètre, on crée une nouvelle liste initialement vide.

```java
IntList empty = new IntList(); // Nouvelle liste vide, contiendra des entiers
println(empty); // Affiche IntList size=0 [  ]
```

On peut aussi créer une liste non vide en passant aux paramètres du constructeur un tableau d'entiers.

```java
IntList notEmpty = new IntList({ 0, 1, 2, 3 });
println(notEmpty); // Affiche IntList size=4 [ 0, 1, 2, 3 ]
```

### Manipulation

La manipulation d'une [`IntList`]https://processing.org/reference/IntList.html se fait via l'appel à différentes méthodes sur cette liste :

- `append(value)` qui prend en paramètre un entier et l'ajoute "à la fin" de la liste
- `get(i)` qui prend en paramètre l'indice d'un élément, et renvoie l'élément se trouvant à cette place dans la liste
- `remove(i)` qui prend en paramètre l'indice d'un élément et le supprime de la liste
- `size()` qui renvoie le nombre d'éléments que contient la liste
- `set(i, value)` qui prend en paramètre un indice et un objet et remplace l'élément à cet indice dans la liste par l'objet passé en paramètre. A l'inverse de la même méthode sur une [`ArrayList`](https://processing.org/reference/ArrayList.html), on peut ici utiliser un indice `i` plus grand que la taille actuelle de la liste, processing rajoutera alors des valeurs 0 dans la liste jusqu'à l'indice où l'on souhaite insérer la valeur.

```java
IntList list = new IntList();
println(list.size()); // Affiche 0
list.append(5);
list.append(6);
println(list.size()); // Affiche 2
println(list.get(0)); // Affiche 5
list.remove(0);
println(list.get(0)); // Affiche 6
list.set(3, 1);
println(list); // Affiche IntList size=4 [ 6, 0, 0, 1 ]
```

### Erreurs
Si on essaie d'accéder directement à une position se situant hors du tableau dans les appels à `get` ou `remove`, on aura une erreur du type `ArrayIndexOutOfBoundsException`. 

### Autres méthodes utiles

Au-delà de la manipulation par défaut des éléments d'une [`IntList`](https://processing.org/reference/IntList.html), il existe d'autres méthodes qui peuvent s'avérer utiles :
- `clear()`, qui retire tous les éléments de la liste ; elle sera à nouveau vide
- `shuffle()`, qui met les éléments de la liste dans un ordre aléatoire
- `sort()`, qui trie les éléments de la liste dans l'ordre croissant
- `reverse()`, qui inverse l'ordre des éléments dans la liste
- `sortReverse()`, qui trie les éléments dans l'ordre décroissant ; cela équivant à appeler consécutivement `sort()` et `reverse()`.
- `min()`, qui renvoie le plus petit élément de la liste
- `max()`, qui renvoie le plus grand élément de la liste

