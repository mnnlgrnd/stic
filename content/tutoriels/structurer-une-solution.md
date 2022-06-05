---
title: "Structurer une solution processing"
---

## Vue d'ensemble
Une solution processing contiendra

-   La déclaration de variables globales (visibles dans tous les blocs)
-   Le `setup`
-   Le `draw`
-   Les fonctions de réaction aux inputs pertinantes (`mousePressed`, `keyPressed`, etc.)
-   Des fonctions globales, utilitaires
-   Des classes

Il est plus facile d'écrire une classe dans un onglet spécifique pour cette classe, et, si le code devient trop long, de regrouper en différents onglets (~ bloc logique) les différentes fonctions.

## Etat et données

L'_état_ du code est l'ensemble des informations (~ variables) qui permettent, à tout moment, de représenter le dessin et de le faire évoluer.

### Constantes

Les variables **constantes** sont des valeurs qui ne changeront pas lors de l'exécution du code, mais qui seront amenées à être utilisées régulièrement. On préfère ainsi voir apparaître ce genre de valeurs dans des variables constantes, pour pouvoir facilement les changer sans devoir reparcourir tout le code. 

Lorsque ces variables sont bien nommées, elles peuvent également améliorer la lisibilité du code :

```java
int WON = 1;
int PLAYING = 0;
int LOST = -1;

int status = PLAYING;

// ... Some code

if (status == WON) {
  // Do something if we won
} else if (status == LOST) {
  // Do something else if we lost
} else {
  // Continue playing
}
```

### Déterminer les informations nécessaires

Les autres variables sont déterminées par ce dont nous avons besoin pour avoir le comportement voulu. Par exemple, si on veut dessiner une balle qui rebondit sur les bords de l'écran, il faudra connaître les informations qui permettent de dessiner cette balle : ses coordonnées, sa taille, sa couleur, etc. Ce qu'on peut voir comme une seule information doit parfois être stockée en plusieurs variables.

> ⚠️ Il est **difficile** de réussir à déterminer toutes les variables dont on a besoin dès le début. C'est seulement en avançant dans la solution et dans les fonctionnalités implémentées qu'on se rend compte qu'il manque des informations.

### Evolution des données

Les variables non constantes sont amenées à changer lors de l'exécution du code. On peut distinguer deux types d'évolution :
- L'évolution naturelle (dans le `draw`)
- L'évolution forcée en réaction aux entrées clavier/souris de l'utilisateur

## Initialisation `setup`

Tout dessin processing doit définir la fonction `setup` dans laquelle il convient d'initialiser l'état, les valeurs initiales des données. On peut aussi y configurer certains paramètres globaux du dessin (largeur des lignes, etc.)

```java
void setup() {
  size(800, 600);

  // Some global drawing parameters

  // Data initialization
	
}
```

## Boucle principale `draw`

La "boucle principale" est une boucle implicite qui permet de passer à l'étape suivante du code. En processing, cette boucle principale est la fonction `draw`, et une étape est une *frame* du dessin. C'est donc de cette fonction que partira la majorité de la logique du code : la représentation, le dessin, et l'évolution naturelle des données. L'ordre des différentes mises à jour de données et des dessins dépendra du comportement voulu

```java
void draw() {
  background(0); // Hide previous frame if needed

  // Update state

  // Draw state

}
```

## Réactions aux entrées

Les différentes entrées possibles en processing sont accessibles via des fonctions qui seront appelées quand l'évènement correspondant survient, entre deux appels de `draw`. Il ne faut définir chaque fonction qu'une seule fois

> ⚠️ Les réactions aux entrées ne fonctionnent que pour les dessins animés, c'est-à-dire les dessins pour lesquels on a défini le `draw`

### Clavier

Pour une entrée clavier, il y aura toujours deux événèments :
- `void keyPressed()` quand on appuie sur la touche du clavier
- `void keyReleased()` quand on relâche la touche

Attention, maintenir une touche du clavier enfoncée peut provoquer plusieurs appels consécutifs à `keyPressed` mais ce comportement et la fréquence à laquelle l'évènement est produit dépendent du système d'exploitation. Par conséquent, utiliser `keyPressed` pour bouger des parties du dessin (comme un personnage) causera des mouvements saccadés, moins fluides que si l'évolution des coordonnées était réalisée dans le `draw`. 

### Souris

Pour une entrée souris, il y aura toujours les évènements :
- `void mousePressed()` quand on appuie sur la touche de la souris
- `void mouseReleased()` quand on relâche la touche
- `void mouseClicked()` quand on a appuyé et relâché une touche

## Fonctions

Ecrire des fonctions permet de ne définir qu'une seule fois un bloc de code qui sera amené à être utilisé plusieurs fois. On peut également écrire des fonctions simplement pour améliorer la lisibilité (à condition de bien nommer les fonctions) ou pour alléger un long bloc de code.

```java
int x1 = 0; int y1 = 0;
int x2 = 10; int y2 = 20;

void setup() {
  size(500, 500);

  fill(int(random(256)));
  ellipse(x1, y1, 20, 20);
	
  fill(int(random(256)));
  ellipse(x2, y2, 20, 20);
}
```

Devient

```java
int x1 = 0; int y1 = 0;
int x2 = 10; int y2 = 20;

void setup() {
  size(500, 500);
  drawCircleWithRandomColor(x1, y1);
  drawCircleWithRandomColor(x2, y2);
}

void drawCircleWithRandomColor(float x, float y) {
  fill(int(random(256)));
  ellipse(x, y, 20, 20);
}
```

## Classes

Les classes permettent de définir des concepts complexes et d'y regrouper les différentes informations (= attributs) et comportements (= méthodes) de ces concepts. Elles permettent, comme les fonctions, d'améliorer la structure et la lisibilité du code. 

Il n'est pas nécessaire de faire des classes (ou des fonctions), mais il est parfois plus facile de concevoir directement la solution en orienté objet ("je vais faire des objets Balle"). Bien souvent, lorsque l'on détermine les informations nécessaires, elles-mêmes sont déduites des concepts qui peuvent directement être traduits en classes.

```java
class CircleWithRandomColor {
  int x, y;
  int diameter;
  int c;

  CircleWithRandomColor(int x, int y, int diameter) {
	this.x = x;
	this.y = y;
	this.diameter = diameter;
	this.c = int(random(256)));	  
  }

  void display() {
    ellipseMode(DIAMETER);
    fill(c);
    ellipse(x, y, diameter, diameter);
  }
}
```

## Conseils généraux
- Aller à l'essentiel, d'abord faire fonctionner ce qu'on veut puis seulement essayer d'améliorer ou de simplifier
- Isoler des fonctionnalités pour seulement ensuite les intégrer au code principal
- Avancer petit à petit, ne pas essayer de tout faire en une fois
- Débugger, via le debugger de processing ou en affichant en console ce qu'il se passe, les valeurs, etc.

## Exemple

Ci-dessous un tutoriel processing (disponible ici) montrant comment réaliser le dessin d'une balle qui part du centre de l'écran vers une direction aléatoire, et rebondit sur les bords

// TODO