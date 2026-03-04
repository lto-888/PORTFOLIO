# Guide Finalisation Web - GLPI 10

Une fois les commandes terminées sur le serveur, tout se passe dans votre navigateur !

## Étape 1 : Accès à l'interface

1.  Ouvrez votre navigateur (Chrome, Firefox...) sur votre PC.
2.  Tapez l'adresse : `http://192.168.10.31/glpi`

## Étape 2 : Assistant d'installation

1.  **Langue :** Choisissez `Français` et validez.
2.  **Licence :** Cliquez sur `J'ai lu et ACCEPTE...` puis `Continuer`.
3.  **Type d'installation :** Cliquez sur le bouton **[ INSTALLER ]**.
4.  **Vérification de l'environnement :**
    *   Vous devriez avoir une liste de points verts.
    *   Si tout est vert (ou orange), cliquez sur `Continuer`.
    *(Si vous avez des points rouges bloquants, dites-le moi !)*

## Étape 3 : Connexion à la Base de Données

C'est ici qu'on utilise les infos que vous avez configurées :

*   **Serveur SQL :** `localhost`
*   **Utilisateur SQL :** `glpi_adm`
*   **Mot de passe SQL :** `Pa$$w0rd`

Cliquez sur `Continuer`.

## Étape 4 : Choix de la Base

*   L'assistant doit vous proposer : "Sélectionner une base existante".
*   Choisissez : `db25_glpi` dans la liste.
*   Cliquez sur `Continuer`.

*(Un message vous dira "Base de données initialisée", ça peut prendre quelques secondes).*

## Étape 5 : Fin

1.  **Télémétrie :** Décochez "Envoyer des statistiques" (au choix).
2.  Cliquez sur `Continuer` jusqu'à voir le bouton **[ UTILISER GLPI ]**.

## Étape 6 : Première Connexion

Vous arrivez sur la mire de connexion de GLPI.
Les identifiants par défaut sont :
*   **Identifiant :** `glpi`
*   **Mot de passe :** `glpi`

⚠️ **Important :** Changez ce mot de passe dès la première connexion !
