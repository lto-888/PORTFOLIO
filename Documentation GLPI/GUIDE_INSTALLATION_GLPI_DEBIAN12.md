# Guide d'Installation de GLPI sur Debian 12 (Bookworm)

Ce guide détaille l'installation de GLPI (Gestionnaire Libre de Parc Informatique) sur un serveur Debian 12, et comment y accéder depuis un client Windows 10.

## Prérequis

*   **Serveur :** Debian 12 installé avec accès root ou sudo.
*   **Client :** Windows 10 sur le même réseau.
*   **Réseau :** Adresse IP statique recommandée pour le serveur (ex: 192.168.1.100).

---

## Étape 1 : Mise à jour du système

Connectez-vous à votre terminal Debian (SSH ou directement) et lancez :

```bash
sudo apt update && sudo apt upgrade -y
```

## Étape 2 : Installation des dépendances (LAMP + Extensions PHP)

GLPI nécessite un serveur web, une base de données et PHP.

### 2.1 Installer Apache et MariaDB

Dans votre terminal, la commande doit ressembler à ceci :

```bash
root@debian:~# sudo apt install apache2 mariadb-server -y
Lecture des listes de paquets... Fait
Construction de l'arbre des dépendances... Fait
[...]
0 mis à jour, 2 nouvellement installés, 0 à enlever et 0 non mis à jour.
```

### 2.2 Installer PHP et ses extensions requises

Copiez cette commande précise pour installer PHP 8.2 et tous les modules indispensables :

```bash
root@debian:~# sudo apt install php php-xml php-common php-json php-mysql php-mbstring php-curl php-gd php-intl php-zip php-bz2 php-imap php-apcu php-ldap -y
```

### 2.3 Configuration PHP

Ouvrez le fichier `php.ini` d'Apache :

```bash
sudo nano /etc/php/8.2/apache2/php.ini
```

Recherchez et modifiez les lignes suivantes (utilisez `Ctrl+W` pour chercher dans nano) :

