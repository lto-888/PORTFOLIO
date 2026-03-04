# Guide Configuration Réseau Manuelle - Debian 13

Ce guide détaille comment configurer une **adresse IP statique** pendant l'installation de Debian 13, comme vu dans vos captures d'écran.

Cette méthode est requise si le DHCP ne fonctionne pas ou si vous souhaitez fixer l'IP du serveur dès le départ.

## Étape 1 : Choisir la configuration manuelle

Lorsque l'installation échoue à configurer le réseau automatiquement, sélectionnez :
*   **[ Configurer vous-même le réseau ]**

## Étape 2 : L'Adresse IP

L'installateur vous demande votre adresse IP.
*   **Valeur à entrer :** `192.168.10.31`
*   *(C'est l'adresse unique de votre serveur GLPI)*

```text
 _____________________________________________________________________________
|                          Configurer le réseau                               |
|                                                                             |
|  Si vous ne savez pas quoi indiquer, veuillez consulter l'administrateur... |
|  Adresse IP :                                                               |
|  __________________________________________________________________________ |
| [ 192.168.10.31___________________________________________________________] |
|_____________________________________________________________________________|
```
*   Cliquez sur **[ Continuer ]**.

## Étape 3 : Le Masque de sous-réseau

Il définit la taille du réseau.
*   **Valeur à entrer :** `255.255.255.0`
*   *(Correspond à un réseau local standard /24)*

```text
 _____________________________________________________________________________
|                          Configurer le réseau                               |
|                                                                             |
|  Valeur du masque-réseau :                                                  |
|  __________________________________________________________________________ |
| [ 255.255.255.0___________________________________________________________] |
|_____________________________________________________________________________|
```
*   Cliquez sur **[ Continuer ]**.

## Étape 4 : La Passerelle (Gateway)

C'est l'adresse de votre routeur (pfSense) pour sortir sur Internet.
*   **Valeur à entrer :** `192.168.10.1`

```text
 _____________________________________________________________________________
|                          Configurer le réseau                               |
|                                                                             |
|  Passerelle :                                                               |
|  __________________________________________________________________________ |
| [ 192.168.10.1____________________________________________________________] |
|_____________________________________________________________________________|
```
*   Cliquez sur **[ Continuer ]**.

## Étape 5 : Servreurs de noms (DNS)

Ceux-ci permettent de traduire les noms (ex: google.com) en IP.
*   **Valeur à entrer :** `192.168.10.1`
*   *(On utilise ici le routeur pfSense comme DNS relais)*.
*   *Alternative si Internet ne marche pas : `8.8.8.8` (Google) ou `1.1.1.1` (Cloudflare).*

```text
 _____________________________________________________________________________
|                          Configurer le réseau                               |
|                                                                             |
|  Adresses des serveurs de noms :                                            |
|  __________________________________________________________________________ |
| [ 192.168.10.1____________________________________________________________] |
|_____________________________________________________________________________|
```
*   Cliquez sur **[ Continuer ]**.

## Étape 6 : Nom de la machine (Hostname)

*   **Valeur à entrer :** `debian` (ou `srv-glpi`)

```text
 _____________________________________________________________________________
|                          Configurer le réseau                               |
|                                                                             |
|  Nom de machine :                                                           |
|  __________________________________________________________________________ |
| [ debian__________________________________________________________________] |
|_____________________________________________________________________________|
```

## Résumé de la configuration

| Paramètre | Valeur Configurée |
| :--- | :--- |
| **IP** | `192.168.10.31` |
| **Masque** | `255.255.255.0` |
| **Passerelle** | `192.168.10.1` |
| **DNS** | `192.168.10.1` |
