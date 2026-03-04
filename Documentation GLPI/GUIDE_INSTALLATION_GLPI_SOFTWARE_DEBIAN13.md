# Guide Installation des Fichiers GLPI - Debian 13

La base de données est prête. Nous allons maintenant installer GLPI lui-même.

## Étape 1 : Téléchargement

Nous allons télécharger la version **10.0.17** de GLPI (version stable recommandée).

1.  Placez-vous dans le dossier temporaire :
    ```bash
    cd /tmp
    ```

2.  Téléchargez l'archive :
    ```bash
    wget https://github.com/glpi-project/glpi/releases/download/10.0.17/glpi-10.0.17.tgz
    ```

## Étape 2 : Extraction et Installation

1.  Décompressez l'archive directement dans le dossier du serveur web :
    ```bash
    tar -xzvf glpi-10.0.17.tgz -C /var/www/html
    ```

2.  Donnez les droits à Apache (www-data) sur le dossier GLPI :
    ```bash
    chown -R www-data:www-data /var/www/html/glpi
    ```

3.  Fixez les permissions des fichiers :
    ```bash
    chmod -R 755 /var/www/html/glpi
    ```

## Étape 3 : Vérification

Vérifiez que le dossier est bien là :
```bash
ls -l /var/www/html/glpi
```
Vous devriez voir une liste de dossiers (config, files, inc, etc.) appartenant à `www-data`.

---

## Étape Suivante : Finalisation Web

Tout est prêt côté serveur !
La prochaine et dernière étape se passera dans votre navigateur web pour l'assistant d'installation graphique.
