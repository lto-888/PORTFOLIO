# Architecture Réseau - Environnement GLPI Virtualisé

Ce document présente l'architecture réseau de votre environnement GLPI hébergé sur Proxmox.

```mermaid
graph TD
    %% Noeuds externs
    WAN((Internet / WAN))
    
    %% Environnement Proxmox
    subgraph Proxmox [Environnement Virtuel Proxmox<br/>IP Hôte: 10.74.3.203:8006]
        direction TB
        
        %% Routeur / Pare-feu
        pfSense[<B>pfSense</B><br/>Pare-feu & Routeur<br/>Gateway]
        
        %% Réseau Privé
        subgraph VLAN10 [VLAN 10 - Réseau Interne]
            direction LR
            
            %% Machines Virtuelles
            GLPI[<B>Serveur GLPI</B><br/>Debian 12/13<br/>IP: 192.168.10.10]
            Win10[<B>Client Windows 10</B><br/>Poste de test<br/>IP: 192.168.10.11]
            
            %% Connexions internes
            GLPI <--> Win10
        end
        
        %% Connexion VLAN vers Routeur
        VLAN10 <-->|.1 (Gateway)| pfSense
    end
    
    %% Connexion Hôte vers WAN
    pfSense <--> WAN
    
    %% Styles
    style Proxmox fill:#f9f9f9,stroke:#333,stroke-width:2px
    style VLAN10 fill:#e1f5fe,stroke:#0277bd,stroke-width:2px,stroke-dasharray: 5 5
    style pfSense fill:#ffccbc,stroke:#d84315,stroke-width:2px
    style GLPI fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    style Win10 fill:#bbdefb,stroke:#1565c0,stroke-width:2px
    style WAN fill:#eeeeee,stroke:#333
```

## Détails de la Configuration

| Composant | Rôle | IP / Réseau | Notes |
| :--- | :--- | :--- | :--- |
| **Proxmox VE** | Hyperviseur | 10.74.3.203 | Gère les VMs et le réseau virtuel. |
| **pfSense** | Routeur / Pare-feu | *WAN (DHCP)* / 192.168.10.1 | Assure la sortie internet pour le VLAN 10. |
| **VLAN 10** | Réseau Privé | 192.168.10.0/24 | Isole les machines de test. |
| **GLPI** | Serveur Applicatif | 192.168.10.10 | Héberge GLPI, Apache, MariaDB. |
| **Windows 10** | Client | 192.168.10.11 | Utilisé pour accéder à l'interface web GLPI. |

## Flux de Communication

1.  **Administration Proxmox** : Accès via `https://10.74.3.203:8006` depuis le réseau physique.
2.  **Accès GLPI** : Le client Windows 10 accède à GLPI via `http://192.168.10.10`.
3.  **Accès Internet** : Les VMs (GLPI et Win10) sortent via la passerelle pfSense (192.168.10.1).
