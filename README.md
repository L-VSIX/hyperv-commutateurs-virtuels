# 🔀 Administration de commutateurs virtuels — Hyper-V

> Configuration du bridge réseau `vmbr0` en mode VLAN aware pour porter la segmentation à 6 VLAN sur les hyperviseurs Proxmox.

## Principe

Le port Ethernet du PC hôte **ASUS**, sur lequel est exécuté **VMware Workstation**, sera connecté au **switch TP-Link**.
Un **commutateur virtuel Hyper-V** sera configuré afin de permettre le transport du **VLAN GES** jusqu'à l'hyperviseur VMware Workstation.
Un **bridge réseau** sera ensuite mis en place sur l'hôte afin d'assurer la transmission du trafic VLAN tagué vers les machines virtuelles concernées.

## Procédure

1. Procéder à la création du commutateur (Action › Gestionnaire de commutateur virtuel).
2. Renseigner les informations:
<img width="722" height="687" alt="hyperv" src="https://github.com/user-attachments/assets/e61ff3b2-417d-42ad-a5e6-c98ebc011e8e" />

4. Pour permettre à l’hôte Hyper-V de communiquer sur un réseau via un commutateur virtuel externe, il est nécessaire d’ajouter une carte réseau virtuelle.
```bash
Add-VMNetworkAdapter -ManagementOS -Name "W-GES-VLAN-tag30" -SwitchName "RAIDAPORTER_LAN" -Passthru | Set-VMNetworkAdapterVlan -Access -VlanId 30
```

## Bénéfice de l'approche

Ajout rapide de réseaux logiques sans ajouter forcément de nouvelles cartes physiques.

## Repos liés

- [`proxmox-commutateurs-virtuels`](https://github.com/L-VSIX/proxmox-commutateurs-virtuels)
- [`conception-infrastructure-datacenter`](https://github.com/L-VSIX/conception-infrastructure-datacenter) — hôte ESXi ASUS (poste de gestion)

## Auteur

**Lilian Vertueux** — [LinkedIn](https://www.linkedin.com/in/lilian-vertueux/)
