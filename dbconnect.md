# **Cours 8 : Connexion PHP et MySQL**

## **Objectif du cours**  
Apprendre à connecter une application PHP à une base de données MySQL à l'aide de PDO ou mysqli, et exécuter des requêtes SQL pour manipuler les données dynamiquement.

---

## **Plan du cours**

### 1. **Introduction : Pourquoi connecter PHP à MySQL ?**  
- Permet de créer des applications web dynamiques.  
- Stockage et gestion des données de manière centralisée.  
- PHP dispose de deux principales extensions pour se connecter à MySQL :  
  - **`mysqli`** (MySQL Improved).  
  - **`PDO`** (PHP Data Objects) : plus flexible et supporte plusieurs bases de données.

---

### 2. **Connexion à une base de données avec `mysqli`**  

#### **Syntaxe de base avec `mysqli` :**
```php
$host = 'localhost';
$username = 'root';
$password = '';
$dbname = 'ma_base';

$conn = new mysqli($host, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Erreur de connexion : " . $conn->connect_error);
}
echo "Connexion réussie !";
```

#### **Points importants :**
- Utilisez `$conn->connect_error` pour vérifier les erreurs de connexion.  
- Toujours fermer la connexion après utilisation :  
  ```php
  $conn->close();
  ```

---

### 3. **Connexion à une base de données avec `PDO`**  

#### **Avantages de PDO :**
- Supporte plusieurs types de bases de données.  
- Requêtes préparées pour sécuriser les données.  

#### **Syntaxe de base avec PDO :**
```php
$host = 'localhost';
$dbname = 'ma_base';
$username = 'root';
$password = '';

try {
    $pdo = new PDO("mysql:host=$host;dbname=$dbname", $username, $password);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connexion réussie !";
} catch (PDOException $e) {
    die("Erreur de connexion : " . $e->getMessage());
}
```

#### **Options importantes de PDO :**
- Gestion des erreurs avec `PDO::ERRMODE_EXCEPTION`.  
- Fermeture automatique de la connexion lorsque le script se termine.

---

### 4. **Exécution de requêtes SQL avec `mysqli`**  

#### **Requêtes simples :**

##### **Insertion de données :**
```php
$sql = "INSERT INTO utilisateurs (nom, email) VALUES ('Alice', 'alice@example.com')";
if ($conn->query($sql) === TRUE) {
    echo "Nouvel enregistrement ajouté avec succès.";
} else {
    echo "Erreur : " . $conn->error;
}
```

##### **Lecture des données :**
```php
$sql = "SELECT * FROM utilisateurs";
$result = $conn->query($sql);

while ($row = $result->fetch_assoc()) {
    echo $row['nom'] . " - " . $row['email'] . "<br>";
}
```

---

### 5. **Exécution de requêtes SQL avec `PDO`**  

#### **Requêtes préparées :**

##### Exemple d'insertion avec requêtes préparées :
```php
$stmt = $pdo->prepare("INSERT INTO utilisateurs (nom, email) VALUES (:nom, :email)");
$stmt->execute([
    'nom' => 'Alice',
    'email' => 'alice@example.com'
]);
echo "Données insérées avec succès.";
```

##### Exemple de récupération des données :
```php
$stmt = $pdo->prepare("SELECT * FROM utilisateurs WHERE nom = :nom");
$stmt->execute(['nom' => 'Alice']);
$result = $stmt->fetchAll();

foreach ($result as $row) {
    echo $row['nom'] . " - " . $row['email'] . "<br>";
}
```

---

### 6. **Comparaison entre `mysqli` et `PDO`**  

| **Caractéristique**      | **`mysqli`**            | **PDO**                   |
|---------------------------|-------------------------|---------------------------|
| Support des bases de données | MySQL uniquement       | Supporte plusieurs bases  |
| Sécurité (requêtes préparées) | Oui                   | Oui                       |
| Flexibilité               | Moins flexible          | Très flexible             |

---

## **Exercices pratiques**

1. Créer une base de données `gestion_utilisateurs` avec une table `utilisateurs` (id, nom, email).  
2. Écrire un script PHP qui :  
   - Se connecte à la base de données.  
   - Ajoute un utilisateur dans la table avec un formulaire HTML.  
   - Affiche tous les utilisateurs dans un tableau HTML.  
3. Réaliser les mêmes tâches avec `mysqli` et PDO.

---

## **Résumé du cours**

Ce cours a montré comment connecter une application PHP à une base de données MySQL en utilisant `mysqli` et PDO. Les étudiants ont appris à exécuter des requêtes SQL pour insérer, lire, et manipuler les données tout en découvrant l'importance des requêtes préparées pour la sécurité.

---

## **À retenir**

1. **`mysqli` et PDO** : Deux options principales pour interagir avec MySQL.  
2. **Requêtes SQL dynamiques** : Toujours valider et sécuriser les données d'entrée pour éviter les failles.  
3. **Requêtes préparées** : Une bonne pratique pour éviter les injections SQL.

---