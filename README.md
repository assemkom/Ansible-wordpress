# PROJET ANSIBLE : 

1.	Automatisation avec Ansible :
o	Création playbook Ansible sur la machine « VM-Ansible » pour automatiser l’installation et la configuration de WordPress sur 2 serveur distant (node01 node02)
o	Vérifiez que WordPress est accessible via un navigateur web après le déploiement.
Réalisation :
Création de de trois VM avec des adresse ip fixes sous 
VMWare :
•	Adresse IP réseau : 192.168.8.0
•	Masque de sous-réseau : 255.255.255.0
•	Adresse IP Gateway : 192.168.8.254

VM-Ansible :
•	Adresse IP réseau : 192.168.8.24
•	Masque de sous-réseau : 255.255.255.0
•	Adresse IP Gateway : 192.168.8.254
Node01 :
•	Adresse IP réseau : 192.168.8.25
•	Masque de sous-réseau : 255.255.255.0
•	Adresse IP Gateway : 192.168.8.254
Node02 :
•	Adresse IP réseau : 192.168.8.23
•	Masque de sous-réseau : 255.255.255.0
•	Adresse IP Gateway : 192.168.8.254


-Configuration des machines VM
VM-Ansible :
passwd root
	passwd sysadmin
	hostnamectl set-hostname vm-ansible
	apt install sudo
	apt update && apt upgrade -y
	ssh-keygen -t rsa
	ssh 192.168.8.25 (connexion sur node01)
	ssh 192.168.8.23 (connexion sur node02)
	ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.8.25  ( copie de la clef vers node01)
	ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.8.23  ( copie de la clef vers node01)
NODE01:
	node-01 
	su -
	hostnamectl set-hostname node01
	passwd root
	passwd sysadmin
	hostnamectl set-hostname node01
	hostname
	apt update && appt upgrade -y
	sudo nano /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
PasswordAuthentication yes (ligne à rajouter)
	nano root.conf
PermitRootLogin yes (ligne à rajouter)
AllowUsers sysadmin root (ligne à rajouter)
	systemctl restart ssh

NODE02:
	node-01 
	su -
	hostnamectl set-hostname node01
	passwd root
	passwd sysadmin
	hostnamectl set-hostname node01
	hostname
	apt update && appt upgrade -y
	sudo nano /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
PasswordAuthentication yes (ligne à rajouter)
	nano root.conf
PermitRootLogin yes (ligne à rajouter)
AllowUsers sysadmin root (ligne à rajouter)
	systemctl restart ssh 


Cliquez ici pour taper du texte.

-Vérification des ping sur Node01 et Node02 par les adresse IP :

root@vm-ansible:~# ansible all -i 192.168.8.25, -m ping
ansible all -i 192.168.8.23, -m ping

résultat :

192.168.8.25 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
192.168.8.23 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"

