# TP4-Reseau
---

**Préparation d'une VM "patron"**

J'ai supprime ma première VM, j'ai crée une nouvelle j'ai effectue cette configuration 

**configuration VM**
+ créer une VM
+ 512 Mo RAM
+ 1 CPU
+ Réseau
+ une carte NAT
+ Stockage
+ disque de 8Go
+ .iso de CentOS 7 (sur le "contrôleur IDE")

**Désactivation de SELinux**

sudo setenforce 0 # temporaire
sudo sed -i 's/enforcing/permissive/g' /etc/selinux/config # permanent

+ `Selinux désactiver ok`

**Mise à jour des dépôts**

sudo yum update -y

+ `good`

**Installation de dépôts additionels**

sudo yum install -y epel-release

**Installation faite, jai juste du mettre ma VM en réseau car il n'y avait pas de réseau** 

+ `Installation Terminé !`

 **Installation de plusieurs paquets réseau dont on se sert souvent**
 
sudo yum install -y traceroute bind-utils tcpdump nc nano

 **Désactivation de la carte NAT au reboot**
 
sudo nano /etc/sysconfig/network-scripts/ifcfg-enp0s3

 mettre ONBOOT à NO
+ `ONBOOT ON`

`(réaliser avec 'Etienne')`

**Eteindre la machine**
sudo shutdown now

+`Lancement`


# I. Mise en place du lab

Création des VMs

**configuration des Vms**

---

Créez les réseaux host-only suivants :

+ le "réseau 1" ou net1 : 10.1.0.0/24
+ la carte réseau de l'hôte doit porter l'IP 10.1.0.1
+ PAS de DHCP
+ le "réseau 2" ou net2 : 10.2.0.0/24
+ la carte réseau de l'hôte doit porter l'IP 10.2.0.1
+ PAS de DHCP

Je me suis déplacer dans "fichier" ensuite "gestionnaire de réseau hôtes"

j'ai crée deux cartes réseau 
+ 10.1.0.1
+ 10.2.0.1

on ne touche pas au `DHCP`

# 2. Création des VMs

---
**Création de nouvelles VMs**

+ VM cliente

+ VM serveur

+ VM routeur

**Création de nouvelles host-only :**

`carte réseau`

+ 10.1.0.254

+ 10.2.0.254

`client  <--net1--> router <--net2--> server`

---

**Checklist (à faire sur toutes les machines) :**

Checklist (à faire sur toutes les machines) :

 + Désactiver SELinux
déja fait dans le patron
 + Installation de certains paquets réseau
déja fait dans le patron
 + Désactivation de la carte NAT
déja fait dans le patron
 + Définition des IPs statiques
 La connexion SSH doit être fonctionnelle
une fois fait, vous avez vos trois fenêtres SSH ouvertes, une dans chaque machine
 + Définition du nom de domaine
 + Remplissage du fichier /etc/hosts
 client1 ping router1.tp4 sur l'IP 10.1.0.254
 server1 ping router1.tp4 sur l'IP 10.2.0.254
