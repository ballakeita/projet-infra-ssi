# projet-infra-ssi

Ce dépôt regroupe les codes, configurations et fichiers liés à la mise en place de notre infrastructure réseau, systèmes et sécurité.

Les différents éléments du projet seront ajoutés et organisés progressivement dans ce dépôt.

## Workflow de déploiement des VM

Le workflow GitHub Actions [deploy-vms.yml](.github/workflows/deploy-vms.yml) permet de déployer manuellement une VM sur l'hyperviseur Alice.

### Déroulement

1. Depuis l'onglet **Actions**, lancer le workflow **Deploy VM on Alice Hypervisor** avec `Run workflow`.
2. Renseigner les paramètres de la VM :
   - `vm_name` : nom de la VM, par exemple `srv4` ;
   - `memory` : mémoire RAM en Mo, par exemple `8192` ;
   - `tapnum` : numéro du port TAP, par exemple `53` ;
   - `tagnum` : numéro du VLAN, par exemple `20`.
3. Le job s'exécute sur le runner auto-hébergé installé sur Alice.
4. Le workflow génère `vm.yaml` avec les paramètres de la VM et `switch.yaml` avec la configuration du port Open vSwitch.
5. La configuration du switch est appliquée avec `switch-conf.py`.
6. La VM est démarrée avec `lab-startup.py`.

### Prérequis

Le runner doit pouvoir accéder aux scripts suivants et à l'image Debian utilisée par défaut :

- `$HOME/masters/scripts/switch-conf.py` ;
- `$HOME/masters/scripts/lab-startup.py` ;
- `debian-testing-amd64.qcow2`.
