# 🔀 Administration de commutateurs virtuels — Hyper-V

> Configuration du bridge réseau `vmbr0` en mode VLAN aware pour porter la segmentation à 6 VLAN sur les hyperviseurs Proxmox.

## Principe

Le port Ethernet du PC hôte **ASUS**, sur lequel est exécuté **VMware Workstation**, sera connecté au **switch TP-Link**.
Un **commutateur virtuel Hyper-V** sera configuré afin de permettre le transport du **VLAN GES** jusqu'à l'hyperviseur VMware Workstation.
Un **bridge réseau** sera ensuite mis en place sur l'hôte afin d'assurer la transmission du trafic VLAN tagué vers les machines virtuelles concernées.

## Procédure

1. Procéder à la création du commutateur (Action › Gestionnaire de commutateur virtuel).
2. Renseigner les informations: <img width="722" height="687" alt="hyperv" src="https://github.com/user-attachments/assets/e61ff3b2-417d-42ad-a5e6-c98ebc011e8e" />
3. Pour permettre à l’hôte Hyper-V de communiquer sur un réseau via un commutateur virtuel externe, il est nécessaire d’ajouter une carte réseau virtuelle.
```bash
Add-VMNetworkAdapter -ManagementOS -Name "W-GES-VLAN-tag30" -SwitchName "RAIDAPORTER_LAN" -Passthru | Set-VMNetworkAdapterVlan -Access -VlanId 30
```

## Bénéfice de l'approche

Un seul commutateur virtuel par nœud suffit à porter l'ensemble des 6 VLAN de l'infrastructure (LAN, TEST, SRV, GES, SEC, PRA, VPN), le tagging 802.1Q se faisant au niveau de chaque interface de VM/LXC plutôt que par la multiplication de bridges physiques.

## Repos liés

- `proxmox-commutateurs-virtuels`
- `conception-infrastructure-datacenter` — hôte ESXi ASUS (poste de gestion)

## Auteur

**Lilian Vertueux** — [LinkedIn](https://www.linkedin.com/in/lilian-vertueux/)
