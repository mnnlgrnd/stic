---
title: '15 - Tables'
prev_class: '14-images-pixels'
---

## Définition

Processing permet de charger des fichiers tabulaires (`csv`) pour en manipuler les données, supprimer/rajouter des lignes, etc. Ces données sont stockées dans une *table*, représentée par la classe [`Table`](https://processing.org/reference/Table.html). On peut facilement se représenter de quoi il s'agit en visualisant une feuille Excel. On peut aussi créer soi même des tables et les sauvegarder dans des fichiers.

## Chargement, création et sauvegarde

### Chargement

Pour charger une table depuis un fichier, il faut utiliser la fonction [`loadTable`](https://processing.org/reference/loadTable_.html), avec, en paramètre, une [chaîne de caractères](cours/10-strings.md) contenant le chemin vers le fichier. La logique de chargement est similaire à celle des [images](cours/14-images-pixels.md) ; le nom du fichier peut être un chemin relatif au sketch processing ou absolu, et on ne peut pas charger des tables avant le `setup`, s'il y a en un.

```java
Table table = loadTable("data.csv");
```

Lorsque l'on charge une table depuis un fichier, il est possible que le fichier ait une première ligne représentant le nom des colonnes (comme dans un tableau Excel). Processing ne pouvant pas le deviner, il faut, quand c'est le cas, spécifier qu'on charge un fichier dont la première ligne contient les en-têtes, en rajoutant en paramètre la valeur `"header"`.

```java
Table table = loadTable("data.csv", "header");
```

### Création

Pour créer une nouvelle table, vide, il suffit simplement d'appeler le constructeur de la classe [`Table`](https://processing.org/reference/Table.html) avec le mot clé `new`.

```java
Table newTable = new Table();
```

### Sauvegarde

Pour sauvegarder le contenu d'une table dans un fichier, il faut appeler la fonction [`saveTable`](https://processing.org/reference/saveTable_.html) avec en paramètres la table à sauvegarder, et le nom/chemin du fichier où la sauvegarder.

```java
Table table = loadTable("data.csv");
saveTable(table, "renamedData.csv");
```

## Manipulation

### Lecture
La classe [`Table`](https://processing.org/reference/Table.html) a différentes méthodes qui permettent de lire son contenu ou les informations liées :
- [`getRowCount()`](https://processing.org/reference/Table_getRowCount_.html) renvoie le nombre de lignes, sans inclure la ligne d'en-tête s'il y en a une, présentes dans la table.
- [`getColumnCount()`](https://processing.org/reference/Table_getColumnCount_.html) renvoie le nombre de colonnes dans la table.
- [`getString(i, j)`](https://processing.org/reference/Table_getString_.html) ou [`getString(i, name)`](https://processing.org/reference/Table_getString_.html) renvoie la valeur contenue dans la cellule en ligne *i*, colonne *j* (indice) ou *name* (en-tête) comme [`String`](cours/10-strings).
- [`getFloat(i, j)`](https://processing.org/reference/Table_getFloat_.html)ou [`getFloat(i, name)`](https://processing.org/reference/Table_getFloat_.html) renvoie la valeur contenue dans la cellule en ligne *i*, colonne *j* (indice) ou *name* (en-tête) convertie en `float`.
- [`getInt(i, j)`](https://processing.org/reference/Table_getInt_.html) ou [`getInt(i, name)`](https://processing.org/reference/Table_getInt_.html) renvoie la valeur contenue dans la cellule en ligne *i*, colonne *j* (indice) ou *name* (en-tête) convertie en `int`.

Soit le fichier `data.csv`

```csv
c1,c2
a,1
b,2
c,3
```

```java
Table table = loadTable("data.csv", "header");
println(table.getRowCount()); // Affiche 3
println(table.getColumnCount()); // Affiche 2
println(table.getString(0, 0)); // Affiche a
println(table.getInt(1, "c2")); // Affiche 2
```

### Ecriture

Pour modifier directement la valeur de cellules existantes dans la table, on peut utiliser les méthodes :
- [`setString(i, j, s)`](https://processing.org/reference/Table_setString_.html) ou [`setString(i, name, s)`](https://processing.org/reference/Table_setString_.html) met la chaîne de caractères *s* dans la cellule en ligne *i*, colonne *j* (indice) ou *name* (en-tête).
- [`setFloat(i, j, f)`](https://processing.org/reference/Table_setFloat_.html)ou [`setFloat(i, name, f)`](https://processing.org/reference/Table_setFloat_.html) met le nombre flottant *f* dans la cellule en ligne *i*, colonne *j* (indice) ou *name* (en-tête).
- [`setInt(i, j, v)`](https://processing.org/reference/Table_setInt_.html) ou [`setInt(i, name, v)`](https://processing.org/reference/Table_setInt_.html) met la valeur entière *k* dans la cellule en ligne *i*, colonne *j* (indice) ou *name* (en-tête).

Soit le fichier `data.csv`

```csv
c1,c2
a,1
b,2
c,3
```

```java
Table table = loadTable("data.csv", "header");
table.setString(0, 0, "aa");
table.setInt(1, "c2", 22);
saveTable(table, "data.csv");
```

Le fichier `data.csv` contient maintenant

```csv
c1,c2
aa,1
b,22
c,3
```

### `TableRow`

On peut accéder directement aux cellules de la table depuis l'objet table, de type [`Table`](https://processing.org/reference/Table.html), mais on peut également passer par l'étape intermédiaire qui consiste à récupérer l'objet représentant une ligne en appelant la méthode [`getRow(i)`](https://processing.org/reference/Table_getRow_.html) avec l'indice de la ligne voulue. Ces objets "lignes" sont de type [`TableRow`](https://processing.org/reference/TableRow.html), et on peut les manipuler de façon similaire à la table :
- [`getColumnCount()`](https://processing.org/reference/TableRow_getColumnCount_.html) renvoie le nombre de colonnes dans la ligne.
- [`getColumnTitle(j)`](https://processing.org/reference/TableRow_getColumnTitle_.html) renvoie l'en-tête de la colonne d'indice *j*
- [`getString(j)`](https://processing.org/reference/TableRow_getString_.html) ou [`getString(name)`](https://processing.org/reference/TableRow_getString_.html) renvoie la valeur contenue dans la colonne *j* (indice) ou *name* (en-tête) de la ligne, comme [`String`](cours/10-strings).
- [`getFloat(j)`](https://processing.org/reference/TableRow_getFloat_.html)ou [`getFloat(name)`](https://processing.org/reference/TableRow_getFloat_.html) renvoie la valeur contenue dans la colonne *j* (indice) ou *name* (en-tête) de la ligne, convertie en `float`.
- [`getInt(j)`](https://processing.org/reference/TableRow_getInt_.html) ou [`getInt(name)`](https://processing.org/reference/TableRow_getInt_.html) renvoie la valeur contenue dans la colonne *j* (indice) ou *name* (en-tête) de la ligne, convertie en `int`.
- [`setString(j, s)`](https://processing.org/reference/TableRow_setString_.html) ou [`setString(name, s)`](https://processing.org/reference/TableRow_setString_.html) met la chaîne de caractères *s* dans la colonne *j* (indice) ou *name* (en-tête) de la ligne.
- [`setFloat(j, f)`](https://processing.org/reference/TableRow_setFloat_.html)ou [`setFloat(name, f)`](https://processing.org/reference/TableRow_setFloat_.html) met le nombre flottant *f* dans la colonne *j* (indice) ou *name* (en-tête) de la ligne.
- [`setInt(j, v)`](https://processing.org/reference/TableRow_setInt_.html) ou [`setInt(name, v)`](https://processing.org/reference/TableRow_setInt_.html) met la valeur entière *k* dans la colonne *j* (indice) ou *name* (en-tête) de la ligne.

```csv
c1,c2
a,1
b,2
c,3
```

```java
Table table = loadTable("data.csv", "header");
TableRow row1 = table.getRow(0);
TableRow row2 = table.getRow(1);
row1.setString(0, "aa");
row2.setInt("c2", 22);
saveTable(table, "data.csv");
```

Le fichier `data.csv` contient maintenant

```csv
c1,c2
aa,1
b,22
c,3
```

### Structure

Pour modifier la structure d'une table, on peut utiliser les méthodes :
- [`addRow()`](https://processing.org/reference/Table_addRow_.html) ajoute une nouvelle ligne (vide), tout en bas de la table. La ligne créée ([`TableRow`](https://processing.org/reference/TableRow.html)) est renvoyée. Si on passe une autre [`TableRow`](https://processing.org/reference/TableRow.html) en paramètre, la nouvelle ligne créée contiendra alors une copie des données de la ligne passée en paramètre.
- [`removeRow(i)`](https://processing.org/reference/Table_removeRow_.html) supprime la ligne à l'indice *i* dans la table.
- [`addColumn()`](https://processing.org/reference/Table_addColumn_.html) ajoute une nouvelle colonne, vide pour chaque ligne, à droite de la table. Si on passe en paramètre le nom de la colonne, il s'agira de l'en-tête qui pourra ensuite être utilisée pour plus facilement accéder aux éléments de cette colonne. On peut éventuellement passer un deuxième paramètre correspondant au type de données attendu dans la colonne ; `Table.INT`, `Table.FLOAT` et `Table.STRING` (défaut).
- [`removeColumn(j)`](https://processing.org/reference/Table_removeColumn_.html) ou [`removeColumn(name)`](https://processing.org/reference/Table_removeColumn_.html) supprime la colonne à l'indice *j* ou avec le nom *name* spécifié en paramètre. 

```java
Table table = new Table();
table.addColumn("a"); // On ajoute une colonne a
table.addColumn("b"); // On ajoute une colonne b
table.addColumn("c"); // On ajoute une colonne c
table.removeColumn("a"); // On retire la colonne a
table.removeColumn(1); // On retire la deuxième colonne, c
table.addColumn("d"); // On ajoute la colonne d

// On a donc une table avec deux colonnes, b et d

TableRow firstRow = table.addRow(); // Première ligne
firstRow.setString("b", "test");
firstRow.setInt("d", 1);

table.addRow(firstRow); // On rajoute une deuxième ligne qui contient les mêmes valeurs que la première
table.setInt(1, "d", 2); // On met la valeur 2 dans la colonne d de la deuxième ligne

saveTable(table, "random.csv");
```

On obtient alors un fichier `random.csv` contenant :

```csv
b,d
test,1
test,2
```


### Tri

On peut facilement trier une table en appelant la méthode [`sort`](https://processing.org/reference/Table_sort_.html) avec en paramètre l'indice ou le nom de la colonne à trier. Les lignes de la table seront alors réorganisées selon l'ordre croissant des valeurs apparaissant dans cette colonne.

Pour des tris plus complexes qui demandent de comparer plusieurs colonnes, il faudra définir la comparaison adéquate et implémenter un algorithme de tri.

```java
void setup() {
  Table table = loadTable("data.csv");

  // Bubble sort
  for (int k = table.getRowCount()-1; k > 0; k--) {
    for (int i = 0; i < k; i++) {
      TableRow row1 = table.getRow(i);
      TableRow row2 = table.getRow(i + 1);
      if (compare(row1, row2) > 0) {
        // La ligne i devrait être après la ligne i + 1
        // On les échange
        swapRows(table, i, i + 1);
      }
    }
  }
}

int compare(TableRow row1, TableRow row2) {
  // Implémenter la comparaison
  return 0;
}

void swapRows(Table t, int i1, int i2) { 
  for (int j = 0; j < t.getColumnCount(); j++) { 
    String swapped = t.getString(i1, j); 
    t.setString(i1, j, t.getString(i2, j)); 
    t.setString(i2, j, swapped); 
  }
}
```