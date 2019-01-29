# TP4-Reseau
---

**Préparation d'une VM "patron"**

+ créer une VM
+ 512 Mo RAM
+ 1 CPU
+ Réseau
+ une carte NAT
+ Stockage
+ disque de 8Go
+ .iso de CentOS 7 (sur le "contrôleur IDE")

**configuration VM**

 Désactivation de SELinux
sudo setenforce 0 # temporaire
sudo sed -i 's/enforcing/permissive/g' /etc/selinux/config # permanent

+ `Selinux désactiver ok`

Mise à jour des dépôts
sudo yum update -y

+ `good`

Installation de dépôts additionels
sudo yum install -y epel-release

Installation faite, jai juste du mettre ma VM en réseau car il n'y avait pas de réseau 

+ `Installation Terminé !`

 Installation de plusieurs paquets réseau dont on se sert souvent
sudo yum install -y traceroute bind-utils tcpdump nc nano

 Désactivation de la carte NAT au reboot
sudo nano /etc/sysconfig/network-scripts/ifcfg-enp0s3

 mettre ONBOOT à NO

 Eteindre la machine
sudo shutdown now


# I. Mise en place du lab
