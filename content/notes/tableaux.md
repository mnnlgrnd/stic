---
title: "02 - Tableaux"
---

## Définition

Un **tableau** est une collection ordonnée de variables du même type. On accède a une variable du tableau grâce au nom du tableau et à la position de la variable dans celui-ci.

## Déclaration

On déclare un tableau comme on déclare une [variable](notes/variables.md), à ceci près qu'il faut rajouter l'opérateur `[]` pour indiquer qu'il s'agit d'un tableau. On peut ajouter cet opérateur soit après le **type** de données du tableau, soit après son nom. Il s'agit de déclarations équivalentes.

```java
int[] integers;
```

ou

```java
int integers[];
```

On déclare ici une variable appelée `integers` qui est un tableau de nombres entiers.

## Création

Il existe deux façons de créer un tableau :

- On peut créer un tableau vide en indiquant sa taille, le nombre d'éléments qu'il contient :

```java
int[] integers = new int[6];
```

- On peut créer un tableau en indiquant directement les valeurs qu'il contient :

```java
int[] integers = new int[] { 1, 2, 4, 8, 16, 32 };
```

Dans les deux cas, l'utilisation du mot clé `new` est obligatoire. Ce mot clé indique qu'on crée une nouvelle **référence** et est responsable de l'allocation en mémoire.

>⚠️ La taille d'un tableau est fixe et ne peut pas être modifiée après sa création. Si on voulait par exemple ajouter un nouvel élément au tableau, il faudrait en réalité créer un nouveau tableau de plus grande taille.

### Stockage en mémoire

Lorsqu'un programme processing s'exécute, il possède sa propre mémoire dans laquelle seront stockées toutes les variables et tout ce qu'il se déroule dans le programme (appels de fonction, etc.). Cette mémoire se compose de deux parties :

- La mémoire dite statique, le *stack*, qui contient notamment les variables (locales) de type primitif et des **références** vers des données stockées dans le *heap*
- La mémoire dite dynamique, le *heap*, qui contient notamment des tableaux et des objets

