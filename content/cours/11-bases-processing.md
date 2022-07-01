---
title: "11 - Bases de Processing"
prev_class: "10-strings"
next_class: '12-intlist-floatlist'
---

## Fonctions processing

### Initialisation `setup`

Tout dessin processing complexe, c'est-à-dire qui va utiliser des fonctions, doit définir la fonction `setup` qui commence par définir la taille de la fenêtre :
- Plein écran, en appelant la fonction `fullScreen()`
- Taille fixe, en appelant la fonction `size(w, h)` où `w` et `h` seront des valeurs entières correspondant à la largeur et à la hauteur voulues.

```java
void setup() {
  size(800, 600);
	
}
```

C'est également dans le `setup` qu'on va configurer les paramètres globaux du dessin comme :
- Le framerate, le nombre de frames par seconde, via la fonction `frameRate(x)` où x sera la valeur souhaitée. Par défaut, le framerate est 60.
- Des spécifités du dessin qui ne changeront pas (`noStroke()`, etc.)

### Boucle principale `draw`

La "boucle principale" est une boucle implicite qui permet de passer à l'étape suivante du code. En processing, cette boucle principale est la fonction `draw`, et une étape est une *frame* du dessin. C'est donc de cette fonction que partira la majorité de la logique du code : la représentation, le dessin, et l'évolution des données.

```java
void draw() {

}
```

La fonction `draw` est appelée automatiquement par processing *x* fois par seconde selon le framerate défini, il ne faut donc **pas** appeler soi-même cette fonction.

### Réactions aux entrées

Les différentes entrées possibles en processing sont accessibles via des fonctions qui seront appelées quand l'évènement correspondant survient, entre deux appels de `draw`. Il ne faut définir chaque fonction qu'une seule fois.

> ⚠️ Les réactions aux entrées ne fonctionnent que pour les dessins animés, c'est-à-dire les dessins pour lesquels on a défini le `draw`

### Clavier

Pour une entrée clavier, il y aura toujours deux événèments :
- `void keyPressed()` quand on appuie sur la touche du clavier
- `void keyReleased()` quand on relâche la touche

> ⚠ Maintenir une touche du clavier enfoncée peut provoquer plusieurs appels consécutifs à `keyPressed` mais ce comportement et la fréquence à laquelle l'évènement est produit dépendent du système d'exploitation. Par conséquent, utiliser `keyPressed` pour bouger des parties du dessin (comme un personnage) causera des mouvements saccadés, moins fluides que si l'évolution des coordonnées était réalisée dans le `draw`. 

### Souris

Pour une entrée souris, il y aura toujours les évènements :
- `void mousePressed()` quand on appuie sur la touche de la souris
- `void mouseReleased()` quand on relâche la touche
- `void mouseClicked()` après avoir appuyé et relâché une touche

### Exécution d'un dessin processing

<p align="center">
<img src="/stic/images/processing-loop-dm.svg" class="svg-dark-mode w-50"/>
<img src="/stic/images/processing-loop.svg" class="svg-light-mode w-50"/>
</p>

## Variables processing
- `width` et `height` contiennent la largeur et la hauteur de la fenêtre processing, disponibles indéfiniment après l'appel de `size`  ou `fullScreen` dans le `setup`
- `frameCount` contient le numéro de la frame actuellement dessinée par `draw`. Commence à 1.
- `frameRate` contient le nombre de frames par seconde défini par la fonction `frameRate(x)`, ou 60 par défaut.
- `mouseX` et `mouseY` contiennent les coordonnées (x,y) de la position du curseur de la souris dans le dessin
- `pmouseX` et `pmouseY` contiennent les coordonnées (x,y) de la position du curseur dans la frame précédente.
- `keyCode` contient une représentation codifée de la touche sur laquelle on vient d'appuyer : par exemple `ENTER`. Toutes les touches ne sont pas codifiées.
- `key` contient le caractère correspondant à la touche sur laquelle on vient d'appuyer : par exemple `' '` pour la touche espace.
- Des constantes correspondant à des "codes", comme pour les touches standard du clavier (`ENTER`, `LEFT`, `RIGHT`, etc.)

## Dessins
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

### Lignes
### Rectangles
### Ellipses
### Textes


## Transformations 
### `translate`
### `rotate`
### `pushMatrix` et `popMatrix`


## Fonctions utiles
### Distance entre deux points
### Intersections

