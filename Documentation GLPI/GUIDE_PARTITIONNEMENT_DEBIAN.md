# Guide Partitionnement des Disques - Debian 13

Cette étape prépare votre disque dur pour recevoir Debian. 
⚠️ **Attention :** Toutes les données présentes sur le disque virtuel seront effacées.

## Étape 1 : Méthode de partitionnement

L'installateur vous propose plusieurs choix.
*   Sélectionnez : **Assisté - utiliser un disque entier**
*   *(C'est le choix par défaut, le plus simple).*
*   Cliquez sur **[ Continuer ]**.

```text
 _____________________________________________________________________________
|                          Partitionner les disques                           |
|                                                                             |
|  Méthode de partitionnement :                                               |
|  [ Assisté - utiliser un disque entier                                    ] |
|  [ Assisté - utiliser tout un disque avec LVM                             ] |
|  [ Assisté - utiliser tout un disque avec LVM chiffré                     ] |
|  [ Manuel                                                                 ] |
|_____________________________________________________________________________|
```

## Étape 2 : Choix du disque

Sélectionnez le disque sur lequel installer Debian.
*   Sélectionnez : **SCSI1 (0,0,0) (sda) - 34.4 GB QEMU HARDDISK**
*   *(Le nom "QEMU HARDDISK" confirme que c'est bien votre disque virtuel).*
*   Cliquez sur **[ Continuer ]**.

## Étape 3 : Schéma de partitionnement

*   Sélectionnez : **Tout dans une seule partition (recommandé pour les débutants)**
*   *(Cela crée une structure simple avec `/` et une petite zone d'échange `swap`).*
*   Cliquez sur **[ Continuer ]**.

## Étape 4 : Validation (Fin)

L'installateur vous montre le résultat (table des partitions).
*   Vérifiez que la ligne **Terminer le partitionnement et appliquer les changements** est sélectionnée (en bas).
*   Cliquez sur **[ Continuer ]**.

```text
 _____________________________________________________________________________
|                          Partitionner les disques                           |
|                                                                             |
|  > n° 1  primaire  32.6 GB  f  ext4    /                                    |
|  > n° 5  logique    1.8 GB  f  swap    swap                                 |
|                                                                             |
|  Annuler les modifications des partitions                                   |
|  [ Terminer le partitionnement et appliquer les changements               ] |
|_____________________________________________________________________________|
```

⚠️ **Étape suivante (Important) :**
Juste après cet écran, une fenêtre vous demandera confirmation : **"Faut-il appliquer les changements sur les disques ?"**.
*   Il faut impérativement cocher **[ OUI ]**.
*   (Par défaut c'est souvent sur "Non", faites attention).
