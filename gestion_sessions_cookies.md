# Cours 5 : Gestion des sessions et des cookies avec PHP

## Objectif du cours

Ce cours a pour objectif de vous apprendre à utiliser les **sessions** et les **cookies** en PHP pour gérer les données des utilisateurs, maintenir des connexions persistantes et personnaliser leur expérience sur un site web.

---

## 1. Introduction aux sessions et cookies

### **Qu'est-ce qu'une session ?**  
Une **session** permet de stocker temporairement des informations sur un utilisateur côté **serveur**. Les sessions sont souvent utilisées pour gérer des **authentifications** ou conserver un **panier d'achat**.

**Exemple :**  
Lorsqu'un utilisateur se connecte à un site, ses informations sont enregistrées dans une session.

### **Qu'est-ce qu'un cookie ?**  
Un **cookie** est un petit fichier stocké sur l'ordinateur de l'utilisateur. Il est souvent utilisé pour **mémoriser des préférences** ou **suivre un utilisateur sur plusieurs visites**.

**Exemple :**  
Un site peut mémoriser la langue préférée d'un utilisateur grâce à un cookie.

### **Différences entre sessions et cookies**  

| Critère       | Sessions | Cookies |
|--------------|---------|---------|
| Stockage    | Côté serveur | Côté client (navigateur) |
| Durée       | Jusqu'à fermeture du navigateur (ou délai configuré) | Expiration définie (jours, mois, années) |
| Sécurité    | Plus sécurisé (données non accessibles par l'utilisateur) | Moins sécurisé (données accessibles en clair) |
| Utilisation | Authentification, panier d'achat | Préférences, suivi des visiteurs |

---

## 2. Les sessions en PHP

### **Démarrer une session**  
Avant d'utiliser une session, il faut la démarrer avec `session_start()`.

```php
<?php
session_start(); // Démarrage de la session
?>
```

### **Stocker et récupérer des données dans une session**  

```php
<?php
session_start();
$_SESSION['nom_utilisateur'] = 'AlphaDiop';

echo 'Bonjour ' . $_SESSION['nom_utilisateur']; // Affiche "Bonjour AlphaDiop"
?>
```

### **Détruire une session**  

```php
<?php
session_start();
session_destroy(); // Supprime toutes les données de session
?>
```

### **Exemple pratique : Connexion avec sessions**  

```php
<?php
session_start();

if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $_SESSION['utilisateur'] = $_POST['nom']; // Stocker le nom dans la session
    echo "Bienvenue, " . $_SESSION['utilisateur'];
}
?>

<form method="post">
    <input type="text" name="nom" placeholder="Entrez votre nom" required>
    <button type="submit">Se connecter</button>
</form>
```

---

## 3. Les cookies en PHP

### **Créer un cookie**  

```php
<?php
setcookie('langue', 'francais', time() + 3600 * 24 * 30); // Expire après 30 jours
?>
```

### **Lire un cookie**  

```php
<?php
if (isset($_COOKIE['langue'])) {
    echo "Langue sélectionnée : " . $_COOKIE['langue'];
} else {
    echo "Aucune langue sélectionnée.";
}
?>
```

### **Supprimer un cookie**  

```php
<?php
setcookie('langue', '', time() - 3600); // Expire dans le passé, donc supprimé
?>
```

### **Exemple pratique : Mémoriser le thème du site**  

```php
<?php
if (isset($_POST['theme'])) {
    setcookie('theme', $_POST['theme'], time() + 3600 * 24 * 30); // 30 jours
}

$theme = isset($_COOKIE['theme']) ? $_COOKIE['theme'] : 'clair';
?>

<form method="post">
    <select name="theme">
        <option value="clair" <?= $theme == 'clair' ? 'selected' : '' ?>>Clair</option>
        <option value="sombre" <?= $theme == 'sombre' ? 'selected' : '' ?>>Sombre</option>
    </select>
    <button type="submit">Sauvegarder</button>
</form>

<p>Thème actuel : <?= $theme ?></p>
```

---

## 4. Sécurité des sessions et cookies

### **Sécuriser les sessions**  

- **Générer un ID de session aléatoire :**  
  ```php
  session_start();
  session_regenerate_id(true);
  ```

- **Utiliser HTTPS pour éviter le vol de session**  

### **Sécuriser les cookies**  

- **Utiliser les options `secure` et `HttpOnly` :**  
  ```php
  setcookie('auth', 'valeur_secrete', time() + 3600, "/", "", true, true);
  ```

- **Protéger contre les attaques XSS et CSRF**  
  - **XSS** : Ne jamais stocker de données sensibles dans les cookies.
  - **CSRF** : Utiliser des jetons CSRF pour les formulaires sensibles.

---

## 5. Exercices pratiques

1. **Créer une application avec sessions :**  
   - L’utilisateur entre son nom dans un formulaire.  
   - Son nom est stocké dans une session.  
   - Afficher "Bienvenue, [nom]" après soumission.

2. **Créer une application avec cookies :**  
   - L’utilisateur choisit une langue (français/anglais).  
   - Sa préférence est enregistrée dans un cookie.  
   - Lorsqu'il revient sur le site, afficher la langue choisie.

---

## Résumé du cours

- **Les sessions** stockent les données **côté serveur** et sont utilisées pour des données temporaires ou sensibles.  
- **Les cookies** stockent les données **côté client** et permettent de sauvegarder des préférences à long terme.  
- **La sécurité** des sessions et cookies est essentielle pour éviter les attaques courantes.

