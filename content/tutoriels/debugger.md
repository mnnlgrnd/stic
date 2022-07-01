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
L'environnement processing offre un outil de débuggage qui permet de mettre l'exécution du code en *pause* aux endroits voulus, et d'avoir accès au [contexte](cours/07-blocs-contextes.md) de cette ligne de code grâce à une fenêtre supplémentaire qui liste toutes les variables visibles à ce moment de l'exécution ainsi que leur valeur.

Il s'agit en réalité d'un mode d'exécution du code différent, que l'on peut activer dans processing via le raccourci `ctrl-d` ou explicitement via le menu :

{{ $image := .Resources.GetMatch "enable-debugger.png" }} 
{{ with $image }} 
  <img src="{{ .RelPermalink }}" width="{{ .Width }}" height="{{ .Height }}"> 
{{ end }}

//
![[tutoriels/images/enable-debugger.png]]