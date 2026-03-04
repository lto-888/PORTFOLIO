# Guide Configuration Base de Données (MariaDB) - Debian 13

Une fois les extensions PHP installées, nous devons préparer la base de données pour GLPI.

## Étape 1 : Connexion à MariaDB

Connectez-vous à la console de base de données en tant que root :
```bash
mariadb
```
*(Le prompt va changer pour devenir `MariaDB [(none)]>`).*

## Étape 2 : Création de la Base et de l'Utilisateur

Copiez-collez ces commandes une par une (ou tapez-les soigneusement) :

1.  **Créer la base de données pour GLPI (Vous l'avez déjà fait avec `db25_glpi`) :**
    ```sql
    CREATE DATABASE db25_glpi;
    ```

2.  **Créer l'utilisateur (remplacez 'MonMotDePasse' par un vrai mot de passe sécurisé) :**
    ```sql
    CREATE USER 'glpi_user'@'localhost' IDENTIFIED BY 'MonMotDePasseGLPI';
    ```

3.  **Donner les permissions à l'utilisateur sur la base `db25_glpi` :**
    ```sql
    GRANT ALL PRIVILEGES ON db25_glpi.* TO 'glpi_user'@'localhost';
    ```

4.  **Appliquer les changements :**
    ```sql
    FLUSH PRIVILEGES;
    ```

5.  **Quitter MariaDB :**
    ```sql
    EXIT;
    ```

## Résumé des identifiants BDD
Gardez ces infos précieusement, GLPI vous les demandera plus tard lors de l'installation web :
*   **Serveur de BDD :** `localhost`
*   **Utilisateur :** `glpi_user` (ou celui que vous avez créé)
*   **Mot de passe :** `MonMotDePasseGLPI` (celui que vous avez choisi)
*   **Base de données :** `db25_glpi`

---

## Étape Suivante : Téléchargement de GLPI

Une fois la base prête, nous téléchargerons la dernière version de GLPI.
