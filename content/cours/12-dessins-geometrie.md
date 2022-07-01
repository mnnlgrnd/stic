---
title: '12 - Dessins et géometrie
prev_class: '11-bases-processing'
next_class: '13-images-pixels'
---

## Dessins
### Fenêtre

La fenêtre de processing est un repère à deux dimensions dans lequel une coordonnée *(x, y)* correspond à un pixel. L'axe horizontal, des x, croît de gauche à droite et l'axe vertical, des y, croît de bas en haut. L'origine *(0,0)* de ce repère est donc le coin supérieur gauche de la fenêtre.

<p align="center">
<img src="/stic/images/grid-processing-dm.svg" class="svg-dark-mode w-50"/>
<img src="/stic/images/grid-processing-lm.svg" class="svg-light-mode w-50"/>
</p>

### Couleurs
Processing permet de travailler sur deux échelles de couleur différentes :
- En noir et blanc ; la couleur est alors une valeur entière entre 0 (noir) et 255 (blanc)

```java
int black = 0;
int middleGrey = 122;
int white = 255;
```

- En couleur ; la couleur est alors une valeur de type `color` contenant trois valeurs entières allant de 0 à 255 pour les composantes rouge, verte et bleue.

```
color red = color(255, 0, 0);
color green = color(0, 255, 0);
color blue = color(0, 0, 255);
color black = color(0, 0, 0);
color white = color(255, 255, 255);
color someColor = color(13, 201, 154);
```

On peut utiliser une couleur pour définir :
- La couleur du fond de la fenêtre via la fonction `background`
- La couleur des *traits* (lignes) via la fonction `stroke` 
- La couleur de *remplissage* des formes géométriques et du texte via la fonction `fill`

L'appel à background remplit le fond avec la couleur passée en paramètre en *effaçant* tout ce qui a été dessiné jusqu'à présent.

Quand on appelle `stroke` ou `fill`, la couleur ne changera pas jusqu'à ce qu'on appelle à nouveau cette fonction avec une autre valeur.

```java
background(255); // Fond blanc

stroke(0); // A partir d'ici, les traits sont noirs
fill(color(255, 0, 0)); // A partir d'ici, le remplissage est en rouge

// On dessine

stroke(color(0, 255, 0)); // A partir d'ici, les traits sont verts
fill(0); // A partir d'ici, le remplissage est noir

// On dessine d'autres choses
```

Alternativement, on peut aussi dire à processing de ne *pas* coloriser les traits ou le remplissage, en appelant respectivant `noStroke()` ou `noFill()`. 

Enfin, on peut également appliquer un certain niveau d'opacité en rajoutant un paramètre aux appels de `stroke` et `fill`. Ce paramètre est le niveau d'opacité allant de 0 (complètement opaque) à 255 (complètement transparent).

```java
stroke(0, 122); // Trait noir à 50% d'opacité
fill(color(255, 0, 0), 51); // Remplissage rouge à 20% d'opacité
```

### Points et lignes

En processing, on peut dessiner un *point*, un pixel, grâce à la fonction `point` qui prend en paramètre les coordonnées x et y du point.

```java
void setup() {
  size(800, 600);
  background(255);
  stroke(0);

  point(10, 10); // Dessine un point noir en (10, 10)
}
```

On peut dessiner une ligne grâce la fonction `line` qui prend en paramètres les coordonnées des points aux deux extrémités de la ligne.

```java
void setup() {
  size(800, 600);
  background(255);
  stroke(0);

  line(0, 0, width, height); // Dessine une ligne diagonale
  line(width, 0, 0, height); // Dessine l'autre ligne diagonale
}
```

### Rectangles

On dessine des rectangles grâce à la fonction `rect` qui prend toujours 4 paramètres. Ce que *sont* ces paramètres dépend du mode de dessin des rectangles ; il existe 4 modes différents :

- `CORNER` : on indique les coordonnées *(x, y)* du coin supérieur gauche, la largeur *w* et la hauteur *h* du rectangle
- `CORNERS` : on indique les coordonnées *(x1, y1)* du coin supérieur gauche et les coordnnées *(x2, y2)* du coin inférieur droit
- `CENTER` : on indique les coordonnées *(x, y)* du centre du rectangle, la largeur *w* et la hauteur *h*
- `RADIUS` : indique les coordonnées *(x, y)* du centre du rectangle, la moitié de la largeur *w* et la moitié de la hauteur *h* 

On définit le mode de dessin en appelant la fonction `rectMode` avec le mode souhaité. Le mode `CORNER` est le mode par défaut.
<p align="center">
<img src="/stic/images/rect-dm.svg" class="svg-dark-mode w-75"/>
<img src="/stic/images/rect-lm.svg" class="svg-light-mode w-75"/>
</p>

Peu importe le mode, les informations à passer à la fonction pour dessiner un rectangle nous permettent toujours d'obtenir toutes les autres informations du rectangle : les coordonnées de tous ses coins, de son centre, sa largeur et sa hauteur.

- `CORNER`, soit les coordonnées *(x, y)*, la largeur *w* et la hauteur *h* :
	- Le coin supérieur droit est *(x + w, y)*
	- Le coin inférieur gauche est *(x, y + h)*
	- Le coin inférieur droit est *(x + w, y + h)*
	- Le centre du rectangle est *(x + w / 2, y + h / 2)*
- `CORNERS`, soit les coordonnées *(x1, y1)* du coin supérieur gauche et les coordonnées *(x2, y2)* du coin inférieur droit :
	- Le coin supérieur droit est *(x2, y1)*
	- Le coin inférieur gauche est *(x1, y2)*
	- La largeur *w* est égale à *x2 - x1*
	- La hauteur *h* est égale *y2 - y1*
	- Le centre du rectangle est *(x1 + w / 2, y1 + h / 2)*
- `CENTER`, soit les coordonnées *(x, y)* du centre, la largeur *w* et la hauteur *h* :
	- Le coin supérieur gauche est *(x - w / 2, y - w / 2)*
	- Le coin supérieur droit est *(x + w / 2, y - h / 2)*
	- Le coin inférieur gauche est *(x - w / 2, y + h / 2)*
	- Le coin inférieur droit est *(x + w / 2, y + h / 2)*
- `RADIUS`, soit les coordonnées *(x, y)* du centre, la moitié de la largeur *w* et la moitié de la hauteur *h* :
	- Le coin supérieur gauche est *(x - w, y - h)*
	- Le coin supérieur droit est *(x + w, y - h)*
	- Le coin inférieur gauche est *(x - h, y + h)*
	- Le coin inférieur droit est *(x + w, y + h)*
	- La largeur est égale à *2 \* w*
	- La hauteur est égale à *2 \* h*

### Ellipses

<p align="center">
<img src="/stic/images/ellipse-dm.svg" class="svg-dark-mode w-75"/>
<img src="/stic/images/ellipse-lm.svg" class="svg-light-mode w-75"/>
</p>


### Textes


## Transformations 
### `translate`
### `rotate`
### `pushMatrix` et `popMatrix`


## Fonctions utiles
### Distance entre deux points
### Intersections

