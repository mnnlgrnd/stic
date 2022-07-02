---
title: '14 - Images et pixels'
prev_class: '13-intlist-floatlist'
next_class: '15-tables'
---

## Images

Processing permet de charger des images depuis des fichiers et de les manipuler ensuite pour, notamment, les afficher dans la fenêtre. Ces images peuvent ensuite être sauvegardées dans un fichier.

Une image est représentée par la classe [`PImage`](https://processing.org/reference/PImage.html).

### Chargement et sauvegarde

Pour charger une image depuis un fichier existant, il faut utiliser la fonction processing [`loadImage`](https://processing.org/reference/loadImage_.html) avec, en paramètre, une [chaîne de caractères](cours/10-strings.md) contenant le chemin vers le fichier de l'image.

> ℹ Ce chemin peut être spécifié de façon relative depuis l'endroit où se situe le fichier .pde (processing) à exécuter, ou de façon absolue en partant de la racine C:\\ (Windows) ou / (Unix).

```java
PImage img;

void setup() {
  img = loadImage("images/dog.png");
}
```

Processing ne permet pas de charger des images *avant* le `setup`. On ne peut donc pas appeler la fonction [`loadImage`](https://processing.org/reference/loadImage_.html) au niveau des variables globales. 

Les formats d'image acceptés sont `gif`, `jpg`, `png` et `tga`.

> ⚠ Si le chemin spécifié pour charger une image n'existe pas, la fonction renverra `null`.

On peut sauvegarder une image grâce à la méthode `save` sur l'image en 
passant en paramètre le chemin vers le fichier où on l'on veut sauver l'image. Si ce fichier n'existe pas, il sera créé.

```java
PImage img;

void setup() {
  img = loadImage("images/dog.png"); // Charge l'image dog.png
  img.save("images/renamedDog.png"); // Sauve l'image dans un autre fichier
}
```

### Manipulation

#### Attributs

Une fois une image chargée, on a accès 
- A sa largeur, via l'attribut `width`
- A sa hauteur, via l'attribut `height`
- Aux pixels qui la composent, stockés dans un attribut `pixels`, un *tableau à une dimension* de `color`.

Comme les pixels sont stockés dans un tableau à une dimension, on ne peut pas directement accéder à un pixel via ses coordonnées *(x, y)*. Il faut d'abord convertir ces coordonnées dans un repère à deux dimensions (~ matrice) à leur coordonnée équivalente à une dimension. Ce calcul est relativement dès lors qu'on connaît la largeur de l'image (ou de la matrice), car le tableau a une dimension contient en fait le contenu de chaque *ligne* de la matrice, mise bout à bout.


<p align="center">
<img src="/stic/images/1d-2d-dm.svg" class="svg-dark-mode w-75"/>
<img src="/stic/images/1d-2d-lm.svg" class="svg-light-mode w-75"/>
</p>


La formule pour passer des coordonnées *(x, y)* à deux dimensions à la coordonnée *k* à une dimension, connaissant la largeur *w*, est `k = y x w + x`. On multiplie *y*, le nombre de lignes, par la largeur de l'image *w*, car on aura, avant le *x*, l'indice de la colonne, tous les éléments des lignes d'avant, sachant qu'on a *w* éléments par ligne et *y* lignes.

Similairement, la formule pour passer de la coordonnée *k* à une dimension aux coordonnées *(x, y)*, connaissant la largeur w est :
- `y = int(k / w)`, la division entière de *k* par la largeur, pour savoir combien de lignes *complètes* sont incluses jusqu'à la position *k*
-  `x = k % w`, le reste de la division entière de *k* par la largeur, pour savoir combien d'éléments il y a sur la ligne actuelle *incomplète* de la matrice où se situe *k*

```java
PImage img;

void setup() {
  img = loadImage("images/dog.png"); // Charge l'image dog.png

  // Parcourir les pixels
  for (int k = 0; k < img.pixels.length; k++) {
    int x = k % img.width;
    int y = k / img.width;
    if (img.pixels[k] != img.get(x, y)) {
      println("Pas possible ?!"); // On ne devrait jamais arriver ici
    }
  }

  // Equivalent à
  for (int x = 0; x < img.width; x++) {
    for (int y = 0; y < img.height; y++) {
      int k = y * img.width + x;
      if (img.pixels[k] != img.get(x, y)) {
        println("Pas possible ?!"); // On ne devrait jamais arriver ici
      }
    }
  }
}
```

#### Méthodes

La classe `PImage` propose des méthodes utilitaires pour plus facilement manipuler des images :
- `get(x, y)` qui renvoie la couleur (`color`) du pixel en position *(x, y)* sur l'image.
- `get(x, y, w, h)` qui renvoie une sous partie de l'image ; un rectangle dont le coin supérieur gauche est en position *(x, y)*, de largeur *w* et de hauteur *h*.
- `set(x, y, c)` qui change la couleur du pixel en position *(x, y)* par la couleur *c* passée en paramètre.
- `save(filename)` comme déjà mentionné, pour sauver l'image dans un fichier *filename*.

Il est plus facile d'interagir avec les pixels de l'image avec les méthodes `get` et `set`, mais cela est moins efficace que d'accéder directement aux éléments du tableau de pixels.

## Pixels
### Chargement
### Manipulation