<p align="center">
<svg content="&lt;mxfile host=&quot;app.diagrams.net&quot; modified=&quot;2022-06-04T19:42:22.595Z&quot; agent=&quot;5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.5005.63 Safari/537.36&quot; etag=&quot;a0vEkeK99Sm97No7t7oZ&quot; version=&quot;19.0.0&quot; type=&quot;google&quot;&gt;&lt;diagram id=&quot;nCawtDRiWLKSfNkT661O&quot; name=&quot;Mémoire&quot;&gt;7Vttk5s2EP41/pgbQIDNx/h8STpJ06TutNePipGBRkaMLJ9Nfn2FEcawxHeJARkmMzc3aPWC9Dwr7WoXT9D95vCW4yT8nfmETizDP0zQYmJZjofk/0yQ5gJkKkHAIz8XmaVgGX0jSmgo6S7yybbSUDBGRZRUhSsWx2QlKjLMOdtXm60Zrb41wQEBguUKUyj9J/JFmEtn1rSUvyNREBZvNl0vr9ngorFayTbEPtufidDDBN1zxkT+tDncE5phV+CS93vzndrTxDiJxUs67JP3fz5+JDh4hc3P3/4Qv6Vp8EqN8oTpTi1YTVakBQKc7WKfZIMYEzTfh5EgywSvstq9pFzKQrGhsmTKxyfCRSTRe02jIJYywbIGWJVWcqqESwHFXwid49XX4Dj6PaNMihcxi8mplnGf8FrNOqK0JlILkO8lh+8iY57wlnpK2IYInsomRQfrzsn7FEqqKNuXjEtVzmXhOdsz1RArLQtOY5dEyAfFxQ/wgjxAzN9SJ3f8Onou496A7prFYqleZrYBtVNFegqRdg0ItNUVzrYBcHZ6hrgDVD3dqMJjRXD5NHhgTVM3shZAFt2Z9giQbThze0XWQQBE4ktXQBUZFyELWIzpQymdV2Eu23xgmd07gvsfESJVfg3eCVaF/ni+5pXSMUJziR5PH9V4x8K/WUHaJ1VcHM4rF2lROkTiUY2ZPZ/1kqWyU1Yo+uTrzRZ5mUOJCdvxFbkA3rRwzTAPiLiEst2sFZxQLKKn6kyaOFZdP7FIzvGkTVZhiAttcmpqkk9M9So15TXnOD1rlmQNthfeM629x635XM+1N4yaouYzKNX2hMkVZwQCZ8QIzgdH8/lQePxnqP6VJn3btLb9Me+23DFrBkAuduygtNe7LX/MgreJL/ISTXA8eGi1e2QI3iDWlOHhK612jwzBW0R2GDjzibMYPrra7RkA9yPbDNyaoduyZtAPi4ant+i2TJkNLdngMdVuwxxowoYPqm7z5QJQxfC3v3az5UC7BUCVw0TJNgNgG+IkE64o2/nXAnwhLVGL4jRQ8cLESAuMWZ5XpawhmeGZDZSZnXEGD20TkNbiTriKqDb2zMy+e9ZqWr3uGnjCdxoT0s2AbdwcA9AcdBq1186AdXMMwADebNQM2DfHAIzume6oKXBvjQIX4t1DlutnslM/mwmrM5uvt50sl7KZz2a5XNSsFi/Ocl3HMYxIdrnJesr/6A7muDAaWcTQRxKR1I4wvNqJEQR3tMMKw5Bdf4yj2+7CC5hpQxbsXlmAd+A1pttR0wDvAPppgBfhsW8G6ITqZwHmo98RiWqdBbloUYV6Kzj7Sp4/x0FgrR5/20S+f3Rum7itst8avW1nu7xpjdgmXps+W+6K1yn0PJdCAveL2B/zfY36B+naiW36nQAq/kZNbht81r8CbEiioD7P3+Ii+4vOVuhs8PD7pRN6+KjTK792l6bHBIsslr/Ryj/RLX/ohh7+Bw==&lt;/diagram&gt;&lt;/mxfile&gt;" height="211px" version="1.1" viewBox="-0.5 -0.5 579 211" width="579px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<defs/>
	<g>
		<rect fill="none" height="180" pointer-events="all" stroke="var(--dark)" width="225" x="0.5" y="20"/>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="143" y="60"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 70px; margin-left: 144px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; overflow-wrap: normal;">Valeur</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" font-weight="bold" text-anchor="middle" x="173" y="74">Valeur</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="143" y="80"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 90px; margin-left: 144px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">5</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="173" y="94">5</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="143" y="100"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 110px; margin-left: 144px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">true</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="173" y="114">true</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="143" y="120"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 130px; margin-left: 144px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">3.14</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="173" y="134">3.14</text>
			</switch>
		</g>
		<path d="M 188 150 L 258.03 150.03 L 258.03 90.03 L 366.13 90" fill="none" pointer-events="stroke" stroke="var(--dark)" stroke-miterlimit="10"/>
		<path d="M 371.38 90 L 364.38 93.5 L 366.13 90 L 364.38 86.5 Z" fill="var(--dark)" pointer-events="all" stroke="var(--dark)" stroke-miterlimit="10"/>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="143" y="140"/>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="83" y="60"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 70px; margin-left: 84px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; overflow-wrap: normal;">Type</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" font-weight="bold" text-anchor="middle" x="113" y="74">Type</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="83" y="80"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 90px; margin-left: 84px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">int</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="113" y="94">int</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="83" y="100"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 110px; margin-left: 84px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">boolean</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="113" y="114">boolean</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="83" y="120"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 130px; margin-left: 84px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">float</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="113" y="134">float</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="83" y="140"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 150px; margin-left: 84px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">int[]</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="113" y="154">int[]</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="23" y="60"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 70px; margin-left: 24px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; overflow-wrap: normal;">Nom</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" font-weight="bold" text-anchor="middle" x="53" y="74">Nom</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="23" y="80"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 90px; margin-left: 24px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">i</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="53" y="94">i</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="23" y="100"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 110px; margin-left: 24px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">b</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="53" y="114">b</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="23" y="120"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 130px; margin-left: 24px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">f</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="53" y="134">f</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="23" y="140"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 150px; margin-left: 24px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">ti</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="53" y="154">ti</text>
			</switch>
		</g>
		<path d="M 359.75 52.5 C 301.55 52.5 287 105 333.56 115.5 C 287 138.6 339.38 189 377.21 168 C 403.4 210 490.7 210 519.8 168 C 578 168 578 126 541.63 105 C 578 63 519.8 21 468.88 42 C 432.5 10.5 374.3 10.5 359.75 52.5 Z" fill="none" pointer-events="all" stroke="var(--dark)" stroke-miterlimit="10"/>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="20" x="372.5" y="80"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 18px; height: 1px; padding-top: 90px; margin-left: 374px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">1</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="383" y="94">1</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="20" x="392.5" y="80"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 18px; height: 1px; padding-top: 90px; margin-left: 394px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">2</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="403" y="94">2</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="20" x="412.5" y="80"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 18px; height: 1px; padding-top: 90px; margin-left: 414px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">4</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="423" y="94">4</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="20" x="432.5" y="80"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 18px; height: 1px; padding-top: 90px; margin-left: 434px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">8</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="443" y="94">8</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="20" x="452.5" y="80"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 18px; height: 1px; padding-top: 90px; margin-left: 454px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">16</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="463" y="94">16</text>
			</switch>
		</g>
		<path d="M 188 170 L 280.26 170.03 L 280.26 140.03 L 366.13 140" fill="none" pointer-events="stroke" stroke="var(--dark)" stroke-miterlimit="10"/>
		<path d="M 371.38 140 L 364.38 143.5 L 366.13 140 L 364.38 136.5 Z" fill="var(--dark)" pointer-events="all" stroke="var(--dark)" stroke-miterlimit="10"/>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="143" y="160"/>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="83" y="160"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 170px; margin-left: 84px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">boolean[]</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="113" y="174">boolean[]</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="60" x="23" y="160"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 58px; height: 1px; padding-top: 170px; margin-left: 24px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">tb</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="12px" text-anchor="middle" x="53" y="174">tb</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="40" x="372.5" y="130"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 38px; height: 1px; padding-top: 140px; margin-left: 374px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">true</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="393" y="144">true</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="40" x="412.5" y="130"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 38px; height: 1px; padding-top: 140px; margin-left: 414px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">false</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="433" y="144">false</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="40" x="452.5" y="130"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 38px; height: 1px; padding-top: 140px; margin-left: 454px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">true</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="473" y="144">true</text>
			</switch>
		</g>
		<rect fill="none" height="10" pointer-events="all" stroke="none" width="45" x="385.5" y="30"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 43px; height: 1px; padding-top: 35px; margin-left: 387px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; overflow-wrap: normal;">Heap</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" font-weight="bold" text-anchor="middle" x="408" y="39">Heap</text>
			</switch>
		</g>
		<rect fill="none" height="10" pointer-events="all" stroke="none" width="45" x="90.5" y="30"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 43px; height: 1px; padding-top: 35px; margin-left: 92px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; overflow-wrap: normal;">Stack</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" font-weight="bold" text-anchor="middle" x="113" y="39">Stack</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="none" width="30" x="158" y="140"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 28px; height: 1px; padding-top: 150px; margin-left: 159px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">###</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="173" y="154">###</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="none" width="30" x="158" y="160"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 28px; height: 1px; padding-top: 170px; margin-left: 159px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">###</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="173" y="174">###</text>
			</switch>
		</g>
		<rect fill="none" height="20" pointer-events="all" stroke="var(--dark)" width="20" x="472.5" y="80"/>
		<g transform="translate(-0.5 -0.5)">
			<switch>
				<foreignObject height="100%" pointer-events="none" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;" width="100%">
					<div style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 18px; height: 1px; padding-top: 90px; margin-left: 474px;" xmlns="http://www.w3.org/1999/xhtml">
						<div data-drawio-colors="color: var(--dark); " style="box-sizing: border-box; font-size: 0px; text-align: center;">
							<div style="display: inline-block; font-size: 13px; font-family: Helvetica; color: var(--dark); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;">32</div>
						</div>
					</div>
				</foreignObject>
				<text fill="var(--dark)" font-family="Helvetica" font-size="13px" text-anchor="middle" x="483" y="94">32</text>
			</switch>
		</g>
	</g>
	<switch>
		<g requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"/>
		<a target="_blank" transform="translate(0,-5)" xlink:href="https://www.diagrams.net/doc/faq/svg-export-text-problems">
			<text font-size="10px" text-anchor="middle" x="50%" y="100%">Text is not SVG - cannot display</text>
		</a>
	</switch>
