# **Cours 7 : Bases de données et SQL avec MySQL**

## **Objectif du cours**
Découvrir les bases de MySQL et apprendre à utiliser les commandes fondamentales pour créer et manipuler des bases de données, des tables et des données.

---

## **Plan du cours**

### **1. Introduction à MySQL (30 minutes)**

#### **Qu'est-ce qu'une base de données ?**
- **Définition** : Les bases de données sont des systèmes qui permettent de stocker, gérer et manipuler des données de manière structurée. Elles jouent un rôle essentiel dans le développement d'applications modernes, car elles permettent de conserver des informations accessibles et organisées.  
- **Importance** : Les bases de données jouent un rôle crucial dans les applications web modernes.

#### **Présentation de MySQL :**
- Base de données relationnelle.
- **Avantages** :
  - Rapide.
  - Open source.
  - Largement utilisé.

#### **Outils pour interagir avec MySQL :**
- Ligne de commande MySQL.
- Interfaces graphiques : 
  - phpMyAdmin.
  - MySQL Workbench.

---

### **2. Création d'une base de données et de tables (30 minutes)**

#### **Syntaxe pour créer une base de données :**
```sql
CREATE DATABASE nom_base;
```

#### **Utilisation de la base de données :**
```sql
USE nom_base;
```

#### **Création d'une table :**
```sql
CREATE TABLE utilisateurs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(50),
    email VARCHAR(100),
    date_inscription DATE
);
```

#### **Explication des types de données :**
- `INT`
- `VARCHAR`
- `DATE`

---

### **3. Commandes de base pour manipuler les données (1 heure)**

#### **Insertion de données dans une table :**
```sql
INSERT INTO utilisateurs (nom, email, date_inscription) 
VALUES ('Alice', 'alice@example.com', '2025-01-22');
```

#### **Lecture des données (`SELECT`) :**
- Sélectionner toutes les colonnes :
  ```sql
  SELECT * FROM utilisateurs;
  ```
- Sélectionner des colonnes spécifiques :
  ```sql
  SELECT nom, email FROM utilisateurs;
  ```
- Ajout de conditions avec `WHERE` :
  ```sql
  SELECT * FROM utilisateurs WHERE nom = 'Alice';
  ```

#### **Mise à jour des données (`UPDATE`) :**
```sql
UPDATE utilisateurs 
SET email = 'alice.new@example.com' 
WHERE nom = 'Alice';
```

#### **Suppression de données (`DELETE`) :**
```sql
DELETE FROM utilisateurs WHERE nom = 'Alice';
```

---

### **4. Exemples pratiques (30 minutes)**

#### **Création d'une base de données `bibliothèque` :**
- Ajout d'une table `livres` :
  ```sql
  CREATE TABLE livres (
      id INT AUTO_INCREMENT PRIMARY KEY,
      titre VARCHAR(100),
      auteur VARCHAR(50),
      annee_publication INT
  );
  ```
- Insérer des données dans `livres` et effectuer des requêtes `SELECT`.
- Mettre à jour les informations d’un livre.
- Supprimer un livre spécifique.

---

### **5. Exercices (30 minutes)**

1. Créer une base de données pour un magasin en ligne avec une table `produits` (id, nom, prix, quantité).  
2. Insérer plusieurs produits dans la table.  
3. Récupérer tous les produits dont le prix est supérieur à 50.  
4. Modifier la quantité d’un produit spécifique.  
5. Supprimer un produit en fonction de son ID.

---

## **Résumé du cours 7**
Dans ce cours, les étudiants ont appris les bases de MySQL, y compris :  
- La création et l’utilisation d’une base de données.  
- La définition de tables.  
- L’exécution des commandes SQL fondamentales (`CREATE`, `SELECT`, `INSERT`, `UPDATE`, `DELETE`).  

Ces compétences sont essentielles pour gérer les données dans une application web dynamique.

---

## **À retenir**
1. **Commandes SQL de base** :
   - `CREATE` : Créer des bases de données et des tables.
   - `SELECT` : Lire les données.
   - `INSERT` : Ajouter de nouvelles données.
   - `UPDATE` : Modifier les données existantes.
   - `DELETE` : Supprimer des données.
2. **Bonne pratique** :
   - Toujours utiliser des conditions avec `WHERE` pour éviter les erreurs dans les requêtes `UPDATE` et `DELETE`.