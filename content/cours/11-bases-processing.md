---
title: "11 - Bases de Processing"
prev_class: "10-strings"
next_class: '12-dessins-geometrie'
---

## Fonctions processing
> ⚠ Ce qui suit n'inclut qu'une partie de ce que peut faire processing. Pour les informations complètes, veuillez vous référer à la documentation officielle : [https://processing.org/reference](https://processing.org/reference)

### Initialisation `setup`

Tout dessin processing complexe, c'est-à-dire qui va utiliser des fonctions, doit définir la fonction [`setup`](https://processing.org/reference/setup_.html) qui commence par définir la taille de la fenêtre :
- Plein écran, en appelant la fonction [`fullScreen()`](https://processing.org/reference/fullScreen_.html)
- Taille fixe, en appelant la fonction [`size(w, h)`](https://processing.org/reference/size_.html) où `w` et `h` seront des valeurs entières correspondant à la largeur et à la hauteur voulues.

```java
void setup() {
  size(800, 600);
	
}
```

C'est également dans le [`setup`](https://processing.org/reference/setup_.html) qu'on va configurer les paramètres globaux du dessin comme :
- Le framerate, le nombre de frames par seconde, via la fonction [`frameRate(x)`](https://processing.org/reference/frameRate_.html) où x sera la valeur souhaitée. Par défaut, le framerate est 60.
- Des spécifités du dessin qui ne changeront pas ([`noStroke()`](https://processing.org/reference/noStroke_.html), etc.)

### Boucle principale `draw`

La "boucle principale" est une boucle implicite qui permet de passer à l'étape suivante du code. En processing, cette boucle principale est la fonction [`draw`](https://processing.org/reference/draw_.html), et une étape est une *frame* du dessin. C'est donc de cette fonction que partira la majorité de la logique du code : la représentation, le dessin, et l'évolution des données.

```java
void draw() {

}
```

La fonction [`draw`](https://processing.org/reference/draw_.html) est appelée automatiquement par processing *x* fois par seconde selon le framerate défini, il ne faut donc **pas** appeler soi-même cette fonction.

### Réactions aux entrées

Les différentes entrées possibles en processing sont accessibles via des fonctions qui seront appelées quand l'évènement correspondant survient, entre deux appels de [`draw`](https://processing.org/reference/draw_.html). Il ne faut définir chaque fonction qu'une seule fois.

> ⚠️ Les réactions aux entrées ne fonctionnent que pour les dessins animés, c'est-à-dire les dessins pour lesquels on a défini le [`draw`](https://processing.org/reference/draw_.html)

### Clavier

Pour une entrée clavier, il y aura toujours deux événèments :
- [`keyPressed()`](https://processing.org/reference/keyPressed_.html) quand on appuie sur la touche du clavier
- [`keyReleased()`](https://processing.org/reference/keyReleased_.html) quand on relâche la touche

> ⚠ Maintenir une touche du clavier enfoncée peut provoquer plusieurs appels consécutifs à [`keyPressed`](https://processing.org/reference/keyPressed_.html) mais ce comportement et la fréquence à laquelle l'évènement est produit dépendent du système d'exploitation. Par conséquent, utiliser [`keyPressed`](https://processing.org/reference/keyPressed_.html) pour bouger des parties du dessin (comme un personnage) causera des mouvements saccadés, moins fluides que si l'évolution des coordonnées était réalisée dans le [`draw`](https://processing.org/reference/draw_.html). 

### Souris

Pour une entrée souris, il y aura toujours les évènements :
- [`mousePressed()`](https://processing.org/reference/mousePressed_.html) quand on appuie sur la touche de la souris
- [`mouseReleased()`](https://processing.org/reference/mouseReleased_.html) quand on relâche la touche
- [`mouseClicked()`](https://processing.org/reference/mouseClicked_.html) après avoir appuyé et relâché une touche

### Exécution d'un dessin processing

<p align="center">
<img src="/stic/images/processing-loop-dm.svg" class="svg-dark-mode w-50"/>
<img src="/stic/images/processing-loop-lm.svg" class="svg-light-mode w-50"/>
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

