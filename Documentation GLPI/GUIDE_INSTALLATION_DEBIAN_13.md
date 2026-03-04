# Guide d'Installation de Debian 13 (Trixie) - Pas à Pas

Ce guide vous accompagne étape par étape dans l'installation de Debian 13 (actuellement en version *Testing*, nom de code *Trixie*).

**Note Importante :** Debian 13 étant en phase de test, certaines options peuvent légèrement varier, mais le principe reste identique à la version stable.

---

## 1. Démarrage (Boot)

Insérez votre clé USB ou CD d'installation et démarrez l'ordinateur.

**Menu de Démarrage (GRUB) :**
Vous verrez un écran avec le logo Debian (spirale rouge).
Sélectionnez :
*   `Graphical install` (Recommandé pour débuter)
*   *Ou `Install` pour le mode texte (plus rapide, moins joli).*

---

## 2. Configuration Régionale

L'installateur va vous poser une série de questions simples.

1.  **Select a language (Langue) :**
    *   Cherchez et sélectionnez `French - Français`
    *   Cliquez sur [Continue]

2.  **Situation géographique :**
    *   Sélectionnez `France` (ou votre pays)
    *   Cliquez sur [Continuer]

3.  **Configurer le clavier :**
    *   Sélectionnez `Français`
    *   Cliquez sur [Continuer]

*(Chargement des composants... Patientez quelques secondes)*

---

## 3. Configuration Réseau

L'installateur détecte votre carte réseau.
Si vous êtes en Ethernet (câble), c'est automatique.
Si vous êtes en Wi-Fi, il vous demandera votre réseau et mot de passe.

1.  **Nom de machine (Hostname) :**
    *   Par défaut : `debian`
    *   Mettez ce que vous voulez, par exemple : `srv-glpi`
    *   [Continuer]

2.  **Nom de domaine :**
    *   Laissez vide (sauf si vous êtes dans un réseau d'entreprise spécifique).
    *   [Continuer]

---

## 4. Configuration Utilisateurs et Mots de passe

C'est ici que vous définissez la sécurité.

1.  **Mot de passe du "superutilisateur" (root) :**
    *   C'est le compte Administrateur suprême.
    *   Choisissez un mot de passe **FORT** et **MEMORISEZ-LE BIEN**.
    *   Confirmez-le.
    *   [Continuer]

2.  **Nom complet du nouvel utilisateur :**
    *   Mettez votre Prénom ou un pseudo (ex: `Léo`).
    *   [Continuer]

3.  **Identifiant pour le compte utilisateur :**
    *   Le système propose une version minuscule (ex: `leo`). Acceptez.
    *   [Continuer]

4.  **Mot de passe pour le nouvel utilisateur :**
    *   C'est le mot de passe pour votre session habituelle.
    *   [Continuer]

---

## 5. Partitionnement des disques

Attention, cette étape formate le disque !

1.  **Méthode de partitionnement :**
    *   Choisissez : `Assisté - utiliser tout un disque` (Le plus simple).
    *   [Continuer]

2.  **Disque à partitionner :**
    *   Sélectionnez votre disque dur / SSD.
    *   [Continuer]

3.  **Schéma de partitionnement :**
    *   Choisissez : `Tout dans une seule partition (recommandé pour les débutants)`
    *   [Continuer]

4.  **Résumé :**
    *   L'écran affiche "Terminer le partitionnement et appliquer les changements".
    *   Vérifiez que c'est le bon choix.
    *   [Continuer]

5.  **Confirmation (Important !) :**
    *   La question est : "Faut-il appliquer les changements sur les disques ?"
    *   Par défaut, c'est sur "Non".
    *   **Cochez [OUI]**.
    *   [Continuer]

*(L'installation du système de base commence... Cela peut prendre 5 à 10 minutes).*

---

## 6. Gestionnaire de paquets (APT)

1.  **Faut-il analyser d'autres supports d'installation ?**
    *   Cochez `Non`.
    *   [Continuer]

2.  **Pays du miroir de l'archive Debian :**
    *   Choisissez `France`.
    *   [Continuer]

3.  **Miroir de l'archive Debian :**
    *   Gardez `deb.debian.org` (le défaut).
    *   [Continuer]

4.  **Mandataire HTTP (Proxy) :**
    *   Laissez vide (sauf besoin spécifique).
    *   [Continuer]

---

## 7. Sélection des logiciels

1.  **Étude de popularité (Popcon) :**
    *   Répondez `Non` (ou `Oui` si vous voulez aider Debian, peu importe).
    *   [Continuer]

2.  **Choix des logiciels à installer :**
    C'est l'étape cruciale pour la "lourdeur" de votre système.
    
    *   [ ] Environnement de bureau Debian (GNOME par défaut)
    *   [ ] ... GNOME
    *   [ ] ... Xfce (Plus léger)
    *   [x] **Serveur SSH** (TRES IMPORTANT pour prendre la main à distance !)
    *   [x] **Utilitaires usuels du système** (Gardez coché)

    **Conseil :**
    *   Si c'est un **Serveur pur** (pour GLPI) : **Décochez "Environnement de bureau Debian"** et **"GNOME"**. Gardez juste "SSH" et "Utilitaires". Vous aurez un écran noir à commandes (très léger et rapide).
    *   Si vous voulez une souris et des fenêtres : Cochez "Environnement de bureau" et choisissez "GNOME" (moderne) ou "XFCE" (léger).

    *   [Continuer]

*(Le téléchargement des paquets commence. Cela dépend de votre connexion internet).*

---

## 8. Finalisation

1.  **Installer le programme de démarrage GRUB :**
    *   Question : "Installer le programme de démarrage GRUB sur le disque principal ?"
    *   Répondez **[OUI]**.
    *   [Continuer]
    *   **Important :** Sélectionnez votre disque (`/dev/sda` ou `/dev/nvme...`) dans la liste. **Ne choisissez PAS** "Saisir le périphérique manuellement".

2.  **Installation terminée :**
    *   Retirez votre clé USB.
    *   Cliquez sur [Continuer] pour redémarrer.

---

## 9. Premier Démarrage

Votre ordinateur redémarre.
*   Si vous avez installé une interface graphique (GNOME), vous verrez un écran de connexion joli. Cliquez sur votre nom et mettez votre mot de passe.
*   Si vous avez installé un serveur (Mode texte), vous aurez :
    ```text
    Debian GNU/Linux trixie/sid srv-glpi login:
    ```
    Tapez votre login (ex: `leo`), validez, puis votre mot de passe (il ne s'affiche pas quand on tape, c'est normal).

Bravo ! Debian 13 est installé. Vous pouvez passer à l'installation de GLPI.
