# 🔀 Administration de commutateurs virtuels — Hyper-V

> Configuration du bridge réseau `vmbr0` en mode VLAN aware pour porter la segmentation à 6 VLAN sur les hyperviseurs Proxmox.

## Principe

Le port Ethernet du PC hôte **ASUS**, sur lequel est exécuté **VMware Workstation**, sera connecté au **switch TP-Link**.
Un **commutateur virtuel Hyper-V** sera configuré afin de permettre le transport du **VLAN GES** jusqu'à l'hyperviseur VMware Workstation.
Un **bridge réseau** sera ensuite mis en place sur l'hôte afin d'assurer la transmission du trafic VLAN tagué vers les machines virtuelles concernées.

## Procédure

1. Activer *VLAN aware* sur l'interface physique `vmbr0` (Datacenter › Système réseau).
2. Pour chaque VLAN métier, créer une interface logique dédiée (Linux Bond ou Linux VLAN) avec l'IP de passerelle et le tag correspondant.
3. Sur chaque VM ou conteneur LXC, attacher la carte réseau virtuelle à `vmbr0` en renseignant simplement le **tag VLAN** voulu — pas besoin de bridge dédié par VLAN.

## Bénéfice de l'approche

Un seul commutateur virtuel par nœud suffit à porter l'ensemble des 6 VLAN de l'infrastructure (LAN, TEST, SRV, GES, SEC, PRA, VPN), le tagging 802.1Q se faisant au niveau de chaque interface de VM/LXC plutôt que par la multiplication de bridges physiques.

## Repos liés

- `proxmox-commutateurs-virtuels`
- `conception-infrastructure-datacenter` — hôte ESXi ASUS (poste de gestion)

## Auteur

**Lilian Vertueux** — [LinkedIn](https://www.linkedin.com/in/lilian-vertueux/)