*   `memory_limit = 256M` (ou plus, ex: 512M)
*   `upload_max_filesize = 20M` (permet l'upload de fichiers plus gros)
*   `post_max_size = 20M`
*   `max_execution_time = 600`
*   `date.timezone = Europe/Paris` (Ajustez selon votre zone géographique)
*   `session.cookie_httponly = On`

Sauvegardez (`Ctrl+O`, `Entrée`) et quittez (`Ctrl+X`).

Redémarrez Apache pour appliquer les changements :

```bash
sudo systemctl restart apache2
```

---

## Étape 3 : Configuration de la Base de Données

Connectez-vous à MariaDB (l'écran deviendra noir avec le prompt `MariaDB [(none)]>`) :

```sql
root@debian:~# sudo mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.

MariaDB [(none)]> CREATE DATABASE glpidb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
Query OK, 1 row affected (0.001 sec)

MariaDB [(none)]> CREATE USER 'glpi_user'@'localhost' IDENTIFIED BY 'votre_mot_de_passe_securise';
Query OK, 0 rows affected (0.002 sec)

MariaDB [(none)]> GRANT ALL PRIVILEGES ON glpidb.* TO 'glpi_user'@'localhost';
Query OK, 0 rows affected (0.001 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.001 sec)

MariaDB [(none)]> EXIT;
Bye
root@debian:~# 
```

**Note visuelle :** Chaque ligne commençant par `Query OK` confirme que la commande a réussi.

---

## Étape 4 : Téléchargement et Installation de GLPI

### 4.1 Télécharger GLPI

Allez dans le répertoire temporaire :

```bash
cd /tmp
```

Téléchargez la dernière version stable de GLPI. (Vérifiez la dernière version sur [cette page](https://github.com/glpi-project/glpi/releases)). 
Exemple pour la version **10.0.10** :

```bash
wget https://github.com/glpi-project/glpi/releases/download/10.0.10/glpi-10.0.10.tgz
```

Décompressez l'archive dans le répertoire web :

```bash
sudo tar -xzvf glpi-10.0.10.tgz -C /var/www/html/
```

### 4.2 Permissions

Donnez les droits à l'utilisateur web (www-data) sur le dossier GLPI :

```bash
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi
```

---

## Étape 5 : Configuration Apache (Virtual Host)

Il est recommandé de configurer un Virtual Host pour GLPI.
Créez un fichier de configuration :

```bash
sudo nano /etc/apache2/sites-available/glpi.conf
```

Ajoutez le contenu suivant :

```apache
<VirtualHost *:80>
    ServerName glpi.local
    # Remplacez glpi.local par votre IP ou nom de domaine si vous en avez un
    
    DocumentRoot /var/www/html/glpi/public
    # Note: GLPI 10 recommande de pointer vers /public pour la sécurité

    <Directory /var/www/html/glpi/public>
        Require all granted
        RewriteEngine On
        RewriteCond %{REQUEST_FILENAME} !-f
        RewriteRule ^(.*)$ index.php [QSA,L]
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/glpi_error.log
    CustomLog ${APACHE_LOG_DIR}/glpi_access.log combined
</VirtualHost>
```
*Note : Si vous utilisez une ancienne version de GLPI ou préférez une config simple, `DocumentRoot /var/www/html/glpi` peut suffire, mais `/public` est recommandé pour la v10.*

Activez le site et le module rewrite :

```bash
sudo a2ensite glpi.conf
sudo a2enmod rewrite
sudo systemctl restart apache2
```

*(Optionnel : Désactivez le site par défaut si vous n'en avez pas besoin : `sudo a2dissite 000-default.conf`)*

---

## Étape 6 : Finalisation Web (Depuis Windows 10)

### 6.1 Accès depuis le client

Sur votre PC Windows 10, lancez votre navigateur.

**Barre d'adresse :**
```text
 _______________________________________________________
|  < > C  |  http://192.168.1.100/glpi             | X |
 -------------------------------------------------------
```
*(Remplacez 192.168.1.100 par l'IP de votre serveur)*

### 6.2 Assistant d'installation (Guide Visuel)

Vous arriverez sur une page blanche avec le logo GLPI. Suivez ces écrans :

**Écran 1 : Choix de la langue**
*   [ ] English
*   [x] **Français**
*   [ ] Espagnol
*   *(Cliquez sur OK)*

**Écran 2 : Licence**
*   Une grande zone de texte apparaît avec la licence GNU GPL.
*   Cochez le bouton radio : **(o) J'ai lu et ACCEPTE les termes de la licence...**
*   Cliquez sur **"Continuer"**.

**Écran 3 : Installation ou Mise à jour**
*   Vous verrez deux gros boutons.
*   Cliquez sur : **[ INSTALLER ]**

**Écran 4 : Vérification de l'environnement**
*   Une liste de tests s'affiche.
*   🟢 **Tout doit être vert** (ou 🟠 orange).
*   🔴 **Si vous voyez du ROUGE** : Stoppez tout. Il manque une extension PHP (voir Étape 2.2).
*   Si tout est bon, cliquez sur **"Continuer"** tout en bas.

**Écran 5 : Connexion à la base de données**
Remplissez le formulaire exactement comme ceci :

| Champ | Valeur à entrer |
| :--- | :--- |
| **Serveur SQL** | `localhost` |
| **Utilisateur SQL** | `glpi_user` |
| **Mot de passe SQL** | `votre_mot_de_passe_securise` |

*   Cliquez sur **"Continuer"**.

**Écran 6 : Choix de la base**
*   Sélectionnez dans la liste : **`glpidb`**
*   *(Si la liste est vide, vérifiez votre utilisateur SQL à l'étape 3)*.
*   Cliquez sur **"Continuer"**.

**Écran 7 : Fin**
*   L'installation est terminée !
*   Notez les identifiants affichés (glpi/glpi).
*   Cliquez sur **"Utiliser GLPI"**.

### 6.3 Première Connexion

Vous arrivez sur l'écran de connexion standard :

```text
       ___________________________
      |         GLPI              |
      |                           |
      |  Identifiant : [ glpi   ] |
      |  Mot de passe: [ ****   ] |
      |                           |
      |       [ Envoyer ]         |
      |___________________________|
```

Connectez-vous avec `glpi` / `glpi`.

⚠️ **Tache Post-Installation :**
Dès la première connexion, GLPI vous demandera de changer les mots de passe des comptes par défaut (`glpi`, `post-only`, `tech`, `normal`). **Faites-le immédiatement** pour sécuriser votre installation.

De plus, supprimez le fichier d'installation pour la sécurité :
Sur Debian :
```bash
sudo rm /var/www/html/glpi/install/install.php
```

---

## Dépannage Client Windows 10

Si le navigateur Windows 10 affiche "Ce site est inaccessible" :

1.  **Vérifier la connexion :**
    Ouvrez l'invite de commande (cmd) sur Windows 10 et tapez :
    `ping 192.168.1.XX` (IP du serveur Debian).
    *   Si "Délai d'attente dépassé" : Vérifiez que les deux machines sont sur le même réseau (ex: Box internet commune ou Switch).

2.  **Vérifier le Pare-feu Debian (UFW) :**
    Si un pare-feu est actif sur Debian, il peut bloquer le port 80 (HTTP). Autorisez-le :
    ```bash
    sudo ufw allow 80/tcp
    sudo ufw allow 443/tcp
    sudo ufw reload
    ```

3.  **Vérifier le service Apache :**
    Sur Debian : `sudo systemctl status apache2`. Il doit être "active (running)".
