---
title: "Structurer une solution processing"
url: "tutoriels/structurer-une-solution"
---

## Vue d'ensemble
Une solution [processing](cours/11-bases-processing.md) contiendra

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

Les [variables](cours/01-variables-litteraux.md) **constantes** sont des valeurs qui ne changeront pas lors de l'exécution du code, mais qui seront amenées à être utilisées régulièrement. On préfère ainsi voir apparaître ce genre de valeurs dans des variables constantes, pour pouvoir facilement les changer sans devoir reparcourir tout le code. 

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

## Initialisation

C'est en général dans le `setup` qu'on va initialiser l'état, les valeurs initiales des données. On peut aussi y configurer certains paramètres globaux du dessin (largeur des lignes, etc.).

```java
void setup() {
  size(800, 600);

  // Configuration globale du dessin

  // Initialisation des données
	
}
```

## Boucle principale

C'est du `draw` que partira la majorité de la logique du code : la représentation, le dessin, et l'évolution naturelle des données. L'ordre des différentes mises à jour de données et des dessins dépendra du comportement voulu.

```java
void draw() {
  background(0);

  // Dessiner

  // Faire évoluer les données

}
```

## Réactions aux entrées

Il faudra définir les fonctions correspondant à toutes les entrées possibles pour le dessin et y ajouter la logique voulue. Cette logique est en général un changement dans l'état des données qui aura un impact sur l'évolution naturelle des données dans le `draw`.

On pourrait par exemple imaginer une voiture qui roule relativement vite sur une avenue dégagée. Le mouvement est continu, on ferait donc évoluer les informations de position dans le `draw`. Au loin, le conducteur aperçoit un feu de signalisation qui vient de passer orange. En *réaction* à ce *signal*, la position de la voiture ou sa vitesse ne va pas changer, mais le conducteur va appuyer sur le frein pour appliquer une décélaration qui fera diminuer la vitesse. Il faut donc en général concevoir les fonctions de réaction aux entrées comme une réaction ponctuelle à un signal sans directement appliquer la conséquence de cette réaction.

```java
int x = 0;
int speed = 10;
int acceleration = 0;

void setup() {
  fullScreen();
  noStroke();
  fill(255);
}

void draw() {
  background(0);

  ellipse(x, height / 2, 50, 50);

  speed = constrain(speed + acceleration, -15, 30);
  x += speed;
}

void keyPressed() {
  // Signal, on appuie sur l'accélérateur ou le frein
  // On ne modifie pas la vitesse directement
  if (keyCode == LEFT) {
    acceleration = -1;  
  } else if (keyCode == RIGHT) {
    acceleration = 1;  
  }
}

void keyReleased() {
  // Signal, on relâche l'accélérateur ou le frein
  // On ne modifie pas la vitesse directement
  acceleration = 0;
}
```

## Fonctions et classes

L'utilisation de [fonctions](cours/06-fonctions.md) et de [classes](cours/09-classes.md) n'est fondamentalement pas obligatoire pour mettre au point une solution, mais on se prive alors de mécanismes précieux permettant de simplifier le code, le rendre plus lisible, d'éviter la redondance, etc.

Prenons par exemple un dessin où un personnage glisse sur le sol jusqu'à rencontrer un obstacle, auquel cas il trouve une nouvelle direction "libre" et continue sa glissade. Le code suivant nous permet facilement de comprendre *ce que fait le dessin*. *Comment* le dessin est effectivement réalisé dépendra de la façon dont on aura défini et implémenté les différentes classes/fonctions.

```java
MyMap map;
MyCharacter character;

void setup() {
  fullScreen();

  map = new Map();
  map.addRandomObstacles();
  
  character = new MyCharacter(width / 2, height / 2);
  character.chooseRandomDirection();
}

void draw() {
  background(0);

  map.display();
  character.display();

  character.move();
  
  if (character.isFacingAnObstacle()) {
    character.changeDirection();
  }

}
```

Il est parfois plus facile de concevoir directement la solution en orienté objet ("je vais faire des objets Balle"). Bien souvent, lorsque l'on détermine les informations nécessaires, elles-mêmes sont déduites des concepts qui peuvent directement être traduits en classes.

## Conseils généraux
- Aller à l'essentiel, d'abord faire fonctionner ce qu'on veut puis seulement essayer d'améliorer ou de simplifier
- Isoler des fonctionnalités pour seulement ensuite les intégrer au code principal
- Avancer petit à petit, ne pas essayer de tout faire en une fois
- [Débugger](tutoriels/debugger.md), via le debugger de processing ou en affichant en console ce qu'il se passe, les valeurs, etc.

## Exemple

Un tutoriel processing (disponible ici) montrant comment réaliser le dessin d'une balle qui part du centre de l'écran vers une direction aléatoire, et rebondit sur les bords, est disponible ici : [http://oppr.org/s/JADVJw4f](http://oppr.org/s/JADVJw4f)
