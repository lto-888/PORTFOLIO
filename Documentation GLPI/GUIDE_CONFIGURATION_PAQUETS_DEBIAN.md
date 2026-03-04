# Guide Configuration Gestionnaire de Paquets (APT) - Debian 13

Une fois le système de base installé, l'installateur configure "APT", l'outil qui permet d'installer les logiciels (comme GLPI plus tard).

## Étape 1 : Analyser d'autres supports

L'installateur vous demande si vous avez d'autres CD/DVD d'installation.
*   **Sélectionnez :** `Non`
*   Cliquez sur **[ Continuer ]**.

```text
 _____________________________________________________________________________
|                  Configurer l'outil de gestion des paquets                  |
|                                                                             |
|  Faut-il analyser d'autres supports d'installation ?                        |
|  ( ) Oui                                                                    |
|  (o) Non                                                                    |
|_____________________________________________________________________________|
```

## Étape 2 : Choisir un miroir de l'archive (Pays)

Il faut choisir le serveur le plus proche pour télécharger les mises à jour rapidement.
*   **Pays :** `France`
*   *(Utilisez les flèches haut/bas pour trouver France dans la liste).*
*   Cliquez sur **[ Continuer ]**.

```text
 _____________________________________________________________________________
|                  Configurer l'outil de gestion des paquets                  |
|                                                                             |
|  Pays du miroir de l'archive Debian :                                       |
|  [ France                                                                 ] |
|_____________________________________________________________________________|
```

## Étape 3 : Choisir un miroir de l'archive (Serveur)

*   **Miroir :** `deb.debian.org`
*   *(C'est le choix par défaut et le plus fiable, il redirige automatiquement vers le meilleur serveur).*
*   Cliquez sur **[ Continuer ]**.

```text
 _____________________________________________________________________________
|                  Configurer l'outil de gestion des paquets                  |
|                                                                             |
|  Miroir de l'archive Debian :                                               |
|  [ deb.debian.org                                                         ] |
|  [ ftp.fr.debian.org                                                      ] |
|_____________________________________________________________________________|
```

## Étape 4 : Mandataire HTTP (Proxy)

*(Si un écran vous demande un mandataire HTTP)*
*   Laissez le champ **VIDE** (sauf si vous êtes dans une entreprise avec un proxy spécifique, ce qui est rare pour un labo personnel).
*   Cliquez sur **[ Continuer ]**.

---

⏳ **Note :** Après cette étape, l'installateur va télécharger des fichiers pendant quelques minutes ("Configuration d'APT...").
C'est normal si la barre de progression reste bloquée un instant sur "Réception de fichier 1 sur X".
