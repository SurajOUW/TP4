# TP4
TP4 - IP statique (routage)

## TP4 - Routage

### Définir l'ip statique

On repère le nom de l'interface que l'on veut changer grâce à la commande "ip a"

Ensuite on modifie l'interface correspondant par le chemin suivant : 
/etc/sysconfig/network-scripts/ifcfg-enp0s8
/etc/sysconfig/network-scripts/ifcfg-enp0s9
respectivement pour la machine 'client' et la machine 'serveur', on met l'adresse ip : 
10.1.0.10
10.2.0.10
et les adresses suivantes sur le routeur
10.1.0.254
10.2.0.254
Puis il faut redemarrer l'interface à chaques fois sur les VM.

### Definition des routes

Il faut ensuite écrire un script qui va créer les routes d'une adresse IP : 
10.2.0.0/24 via 10.2.0.254 dev eth0
10.1.0.0/24 via 10.1.0.254 dev eth0
On transforme la machine routeur en route pour les deux vm et on désactive les firewalls des client et serveur

echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
sudo systemctl disable firewalld


De cette façon la machine 'client'(10.1.0.1) va transmettre le message (elles vont pouvoir se ping !) à la machine routeur qui va echanger le message à la machine serveur (10.2.0.10)

Image : screen final du ping d'une machine à l'autre avec le routeur
Link : https://prnt.sc/mhhl9n
