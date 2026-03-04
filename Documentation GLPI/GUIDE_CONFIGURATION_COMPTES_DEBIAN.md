# Guide Configuration Comptes & Domaine - Debian 13

Ce document fait suite à la configuration réseau manuelle. Il détaille les écrans suivants de l'installation.

## Étape 1 : Le Domaine

Après la configuration IP, l'installateur demande le nom de domaine.
*   **Action :** Laissez ce champ **VIDE**.
*   Cliquez sur **[ Continuer ]**.

```text
 _____________________________________________________________________________
|                          Configurer le réseau                               |
|                                                                             |
|  Le domaine est la partie de l'adresse Internet qui est à la droite...      |
|  Domaine :                                                                  |
|  __________________________________________________________________________ |
| [ ________________________________________________________________________] |
|_____________________________________________________________________________|
```

## Étape 2 : Mot de passe Superutilisateur (Root)

C'est le compte administrateur suprême du système.
*   **Mot de passe :** `Pa$$w0rd`
*   **Confirmation :** `Pa$$w0rd`
*   *(Notez que le caractère `$` s'utilise ici).*
*   Cochez la case **[x] Afficher le mot de passe en clair** pour vérifier.

```text
 _____________________________________________________________________________
|           Créer les utilisateurs et choisir les mots de passe               |
|                                                                             |
|  Mot de passe du superutilisateur (<< root >>) :                            |
|  [ Pa$$w0rd                                                               ] |
|  [x] Afficher le mot de passe en clair                                      |
|                                                                             |
|  Confirmation du mot de passe :                                             |
|  [ Pa$$w0rd                                                               ] |
|  [x] Afficher le mot de passe en clair                                      |
|_____________________________________________________________________________|
```
*   Cliquez sur **[ Continuer ]**.

## Étape 3 : Création du nouvel utilisateur (non-root)

C'est le compte que vous utiliserez au quotidien.

### 3.1 Nom complet
*   **Nom complet :** `Client`
*   Cliquez sur **[ Continuer ]**.

### 3.2 Identifiant (Login)
*   **Identifiant :** `client` (en minuscules)
*   Cliquez sur **[ Continuer ]**.

### 3.3 Mot de passe utilisateur
*   **Mot de passe :** `Pa$$w0rd`
*   **Confirmation :** `Pa$$w0rd`
*   Cochez la case **[x] Afficher le mot de passe en clair** pour éviter les erreurs.

```text
 _____________________________________________________________________________
|           Créer les utilisateurs et choisir les mots de passe               |
|                                                                             |
|  Mot de passe pour le nouvel utilisateur :                                  |
|  [ Pa$$w0rd                                                               ] |
|  [x] Afficher le mot de passe en clair                                      |
|                                                                             |
|  Confirmation du mot de passe :                                             |
|  [ Pa$$w0rd                                                               ] |
|  [x] Afficher le mot de passe en clair                                      |
|_____________________________________________________________________________|
```
*   Cliquez sur **[ Continuer ]**.

## Résumé des Identifiants

| Compte | Identifiant (Login) | Mot de Passe | Rôle |
| :--- | :--- | :--- | :--- |
| **Administrateur** | `root` | `Pa$$w0rd` | Installation de logiciels, configuration système. |
| **Utilisateur** | `client` | `Pa$$w0rd` | Utilisation courante. |
