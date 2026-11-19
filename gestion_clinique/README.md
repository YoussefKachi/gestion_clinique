# Gestion d'une clinique (PHP natif)

Projet universitaire : application web de gestion d'une clinique (patients, consultations, utilisateurs).

## 1. Technologies utilisées

- PHP natif (sans framework)
- HTML5, CSS3, JavaScript natif
- MySQL avec PDO (requêtes préparées)
- Sessions PHP
- XAMPP, VS Code, phpMyAdmin

Aucun framework ni bibliothèque externe (pas de Laravel, Bootstrap, React, etc.).

## 2. Installation de XAMPP

1. Télécharger XAMPP sur https://www.apachefriends.org et l'installer.
2. Ouvrir le **XAMPP Control Panel**.
3. Cliquer sur **Start** pour **Apache** et pour **MySQL**.

## 3. Installation du projet

1. Copier le dossier `gestion_clinique` dans le dossier `htdocs` de XAMPP
   (par exemple `C:\xampp\htdocs\gestion_clinique`).
2. Le nom du dossier doit rester `gestion_clinique`.
   Si vous le renommez, modifiez aussi `BASE_URL` dans `config/database.php`.

## 4. Création de la base de données

1. Ouvrir http://localhost/phpmyadmin
2. Cliquer sur l'onglet **Importer**.
3. Choisir le fichier `database.sql` du projet, puis cliquer sur **Importer**.

Le fichier crée la base `gestion_clinique`, les tables et des données de test.
(Attention : il supprime et recrée les tables si elles existent déjà.)

Si votre MySQL a un mot de passe pour `root`, modifiez-le dans `config/database.php`.

## 5. Lancer le projet

Ouvrir dans le navigateur : **http://localhost/gestion_clinique/**

## 6. Comptes de démonstration

| Rôle       | Email                   | Mot de passe  |
|------------|-------------------------|---------------|
| Médecin    | medecin@clinique.com    | Medecin123    |
| Assistante | assistante@clinique.com | Assistante123 |

## 7. Droits des utilisateurs

| Action                        | Visiteur | Assistante | Médecin |
|-------------------------------|:--------:|:----------:|:-------:|
| Inscription / connexion       |    oui   |     -      |    -    |
| Consulter les patients        |    -     |    oui     |   oui   |
| Ajouter/modifier/supprimer patients |  - |    oui     |    -    |
| Consulter les consultations   |    -     |    oui     |   oui   |
| Ajouter/modifier/supprimer consultations | - |   -     |   oui   |
| Gérer les utilisateurs        |    -     |     -      |   oui   |

L'inscription publique crée toujours un compte **assistante**.
Seul un médecin peut créer un autre compte médecin (menu Utilisateurs).

## 8. Organisation des dossiers

```
gestion_clinique/
├── config/database.php        Connexion PDO + session
├── includes/
│   ├── header.php             Début des pages HTML
│   ├── navbar.php             Sidebar + barre du haut (menu selon le rôle)
│   ├── footer.php             Fin des pages HTML
│   ├── auth.php               Vérification de connexion et des rôles
│   └── functions.php          Fonctions utiles (CSRF, messages, validation)
├── auth/                      inscription, connexion, déconnexion
├── patients/                  CRUD des patients
├── consultations/             CRUD des consultations
├── utilisateurs/              CRUD des utilisateurs
├── assets/
│   ├── css/style.css          Design
│   ├── js/script.js           Confirmation de suppression, menu mobile
│   └── images/
├── index.php                  Redirection selon la connexion
├── accueil.php                Tableau de bord avec statistiques
├── database.sql               Base de données
├── README.md
└── .gitignore
```

## 9. Fonctionnalités principales

- Inscription, connexion et déconnexion (mots de passe avec `password_hash` / `password_verify`)
- Tableau de bord avec statistiques et dernières consultations (requête JOIN)
- CRUD des patients, des consultations et des utilisateurs
- Relations SQL : `consultations.patient_id` → `patients.id` et `consultations.medecin_id` → `utilisateurs.id`
- Menus différents selon le rôle et pages protégées par rôle
- Sécurité : requêtes préparées PDO, `htmlspecialchars`, jeton CSRF, suppression en POST avec confirmation
- Design responsive (bleu foncé, blanc, bleu clair)

## 10. Remarques

- Un patient qui a des consultations ne peut pas être supprimé (clé étrangère).
- Un médecin qui a des consultations ne peut pas être supprimé.
- Un utilisateur ne peut pas supprimer son propre compte.