</svg>
</p>

> ⚠️ Le stockage en mémoire est en réalité plus complexe, l'important ici est de comprendre la différence entre une valeur et une référence. Pour plus de détails sur la gestion de la mémoire lors de l'exécution d'un programme Java, Google est votre ami.

## Manipulation

Une fois un tableau déclaré et créé, on peut accéder à sa taille et aux différents éléments qu'il contient.

### Taille du tableau

La taille d'un tableau est déterminée à sa création et ne peut pas être changée, on peut la récupérer grâce au champ spécial `length` du tableau, de la façon suivante :

```java
int[] integers = new int[] { 1, 2, 3 };
println(integers.length); // Affiche 3
```

### Elements du tableau

Pour accéder à un élément particulier du tableau, il faut utiliser l'opérateur de tableau et l'indice de l'élément après le nom du tableau, par exemple `[1]`.

> ⚠️ En informatique, on commence à compter à partir de 0. Le premier élément aura donc l'indice 0, le deuxième l'indice 1, ainsi de suite.

Lorsque l'on accède à un élément du tableau, on récupère une variable (celle stockée dans le heap), et on peut donc s'en servir comme tel ; c'est-à-dire lui assigner une valeur, ou l'évaluer dans des expressions.

```java
int[] integers = new int[] { 1, 2, 3 };

// Evalue la variable à l'indice 0 dans le tableau et affiche 1
println(integers[0]); 

// Assigne la valeur 0 à la variable à l'indice 1 dans le tableau
integers[1] = 0; 

// Evalue la variable à l'indice 1 dans le tableau et affiche 0
println(integers[0]);

// Evalue la variable à l'indice 2 dans le tableau et affiche 3
println(integers[2]); 
```

### Erreurs

- Lorsque l'on essaie d'accéder à un élément dont l'indice est supérieur à la taille du tableau, c'est-à-dire à une position **hors** du tableau, l'exécution du code provoquera une erreur du type `ArrayIndexOutOfBoundsException` avec l'indice auquel on a voulu accéder.