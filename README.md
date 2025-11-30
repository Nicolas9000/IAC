# Prérequis

## Installation de ansible sur la machine hôte

```
sudo apt update
sudo apt install -y software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install -y ansible
```

### Configuration ssh avec la machine hôte et cibles

#### Sur la machine hôte :

```
ssh-keygen -t rsa -b 2048
```

#### Sur les machines cibles :

```
sudo visudo

# à mettre à la toute fin
<user> ALL=(ALL) NOPASSWD: ALL
```

#### Sur la machine hôte :

```
ssh-copy-id <user>@<IP>
```

# Explication de la structure

## À la racine nous avons 2 dossiers et un fichier site.yaml :

- Le dossier d'inventaires qui contient comme sous dossier staging et production avec à l'intérieur leur fichier d'inventaire et leur variables d'environnement secret qui on été chiffrer par ansible-vault.

- Quand au dossier roles, il contient 3 sous dossier générer avec ansible-galaxy dont Nginx, Php et Mysql qui va nous permettre de déployer notre application web avec la stack LEMP.

- Et pour finir le site.yaml est le point d'entrer de notre configuration ansible

# Déploiement avec Ansible

## Pour déployer notre application web, il suffit de lancer cette commande :

```
# Pour staging
ansible-playbook -i inventories/staging/staging.ini site.yaml --ask-vault-pass

# Pour production
ansible-playbook -i inventories/production/production.ini site.yaml --ask-vault-pass
```