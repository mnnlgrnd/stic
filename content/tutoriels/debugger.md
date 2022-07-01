---
title: "Débugger (et pas déboguer)"
url: "tutoriels/debugger"
---

## Manuellement
Pour débugger manuellement, le plus "facile" est parfois de simplement afficher en console, aux endroits importants du code, l'état de certaines variables, ou simplement un indicateur pour savoir si on est arrivé à cet endroit du code.

```java
void setup() {
  println("Now calling foo(0)");
  foo(0);
  println("Now calling foo(1)");
  foo(1);
}

void foo(int i) {
  println("Starting foo with parameter " + i);
  for (int j = 0; j < 4; j++) {
    i = i + 2;
    println("i = " + i, "j = " + j);
    println(i + j);
  }
}
```

Le problème avec cette façon de faire est qu'on peut très vite se perdre dans la quantité d'informations qui sera affichée en console, d'autant plus pour des dessins animés où chaque frame génère plein d'impressions en console. Le code s'alourdit également et on en perd en lisibilité.

## Debugger processing

### Activer le mode debug

L'environnement processing offre un outil de débuggage qui permet de mettre l'exécution du code en *pause* aux endroits voulus, et d'avoir accès au [contexte](cours/07-blocs-contextes.md) de cette ligne de code grâce à une fenêtre supplémentaire qui liste toutes les variables visibles à ce moment de l'exécution ainsi que leur valeur.

Il s'agit en réalité d'un mode d'exécution du code différent, que l'on peut activer dans processing via le raccourci `ctrl-d` ou explicitement via le menu :

![[tutoriels/images/enable-debugger.png]]

### Points d'arrêt

Une fois le mode activé, la fenêtre de debug s'ouvre. Elle est actuellement vide puisqu'il n'y a pas encore de code en train d'être exécuté. On peut maintenant définir des points d'arrêt, ou *breakpoints*, en cliquant sur le numéro d'une ligne ; il y aura alors un symbole (losange) à la place du numéro de la ligne. Lorsque le code exécuté arrivera sur cette ligne de code, il se mettra en pause *avant* que cette ligne soit exécutée. Pour retirer le point d'arrêt, on peut cliquer sur le losange et il disparaîtra. On peut définir autant de points d'arrêt que l'on veut, tant qu'il s'agit d'une ligne *exécutable* (par une ligne vide, par exemple).

![[tutoriels/images/breakpoints.png]]

Dans l'exemple ci-dessus, on voit qu'on a mis des points d'arrêt sur les lignes 2, 3, et 8.

### Débugger !
Une fois le code lancé, l'exécution se mettra automatiquement en pause dès qu'on arrive sur un point d'arrêt. La ligne sur laquelle on s'est arrêté aura un symbole différent (une flèche). 

Lorsque l'exécution est en pause, plusieurs choix sont possibles :

![[tutoriels/images/choices.png]]

- Le premier bouton lance l'exécution complète du code. S'il était déjà lancé, il se relançera ; c'est la même chose que pour le mode d'exécution normal.
- Le deuxième bouton "step" permet d'exécuter la ligne de code actuelle, et de passer à la suivante comme si on y avait mis un point d'arrêt.
- Le troisième bouton "continue" permet de relancer l'exécution du code jusqu'au prochain point d'arrêt.

Le bouton step permet ainsi d'exécuter le code ligne par ligne et de voir tous les changements dans le contexte au fur et à mesure.

### Exemple
- Dans l'appel de `foo(0)`, on s'arrête sur la ligne 8 lors de la première boucle du `for`. On voit dans la fenêtre des variables que `i` vaut 0 et `j` vaut 0.

![[tutoriels/images/debug.png]]

- On clique sur le bouton "step" et on passe à la ligne 9. On voit dans la fenêtre des variables que `i` vaut maintenant 2 (résultat de `i` + 2 à la ligne d'avant).

![[tutoriels/images/debug-2.png]]

- Ainsi de suite...