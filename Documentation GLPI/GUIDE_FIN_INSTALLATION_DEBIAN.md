# Guide Finalisation Installation - Debian 13

Voici les dernières étapes pour terminer l'installation de votre serveur GLPI.

## Étape 1 : Popularity Contest (Statistiques)

Debian vous demande si vous voulez envoyer des statistiques anonymes sur les logiciels utilisés.
*   **Sélectionnez :** `Non`
*   Cliquez sur **[ Continuer ]**.

## Étape 2 : Sélection des logiciels (IMPORTANT)

C'est ici que l'on définit le rôle du serveur.
Pour un serveur GLPI performant, nous n'avons pas besoin d'interface graphique (qui alourdit le système inutilement).

**Cochez UNIQUEMENT les cases suivantes** (Décochez les autres avec la barre d'espace) :

*   [ ] environnement de bureau Debian (**DÉCOCHER**)
*   [ ] ... GNOME (**DÉCOCHER**)
*   [ ] ... (Tous les autres bureaux décochés)
*   [x] **serveur SSH** (**COCHER** - Indispensable pour se connecter à distance)
*   [x] **utilitaires usuels du système** (**COCHER** - Garder coché)

*(Si vous tenez absolument à avoir une interface graphique, laissez "environnement de bureau" coché, mais cela consommera plus de ressources).*

*   Cliquez sur **[ Continuer ]**.

## Étape 3 : Installation du chargeur de démarrage GRUB

GRUB est le petit programme qui lance Debian au démarrage.

### 3.1 Installer GRUB sur le disque principal
*   L'installateur demande : "Installer le programme de démarrage GRUB sur le disque principal ?"
*   **Sélectionnez :** `Oui`
*   Cliquez sur **[ Continuer ]**.

### 3.2 Choix du périphérique
*   L'installateur vous demande où l'installer.
*   **Sélectionnez :** `/dev/sda (scsi-0QEMU_HARDDISK...)`
*   *(Ne choisissez pas "Saisir le périphérique manuellement").*
*   Cliquez sur **[ Continuer ]**.

## Étape 4 : Fin de l'installation

L'installation est terminée !
*   L'installateur va ejecter le "CD" virtuel automatiquement.
*   Cliquez sur **[ Continuer ]** pour redémarrer le système.

---

🎉 **Félicitations !** Votre serveur Debian 13 est installé.
Au redémarrage, vous arriverez sur un écran noir (terminal) demandant un login.
*   **Login :** `root`
*   **Password :** `Pa$$w0rd`
