<<<<<<< HEAD
# LAB 9 — Consommer un Web Service PHP 8 depuis Android avec Volley

## 📋 Objectifs

- Créer une base de données MySQL pour gérer les étudiants
- Développer un Web Service PHP capable d'ajouter et de renvoyer les données en JSON
- Construire une application Android qui consomme ce service via **Volley**
- Utiliser **Gson** pour parser la réponse JSON et afficher les résultats

---

## 🏗️ Architecture du projet

```
lab1-android/
├── app/                          # Application Android
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/example/hellotoast/
│       │   ├── AddEtudiant.java          # Activité : formulaire d'ajout
│       │   ├── ListEtudiantActivity.java # Activité : liste des étudiants
│       │   └── beans/
│       │       └── Etudiant.java         # Classe modèle
│       └── res/
│           ├── layout/
│           │   ├── activity_add_etudiant.xml
│           │   ├── activity_list_etudiant.xml
│           │   └── item_etudiant.xml
│           ├── values/
│           │   ├── strings.xml
│           │   ├── colors.xml
│           │   └── themes.xml
│           └── xml/
│               └── network_security_config.xml
├── php/                          # Backend PHP (à copier dans XAMPP)
│   ├── classes/Etudiant.php
│   ├── connexion/Connexion.php
│   ├── dao/IDao.php
│   ├── service/EtudiantService.php
│   ├── ws/
│   │   ├── createEtudiant.php    # POST : ajouter un étudiant
│   │   └── loadEtudiant.php      # GET  : charger tous les étudiants
│   └── sql/
│       └── setup.sql             # Script de création de la BDD
└── README.md
```

---

## 🚀 Mise en place

### Partie 1 — Base de données MySQL

1. Démarrer **XAMPP** (Apache + MySQL)
2. Ouvrir [http://localhost/phpmyadmin](http://localhost/phpmyadmin)
3. Exécuter le script SQL situé dans `php/sql/setup.sql` :

```sql
CREATE DATABASE IF NOT EXISTS school1;
USE school1;

CREATE TABLE IF NOT EXISTS Etudiant (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nom VARCHAR(50),
  prenom VARCHAR(50),
  ville VARCHAR(50),
  sexe VARCHAR(10)
);

INSERT INTO Etudiant (nom, prenom, ville, sexe)
VALUES ('Lachgar', 'Mohamed', 'Rabat', 'homme'),
       ('Safi', 'Amine', 'Marrakech', 'homme');
```

### Partie 2 — Déploiement du Web Service PHP

1. Copier le dossier `php/` dans `C:\xampp\htdocs\projet` :
   ```
   C:\xampp\htdocs\projet\
   ├── classes/
   ├── connexion/
   ├── dao/
   ├── service/
   └── ws/
   ```

2. Tester les endpoints :
   - **GET** : `http://localhost/projet/ws/loadEtudiant.php`
   - **POST** : `http://localhost/projet/ws/createEtudiant.php` (avec les paramètres `nom`, `prenom`, `ville`, `sexe`)

### Partie 3 — Application Android

1. Ouvrir le projet dans **Android Studio**
2. Synchroniser Gradle (`Sync Now`)
3. Lancer l'application sur l'émulateur Android

> **Note** : L'émulateur Android accède à `localhost` de la machine hôte via l'adresse `10.0.2.2`. C'est pourquoi les URLs dans le code Java utilisent `http://10.0.2.2/projet/ws/...`.

---

## 📱 Fonctionnalités de l'application

| Écran | Description |
|-------|-------------|
| **AddEtudiant** | Formulaire avec Nom, Prénom, Ville (Spinner), Sexe (RadioButton) et bouton ADD. Envoie une requête POST via Volley. |
| **ListEtudiantActivity** | Affiche la liste complète des étudiants depuis le serveur via une requête GET. Clic sur un élément = popup avec détails. |

---

## 🔧 Technologies utilisées

| Composant | Technologie |
|-----------|-------------|
| Backend | PHP 8 + PDO + MySQL |
| Android HTTP | Volley 1.2.1 |
| JSON Parsing | Gson 2.10.1 |
| UI | Material Components |
| Architecture | MVC (PHP) + Activity-based (Android) |

---

## ⚠️ Configuration réseau (Android 9+)

Le fichier `res/xml/network_security_config.xml` autorise le trafic HTTP clair vers `10.0.2.2` (localhost de l'émulateur). C'est indispensable car Android 9+ bloque les connexions HTTP non sécurisées par défaut.

---

## 🧪 Tester avec Postman / Advanced REST Client

### Ajouter un étudiant (POST)
- **URL** : `http://localhost/projet/ws/createEtudiant.php`
- **Method** : POST
- **Body** (x-www-form-urlencoded) :
  - `nom` = Dupont
  - `prenom` = Sara
  - `ville` = Casablanca
  - `sexe` = femme

### Charger les étudiants (GET)
- **URL** : `http://localhost/projet/ws/loadEtudiant.php`
- **Method** : GET

### Réponse attendue
```json
[
  {"id": 1, "nom": "Lachgar", "prenom": "Mohamed", "ville": "Rabat", "sexe": "homme"},
  {"id": 2, "nom": "Safi", "prenom": "Amine", "ville": "Marrakech", "sexe": "homme"}
]
```

---

## 📝 Logcat attendu

```
D/RESPONSE: [{"id":"1","nom":"LACHGAR","prenom":"Mohamed","ville":"Rabat","sexe":"homme"}, ...]
D/ETUDIANT: Etudiant{id=1, nom='LACHGAR', prenom='Mohamed', ville='Rabat', sexe='homme'}
```
=======
# test


Démarrer XAMPP et activer Apache + MySQL. 


<img width="663" height="276" alt="image" src="https://github.com/user-attachments/assets/23340286-707c-4866-a38a-c85c30584ad7" />

<img width="1920" height="1018" alt="image" src="https://github.com/user-attachments/assets/65c28c3a-3d67-4b92-b4dc-ce6584b34c94" />


<img width="1920" height="923" alt="image" src="https://github.com/user-attachments/assets/0712a19a-e63c-4fc8-9035-48fd873ae9b3" />


Créer la table Etudiant : 

<img width="1920" height="1013" alt="image" src="https://github.com/user-attachments/assets/5dd4b973-4e92-4c77-a9d1-8120c8d3b8f2" />

<img width="1312" height="419" alt="image" src="https://github.com/user-attachments/assets/1b12d1ac-899b-40d2-a28d-c49288111f86" />

<img width="1305" height="671" alt="image" src="https://github.com/user-attachments/assets/58569b61-dae4-4ba9-b502-b18ea8beff93" />


Application Android (Volley + Gson) : 


Création du projet Android : 


<img width="645" height="1016" alt="image" src="https://github.com/user-attachments/assets/0a6c5791-743b-43c5-8942-8525b57c626d" />



>>>>>>> b62e410e98e472d1152ccf34ce60e7d6b6307c69
