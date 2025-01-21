### **Cours 3 : Premières pages dynamiques avec PHP**

#### **Objectif du cours**

Apprendre à créer des pages web dynamiques en PHP en utilisant des inclusions de fichiers et le traitement de formulaires HTML avec les superglobales `$_GET` et `$_POST`.

---

### **Plan du cours**

#### 1. **Inclusion de fichiers en PHP**

##### **Introduction**

L’inclusion de fichiers est une pratique essentielle pour organiser le code et éviter les répétitions. Elle permet de diviser une application en plusieurs modules réutilisables, facilitant ainsi la maintenance et la lisibilité.

##### **Syntaxe et exemples**

- `include` : Inclut un fichier et continue l’exécution même si le fichier est introuvable.
- `require` : Similaire à `include`, mais arrête l’exécution si le fichier est introuvable.
- `include_once` et `require_once` : Incluent un fichier une seule fois, même si l’instruction est appelée plusieurs fois.

**Exemple : Inclusion d'un fichier commun**

1. Créez un fichier `header.php` avec le contenu suivant :
   ```php
   <!DOCTYPE html>
   <html lang="fr">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Site Dynamique</title>
   </head>
   <body>
       <header>
           <h1>Bienvenue sur mon site</h1>
       </header>
   ```
2. Incluez ce fichier dans d'autres fichiers avec :
   ```php
   <?php include 'header.php'; ?>
   <p>Contenu de la page principale.</p>
   ```

---

#### 2. **Introduction aux formulaires HTML et PHP**

##### **Créer un formulaire HTML simple**

Un formulaire permet de collecter des données saisies par un utilisateur. Exemple de formulaire simple :

```html
<form action="traitement.php" method="post">
    <label for="nom">Nom :</label>
    <input type="text" id="nom" name="nom">
    <button type="submit">Envoyer</button>
</form>
```

##### **Différence entre `GET` et `POST`**

- **GET** : Les données sont visibles dans l’URL. Utilisez-le pour des requêtes non sensibles ou pour passer des paramètres.
- **POST** : Les données sont envoyées dans le corps de la requête. Privilégiez-le pour des informations sensibles.

##### **Superglobales `$_GET` et `$_POST`**

Ces variables permettent d’accéder aux données envoyées par un formulaire.

- Exemple d’utilisation de `$_POST` :
  ```php
  <?php
  if ($_SERVER['REQUEST_METHOD'] === 'POST') {
      $nom = $_POST['nom'] ?? '';
      echo "Bonjour, " . htmlspecialchars($nom);
  }
  ?>
  ```

---

#### 3. **Validation et nettoyage des données (30 minutes)**

##### **Pourquoi valider et nettoyer les données ?**

Les données utilisateur peuvent contenir des caractères dangereux ou non attendus. Valider et nettoyer ces données est essentiel pour garantir la sécurité et le bon fonctionnement de l’application.

##### **Protéger contre les failles XSS**

Utilisez `htmlspecialchars` pour convertir les caractères spéciaux en entités HTML.

```php
<?php
$nom = htmlspecialchars($_POST['nom'] ?? '');
echo "Bonjour, " . $nom;
?>
```

##### **Filtrage avec `filter_input` et `filter_var`**

Ces fonctions permettent de valider et nettoyer des données.

```php
<?php
$email = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
if ($email) {
    echo "Email valide : " . $email;
} else {
    echo "Email invalide";
}
?>
```

---

#### 4. **Exemples pratiques**

##### **Exemple 1 : Affichage d'un message personnalisé**

1. Créez un formulaire avec un champ pour le nom :
   ```html
   <form action="message.php" method="post">
       <label for="nom">Nom :</label>
       <input type="text" id="nom" name="nom">
       <button type="submit">Envoyer</button>
   </form>
   ```
2. Traitez les données dans `message.php` :
   ```php
   <?php
   $nom = htmlspecialchars($_POST['nom'] ?? '');
   echo "Bonjour, " . $nom;
   ?>
   ```

##### **Exemple 2 : Calculatrice simple**

1. Formulaire HTML :
   ```html
   <form action="calcul.php" method="post">
       <label for="a">Nombre 1 :</label>
       <input type="number" id="a" name="a">
       <label for="b">Nombre 2 :</label>
       <input type="number" id="b" name="b">
       <button type="submit">Calculer</button>
   </form>
   ```
2. Script PHP :
   ```php
   <?php
   $a = (int) ($_POST['a'] ?? 0);
   $b = (int) ($_POST['b'] ?? 0);
   echo "La somme est : " . ($a + $b);
   ?>
   ```

---

#### 5. **Exercices**

##### **Exercice 1 : Choisir une couleur**

Créez un formulaire permettant de choisir une couleur et d’afficher un message dans cette couleur.

##### **Exercice 2 : Formulaire de contact**

Créez un formulaire avec les champs suivants : nom, email, et message. Affichez les données saisies sur une autre page.

---

### **Résumé du cours 3**

Dans ce cours, les étudiants ont appris à structurer leurs projets PHP grâce aux inclusions de fichiers, facilitant la réutilisation et l’organisation du code. Ils ont également découvert comment créer et traiter des formulaires HTML en PHP à l’aide des superglobales `$_GET` et `$_POST`. Les notions de validation et de nettoyage des données ont été abordées pour garantir la sécurité des applications.

---

### **À retenir**

1. **Inclusion de fichiers** : Utiliser `include` ou `require` pour organiser le code et éviter les répétitions.
2. **Traitement des formulaires** : Utiliser `$_GET` pour des requêtes visibles et `$_POST` pour des données sensibles.
3. **Validation et sécurité** : Toujours valider et nettoyer les données utilisateurs avant de les utiliser ou les afficher.
