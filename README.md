# 🔀 Administration de commutateurs virtuels — Hyper-V

> Volet Hyper-V de la découverte des mécanismes de commutation virtuelle, en miroir de l'approche Proxmox.

## Statut

🚧 **Documentation à compléter** — ce volet correspond à une phase d'exploration de l'hyperviseur Hyper-V (poste de gestion Windows / VMware Workstation), en parallèle du socle Proxmox qui constitue l'infrastructure de production du homelab. Les procédures détaillées restent à formaliser dans ce dépôt.

## Objectif de la démarche

Comparer les mécanismes de commutation virtuelle entre deux familles d'hyperviseurs :

- **Proxmox (type 1, bare-metal)** : commutateur Linux Bridge en mode VLAN aware, tagging porté par chaque interface de VM/LXC (voir `proxmox-commutateurs-virtuels`).
- **Hyper-V (intégré Windows)** : commutateurs virtuels externes/internes/privés, VLAN ID configuré au niveau de l'adaptateur réseau virtuel de chaque VM.

## Points de comparaison à documenter

- [ ] Types de commutateurs virtuels Hyper-V (externe, interne, privé) et cas d'usage
- [ ] Configuration du tagging VLAN par adaptateur réseau virtuel
- [ ] Différences de performance et d'isolation observées face à l'approche Proxmox
- [ ] Cas d'usage retenu pour le poste de gestion (VMware Workstation / postes W11)

## Repos liés

- `proxmox-commutateurs-virtuels`
- `conception-infrastructure-datacenter` — hôte ESXi ASUS (poste de gestion)

## Auteur

**Lilian Vertueux** — [LinkedIn](https://www.linkedin.com/in/lilian-vertueux/)
