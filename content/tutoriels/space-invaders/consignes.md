---
title: "Space Invaders simplifié"
---

## Introduction

Space Invaders est un jeu d’arcade créé en 1978. Il s’agit du tout premier jeu "shooter' fixe. Dans ce jeu, le joueur incarne un vaisseau qui se déplace latéralement et tente de repousser une vague d’envahisseurs à l’aide d’un canon laser. Les aliens se rapprochent lentement mais sûrement du vaisseau et tirent également des lasers vers le vaisseau. Les lasers se déplacent verticalement et disparaissent quand ils touchent un ennemi ou atteignent le bord de l’écran de jeu. Il y a des obstacles entre le vaisseau et les envahisseurs qui sont progressivement détruits par les lasers.


![LocalSpaceInvaders](tutoriels/space-invaders/images/SpaceInvadersOriginal.png)

![SpaceInvaders](/stic/images/SpaceInvadersOriginal2.png)

## Version minimale

### Vie et fin de jeu 
Dans cette version, les aliens sont inoffensifs et le joueur ne perd jamais. Quand une vague d’aliens est entièrement détruite, une nouvelle vague arrive. 

### Ennemis

Une vague d’aliens a les dimensions suivantes : 5 lignes de 10 aliens. Ils ne se déplacent pas et ne tirent pas. 

### Destruction

Au contact d’un laser, l’alien touché et le laser sont détruits immédiatement. Si un laser atteint le haut de l’écran sans avoir touché un alien, il disparaît. 

### Contrôles

Les mouvements latéraux du vaisseau sont contrôlés par les touches `FLÈCHE-GAUCHE` et `FLÈCHE-DROITE`. La touche `ESPACE` permet de tirer des lasers. 

### Dimensions

Vous pouvez utiliser les dimensions suivantes : 
- Les dimensions de la fenêtre sont de 1000x800 pixels
- Les aliens et le vaisseau sont des rectangles de 50x50 pixels
- Les lasers sont des rectangles de 5x30 pixels 

### Démonstration
<p align="center">
<iframe src="https://openprocessing.org/sketch/1592175/embed/?plusEmbedHash=YTc3Mzc1ODI5ODMzYzhkMTdkYzAyM2U4Yjk1MDc4YWJiZTEyMzc2ZjVmZTRmMTQ4NTQ1MGY5NDdmN2VlNTdlNGMwMWI1ZDNjMzc2NjkyZGEyMThiMWIxZGNmODYyZjEyNmM3ODE3YWUyMjZmMDEyMGVhN2NiYTgwYWNkN2U3Y2RrdGg2VWk4NXkxVWNWVitBZitsbXozUTdOVFQ5UERTd0c2dmpZM0VybXloKzFUMUxDb1dvTU9JWWpBWnlEUVdoSlFscFl5SW1TWXRyeWN2ZWhWVEVBUT09&plusEmbedTitle=true" width="600" height="500"></iframe>
</p>

## Version améliorée

### Fin de jeu

Les aliens se rapprochent lentement mais sûrement du vaisseau. Si le joueur ne parvient pas à détruire l’entièreté de la vague avant que les aliens atteignent le bas de l’écran, le jeu est perdu. 

### Gestion des couleurs

Chaque alien peut, aléatoirement, avoir une des couleurs suivantes : `color(240, 20, 20)`, `color(200, 20, 200)`, `color(20, 200, 20)`, `color(20, 100, 250)`, `color(240, 200, 0)`. 

### Gestion de la difficulté

Lorsque la vague d’aliens est détruite, un nouvelle vague arrive. Chaque vague d’aliens est plus résistante que la précédente : à chaque nouvelle vague, il faut un coup de laser en plus pour détruire un alien. A la deuxième vague, il faudra donc toucher un alien 2 fois pour le détruire, 3 fois pour la troisième vague, et ainsi de suite. 

### Gestion de la transparence

Si vous gérez également la difficulté des vagues, le taux d’opacité d’un alien diminue en fonction du nombre de lasers qui l’ont déjà touché, pour un minimum de 50%. Par exemple, à la vague 3, un alien sera initialement visible à 100%, à 75% après le premier coup et à 50% après le deuxième ; il sera détruit après le troisième coup.

### Démonstration

<p align="center">
<iframe src="https://openprocessing.org/sketch/1592193/embed/?plusEmbedHash=YmI5ZWNkMzIwYzFiZGNhODBkOGM0NzYyN2ZmMTAyNjBiYzc5OGQ4OTk0OTY2YmJmNTUwMjRlOWZmOWU4MmNiMzQ5ODhmOTg5M2E1MTA0ZjU3OWFkMzRjZThjZTliZmU5NDBiNjcyZmIyNmVhNWQ5YmZmOTkyOWRhM2NjOTI0NzFzSkRWU29QRzRzOTZYOXArekUvTmk3OFhNWWRRRjFCbXVwNkUrZ2ZSNmp4UHlwOUlpaE55WUt5NEc0Y1VubWhNM1JlWWJhVnhaQ3N0RmJQL0xyeXJTUT09&plusEmbedTitle=true" width="600" height="500"></iframe>
</p>