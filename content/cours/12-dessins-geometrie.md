---
title: '12 - Dessins et géometrie'
prev_class: '11-bases-processing'
next_class: '13-intlist-floatlist'
---

## Fenêtre

La fenêtre de processing est un *repère à deux dimensions* dans lequel des coordonnées *(x, y)* correspond à un *pixel*. L'axe horizontal, des *x*, croît de gauche à droite et l'axe vertical, des *y*, croît de bas en haut. L'origine *(0, 0)* de ce repère est donc le coin supérieur gauche de la fenêtre.

<p align="center">
<img src="/stic/images/grid-processing-dm.svg" class="svg-dark-mode w-50"/>
<img src="/stic/images/grid-processing-lm.svg" class="svg-light-mode w-50"/>
</p>

## Dessins

### Couleurs
Processing permet de travailler sur deux échelles de couleur différentes :
- En noir et blanc ; la couleur est alors une valeur entière entre 0 (noir) et 255 (blanc)

```java
int black = 0;
int middleGrey = 122;
int white = 255;
```

- En couleur ; la couleur est alors une valeur de type `color` définie par trois valeurs entières allant de 0 à 255 pour les composantes rouge, verte et bleue (on parle de RGB, en anglais). On peut créer des couleurs grâce à la fonction [`color(r, g, b)`](https://processing.org/reference/color_.html) qui prend les valeurs des composantes en paramètre, ou en utilisant directement la notation hexadécimale d'une couleur.

```
color red = color(255, 0, 0);
color green = color(0, 255, 0);
color blue = color(0, 0, 255);
color black = color(0, 0, 0);
color white = color(255, 255, 255);
color someColor = color(13, 201, 154);
color fromHex = #ffffff;
```

Soit une couleur RGB, de type `color`, on peut récupérer la valeur de chacune des composantes RGB grâce aux fonctions [`red`](https://processing.org/reference/red_.html), [`green`](https://processing.org/reference/green_.html)et [`blue`](https://processing.org/reference/blue_.html) :

```java
color c = #FF10AA;
float r = red(c); // 255
float g = green(c); // 16
float b = blue(c); // 170
```

On peut utiliser une couleur pour définir :
- La couleur du fond de la fenêtre via la fonction [`background`](https://processing.org/reference/background_.html)
- La couleur des *traits* (lignes) via la fonction [`stroke`](https://processing.org/reference/stroke_.html) 
- La couleur de *remplissage* des formes géométriques et du texte via la fonction [`fill`](https://processing.org/reference/fill_.html)

L'appel à background remplit le fond avec la couleur passée en paramètre en *effaçant* tout ce qui a été dessiné jusqu'à présent.

Quand on appelle [`stroke`](https://processing.org/reference/stroke_.html) ou [`fill`](https://processing.org/reference/fill_.html), la couleur ne changera pas jusqu'à ce qu'on appelle à nouveau cette fonction avec une autre valeur.

```java
background(255); // Fond blanc

stroke(0); // A partir d'ici, les traits sont noirs
fill(color(255, 0, 0)); // A partir d'ici, le remplissage est en rouge

// On dessine

stroke(color(0, 255, 0)); // A partir d'ici, les traits sont verts
fill(0); // A partir d'ici, le remplissage est noir

// On dessine d'autres choses
```

Alternativement, on peut aussi dire à processing de ne *pas* coloriser les traits ou le remplissage, en appelant respectivant [`noStroke()`](https://processing.org/reference/noStroke_.html) ou [`noFill()`](https://processing.org/reference/noFill_.html). 

Enfin, on peut également appliquer un certain niveau d'opacité en rajoutant un paramètre aux appels de [`background`](https://processing.org/reference/background_.html),  [`stroke`](https://processing.org/reference/stroke_.html) et [`fill`](https://processing.org/reference/fill_.html). Ce paramètre est le niveau d'opacité allant de 0 (complètement opaque) à 255 (complètement transparent).

```java
background(0, 255); // Fond noir complètement opaque
stroke(0, 122); // Trait noir à 50% d'opacité
fill(color(255, 0, 0), 51); // Remplissage rouge à 20% d'opacité
```

### Points et lignes

En processing, on peut dessiner un *point*, un pixel, grâce à la fonction [`point`](https://processing.org/reference/point_.html) qui prend en paramètre les coordonnées *(x, y)* du point.

```java
void setup() {
  size(800, 600);
  background(255);
  stroke(0);

  point(10, 10); // Dessine un point noir en (10, 10)
}
```

On peut dessiner une ligne grâce la fonction [`line`](https://processing.org/reference/line_.html) qui prend en paramètres les coordonnées des points aux deux extrémités de la ligne.

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

On dessine des rectangles grâce à la fonction [`rect`](https://processing.org/reference/rect_.html) qui prend toujours 4 paramètres. Ce que *sont* ces paramètres dépend du mode de dessin des rectangles ; il existe 4 modes différents :

- `CORNER` : on indique les coordonnées *(x, y)* du coin supérieur gauche, la largeur *w* et la hauteur *h* du rectangle.
- `CORNERS` : on indique les coordonnées *(x1, y1)* d'un coin et les coordonnées *(x2, y2)* du coin opposé.
- `CENTER` : on indique les coordonnées *(x, y)* du centre du rectangle, la largeur *w* et la hauteur *h*.
- `RADIUS` : on indique les coordonnées *(x, y)* du centre du rectangle, la moitié de la largeur *w* et la moitié de la hauteur *h*.

On définit le mode de dessin en appelant la fonction [`rectMode`](https://processing.org/reference/rectMode_.html) avec le mode souhaité. Le mode `CORNER` est le mode par défaut.

<p align="center">
<img src="/stic/images/rect-dm.svg" class="svg-dark-mode w-75"/>
<img src="/stic/images/rect-lm.svg" class="svg-light-mode w-75"/>
</p>

```java
void setup() {
  size(800, 600);
  background(0);
  stroke(255);
  fill(255);

  // Dessinons le même rectangle avec chaque mode

  rectMode(CORNER);
  rect(20, 20, 100, 50);

  rectMode(CORNERS);
  rect(20, 20, 120, 70);

  rectMode(CENTER);
  rect(70, 45, 100, 50);

  rectMode(RADIUS);
  rect(70, 45, 50, 25);
}
```

Peu importe le mode, les informations à passer à la fonction pour dessiner un rectangle nous permettent *toujours* d'obtenir toutes les autres informations du rectangle : les coordonnées de tous ses coins, de son centre, sa largeur et sa hauteur.

- `CORNER`, soit les coordonnées *(x, y)* du coin supérieur gauche, la largeur *w* et la hauteur *h* :
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
	- *Ces calculs peuvent s'adapter en prenant d'autres paires de coins opposés ; il faudra notamment prendre la valeur absolue de la largeur et de la hauteur.*


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

On dessine des ellipses grâce à la fonction [`ellipse`](https://processing.org/reference/ellipse_.html) qui prend toujours 4 paramètres. Ce que *sont* ces paramètres dépend du mode de dessin des ellipses ; il existe 4 modes différents :

- `CORNER` : on indique les coordonnées *(x, y)* du coin supérieur gauche, la largeur *w* et la hauteur *h* du rectangle qui "encadre" l'ellipse à dessiner.
- `CORNERS` : on indique les coordonnées *(x1, y1)* d'un coin et les coordonnées *(x2, y2)* du coin opposé du rectangle qui "encadre" l'ellipse à dessiner.
- `CENTER` : on indique les coordonnées *(x, y)* du centre de l'ellipse, la largeur *w* (diamètre sur l'axe horizontal) et la hauteur *h* (diamètre sur l'axe vertical).
- `RADIUS` : indique les coordonnées *(x, y)* du centre de l'ellipse, la moitié de la largeur *w* (rayon sur l'axe horizontal) et la moitié de la hauteur *h* (rayon sur l'axe vertical).

On définit le mode de dessin en appelant la fonction [`ellipseMode`](https://processing.org/reference/ellipseMode_.html) avec le mode souhaité. Le mode `CENTER` est le mode par défaut.
<p align="center">
<img src="/stic/images/ellipse-dm.svg" class="svg-dark-mode w-75"/>
<img src="/stic/images/ellipse-lm.svg" class="svg-light-mode w-75"/>
</p>

On remarque qu'il s'agit en fait exactement du même principe que pour les rectangles, sauf que le dessin concret sera l'ellipse inscrite dans le rectangle défini par les paramètres.

Pour dessiner un cercle, il suffit d'utiliser la même valeur pour la largeur et la hauteur.

### Textes

Au-delà des formes géométriques, on peut également afficher du texte dans la fenêtre processing grâce à la fonction [`text`](https://processing.org/reference/text_.html) qui prend en paramètre une [chaîne de caractères](cours/10-strings.md) et les coordonnées *(x, y)* où placer ce texte.

On peut configurer l'apparence du texte :
- Sa couleur, en appelant la fonction [`fill`](https://processing.org/reference/fill_.html) avec la couleur en paramètre
- Sa taille, en appelant la fonction [`textSize`](https://processing.org/reference/textSize_.html) avec une taille en paramètre
- Son alignement, par rapport aux coordonnées de sa position, en appelant la fonction [`textAlign`](https://processing.org/reference/textAlign_.html) avec un ou deux paramètres :
	- L'alignement horizontal, qui peut être `CENTER`, `LEFT` ou `RIGHT`
	- L'alignement vertical qui peut être `CENTER`, `BOTTOM`, `TOP` ou `BASELINE`

```java
void setup() {
  size(800, 600);
  background(0);
  fill(255);
  textSize(50);
  textAlign(CENTER, CENTER);
  text("HELLO", width / 2, height / 2); // Affiche HELLO au milieu de la fenêtre
}
```

### Ordre des dessins

Chaque nouveau dessin (ligne, rectangle, etc.) est réalisé "par-dessus" la version actuelle de la fenêtre. Ainsi, si on dessine par exemple consécutivement deux rectangles de même taille mais de couleur différente au même endroit, on ne verra plus que le deuxième.

L'appel à [`background`](https://processing.org/reference/background_.html) remplit la fenêtre de la couleur indiquée et efface donc tout ce qui avait été dessiné avant ; c'est pourquoi on utilise en général [`background`](https://processing.org/reference/background_.html) au début de la fonction `draw` pour effacer la frame d'avant.

## Transformations 

### `translate`

Comme expliqué précédemment, les dessins processing se basent sur l'axe par défaut dont l'origine est le coin supérieur gauche de la fenêtre. Il est toutefois possible de *déplacer* cette origine grâce à la fonction [`translate`](https://processing.org/reference/translate_.html) qui prend en paramètre le déplacement en *x* et en *y* à effectuer.

<p align="center">
<img src="/stic/images/translate-dm.svg" class="svg-dark-mode w-75"/>
<img src="/stic/images/translate-lm.svg" class="svg-light-mode w-75"/>
</p>

```java
void setup() {
  size(800, 600);
  background(0);
  stroke(255);
  fill(255);
  rectMode(CENTER);
  
  // L'origine (0, 0) est le coin supérieur gauche
  // On va tracer un rectangle au milieu de l'écran
  rect(width / 2, height / 2, 100, 100);

  // Equivalent en déplaçant l'origine
  translate(width / 2, height / 2); // L'origine (0, 0) est maintenant le centre de la fenêtre
  rect(0, 0, 100, 100);
}
```

Si on réalisait par exemple un dessin à partir du centre de la fenêtre, comme plusieurs cercles concentriques, il serait bien plus facile de déplacer l'origine au centre de la fenêtre et d'ensuite simplement dessiner à partir de l'origine.

### `rotate`

De la même façon qu'il est possible déplacer l'origine des axes, on peut également *changer l'orientation* des axes. Pour ce faire, on utilise la fonction [`rotate`](https://processing.org/reference/rotate_.html) en passant en paramètre l'angle (en radians) de rotation à appliquer. Les axes tournent dans le sens horaire. On peut également transformer un angle en degré en radians grâce à la fonction [`radians`](https://processing.org/reference/radians_.html).

<p align="center">
<img src="/stic/images/rotate-dm.svg" class="svg-dark-mode w-75"/>
<img src="/stic/images/rotate-lm.svg" class="svg-light-mode w-75"/>
</p>

```java
void setup() {
  size(800, 600);
  background(0);
  stroke(255);
  fill(255);
  rectMode(CENTER);
  
  translate(width / 2, height / 2);
  rotate(radians(45)); // Les axes tournent de 45° dans le sens horaire
  rect(0, 0, 100, 100);
}
```

Pour facilement appliquer une rotation à une figure géométrique, il vaut mieux d'abord déplacer l'origine aux coordonnées du centre de la figure, puis d'appliquer la rotation. Sinon, les calculs pour trouver les bonnes coordonnées deviennent assez compliqués.

### `scale`

On peut augmenter ou diminuer la taille des dessins grâce la transformation [`scale`](https://processing.org/reference/scale_.html) qui prend en paramètre le pourcentage de "zoom". Par exemple,  `scale(2)` doublera la taille des figures.

### `pushMatrix` et `popMatrix`

Si l'on veut utiliser des transformations pour faciliter une partie du dessin, on peut se retrouver dans une situation où le nouveau système de coordonnées après ces transformations ne convient pas du tout au reste du dessin. On pourrait envisager de refaire des transformations pour revenir à la situation précédente, mais l'exercice peut être pénible.

Processing permet de sauvegarder l'état du système de coordonnées grâce à la fonction [`pushMatrix`](https://processing.org/reference/pushMatrix_.html). Au moment où on appelle cette fonction, l'état actuel du système de coordonnées est ajouté sur une *stack*, une pile d'états. Plus tard dans le code, en appelant la fonction [`popMatrix`](https://processing.org/reference/popMatrix_.html), on récupère et rétablit le dernier état sauvegardé via [`pushMatrix`](https://processing.org/reference/pushMatrix_.html). On peut ainsi *stacker* plusieurs états et les récupérer un à un.

```java
void setup() {
  size(800, 600);

  // Etat par défaut : origine en haut à gauche
  pushMatrix(); // Je rajoute l'état dans la stack

  translate(10, 10); // L'origine est maintenant (10, 10) selon l'axe original
  pushMatrix(); // Je rajoute cet état dans la stack

  translate(10, 10); // L'origine est maintenant (20, 20) selon l'axe original

  // Dessins

  popMatrix(); // Je retire le dernier état de la stack et le rétablit
  // L'origine est donc de nouveau (10, 10) selon l'axe original

  // Dessins

  popMatrix(); // Je retire le dernier état de la stack et le rétablit
  // L'origine est donc de nouveau (0, 0)
}
```


> ⚠ Lorsque l'on réalise un dessin animé, toutes les transformations appliquées à l'origine et aux axes sont réinitialisées au début de chaque frame. C'est-à-dire que le dessin de chaque frame commence avec l'origine (0, 0) étant le coin supérieur gauche, et pas d'angle de rotation.

## Fonctions utiles
### Distance entre deux points

Pour calculer la distance entre deux points, on peut simplement utiliser la fonction processing `dist`, qui prend les coordonnées de deux points en paramètre et renvoie la distance entre ces points. On pourrait néanmoins facilement réécrire cette fonction :

```java
float distanceBetween(float x1, float y1, float x2, float y2) {
  float dx = x1 - x2;
  float dy = y1 - y2;
  float distance = sqrt(dx * dx + dy * dy);
  return distance;
}
```

### Intersections

#### Entre un point et un rectangle

Un point se situe à l'intérieur d'un rectangle si ses coordonnées sont comprises entre les bords de ce rectangle. 

On utilise le coin supérieur gauche du rectangle, la largeur et la hauteur du rectangle.

```java
boolean isPointInRect(float x, float y,
                      float rx, float ry, float rw, float rh) {
  return x > rx && x < rx+rw &&
         y > ry && y < ry+rh;				  
}
```

#### Entre deux rectangles

Il y a intersection entre deux rectangles lorsque le coin supérieur gauche de chaque rectangle se situe plus haut et plus à gauche que le coin inférieur droit de l'autre rectangle ; cette situation n'est possible que si les rectangles se croisent.

On utilise les coordonnées du coin supérieur gauche, la largeur et la hauteur de chaque rectangle.

```java
boolean isIntersectionRects(
    float x1, float y1, float w1, float h1, 
    float x2, float y2, float w2, float h2) {
  return x1 < x2+w2 && y1 < y2+h2 && 
         x2 < x1+w1 && y2 < y1+h1;			 
}
```

#### Entre un point et un cercle

Un point se situe à l'intérieur d'un cercle si la distance entre ce point et le centre du cercle est plus petite que le rayon du cercle

```java
boolean isPointInCircle(float x, float y,
                        float cx, float cy, float cr) {
  float dx = x - cx;
  float dy = y - cy;
  float distance = sqrt(dx * dx + dy * dy);
  return distance < cr;
}
```

#### Entre deux cercles

Il y a intersection entre deux cercles si la distance entre les centres de ces cercles est plus petite que la somme de leur rayon.

```java
boolean isIntersectionCircles(
    float x1, float y1, float r1, 
    float x2, float y2, float r2) { 
  float dx = x1 - x2;
  float dy = y1 - y2;
  float distance = sqrt(dx * dx + dy * dy);
  return distance < r1 + r2;
}
```

> ℹ Si on remplace `<` et `>` par `<=` et `>=` dans les conditions ci-dessus, on considère alors qu'il y a aussi intersection si les bords se touchent ou si le point est sur le bord.