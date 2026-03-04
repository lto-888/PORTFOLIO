# Guide Installation LAMP & Configuration Initiale - Debian 13

Ce guide reprend vos actions et détaille la suite pour installer le socle technique de GLPI.

## Étape 1 : Connexion au serveur (Post-Installation)

Après le redémarrage, connectez-vous.
*   Si vous êtes en mode graphique : Ouvrez le terminal.
*   Si vous êtes en mode texte : Loguez-vous directement.

Passez en mode administrateur (Root) :
```bash
su -
# Entrez le mot de passe : Pa$$w0rd
```
*(Vous devez voir le prompt `#` à la fin de la ligne, indiquant que vous êtes root)*.

## Étape 2 : Mise à jour du système

Assurez-vous que Debian est parfaitement à jour (comme vous l'avez fait) :
```bash
apt update && apt full-upgrade -y
```

## Étape 3 : Installation de la pile LAMP (Linux, Apache, MySQL/MariaDB, PHP)

Vous avez lancé l'installation avec PHP 8.4 (version très récente de Debian Trixie). C'est parfait pour la performance.

La commande que vous avez utilisée :
```bash
sudo apt-get install apache2 php8.4-fpm mariadb-server -y
```

### 3.1 Activer PHP-FPM dans Apache
Comme vous avez installé `php8.4-fpm` (et non le module standard libapache2-mod-php), il faut dire à Apache de l'utiliser.

Tapez ces commandes une par une :
```bash
a2enmod proxy_fcgi setenvif
a2enconf php8.4-fpm
systemctl restart apache2
```

### 3.2 Vérifier que tout fonctionne
Pour vérifier, créez un petit fichier de test :
```bash
echo "<?php phpinfo(); ?>" > /var/www/html/info.php
```

Depuis un navigateur (sur votre PC ou dans la VM), allez sur :
`http://192.168.10.31/info.php`

Vous devriez voir une page violette PHP Version 8.4.x.

### 3.3 Installer les extensions PHP pour GLPI (Très Important)
GLPI a besoin de modules supplémentaires pour fonctionner.
Vous avez lancé la commande parfaite :

```bash
sudo apt install php8.4-{curl,gd,intl,mysql,zip,bcmath,mbstring,xml,bz2}
```

*   Le système va lister les paquets et vous demander confirmation.
*   Répondez **O** (Oui) et faites **Entrée**.

---

## Étape Suivante : Configuration de la Base de Données

Une fois LAMP et les extensions installés, nous devons sécuriser MariaDB et créer la base pour GLPI.
*(Attendez mes instructions pour cette partie, ou lancez `mariadb-secure-installation` si vous connaissez).*
