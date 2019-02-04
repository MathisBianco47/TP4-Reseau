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
 
 
 Désactivation des IPs statiques 

j'ai executer la commande `ip a`

j'ai reperer le nom de l'interface `enp0s3`

j'ai modifie le fichier correspondant à l'interface donc 
+ je rentre dans le dossier `/etc/sysconfig/network-scripts`
 ma machine m'indique que (c'est un dossier)
+ j'ai crée un fichier portant le nom de l'interface
+ j'ai rentrée quelques commande comme l'ip et le netmask que j'avais fait auparavant dans le TP dans le gestionnaires de réseau hotes
+ j'ai utilise `ifdown et ifup` à la fin de mon terminal connexion activée 

**J'ai utilise le cours pour créer ou modifier une ip statique, je vais maintenant le faire pour les 3 autres VMs.**

Je passe à la VM Cliente
je vais faire la même manipulation que pour la VM patron

sauf que je vais changer le netmask et l'ip indique plus haut 
 
`10.2.0.0`

Ils vont bien-sur avoir le même nom que la VM patron 

`enp0s3`

**sur certaines vm je devais changer !**

Checklist (à faire sur toutes les machines) : checklist faites !

# 3. Mise en place du routage statique
# 1 sur router1 :
SELinux toujours désactivé

NAT doit être désactivée (faite dans la partie 2 avec la Vm Patron)

j'ai transformer ma machine en routeur (routeur1)
j'ai active l'ipv4 avec la commande `sudo sysctl -w net.ipv4.conf.all.forwarding=1`

d'abord je commence toujours par faire `su` je me mets en administrateur 
après avoir activer l'ipv4 j'ai mis en temporaire le pare feu de ma Vm Routeur

sur ma Vm quand j'ai mis la commande `ip route show` elle est connecte
 
# 2  sur client1 :

j'ai rencontre une difficulte en laissant le pare feu ducoup j'ai fais la même manipulation et de même sa "route" de net1 à net2

j'ai fais également la même manipulation sur le serveur 1


# 4 test
