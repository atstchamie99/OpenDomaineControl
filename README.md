# OpenDomaineControl

Nous allons configure Active Directory et un Controlleur de Domaine sous Ubuntu Server 20 avec Samba Dc.


Configurer Samba comme COntrolleur de domaine est une alternative très serieuse et logique à celui de Windows server et son Active Directory car le Controleur de Domaine Samba peut integrer des client windows(7/10/11) comme le ferai si bien celui de windows Server. D'apres le wiki de Samba fonctionne au niveau fonctionnel forestier de Windows Server 2008 R2, suffisant pour gérer des entreprises sophistiquées et repond aux exigences strictes de conformité comme le NIST 800-171 par exemple.


      Cette travail est 'une des sections d'un projet (Lab) OpenSourceInfra

Le but principale est de concevoire une infrastructure complete et fonctionel basé sur des outils opensource afin d'offrire une alternative réel et performante au outils propritaire. Le Lab sera mis regulierement mis à jour et devra respecter certaines normes, règles et critères de conformité en matière de sécurité afin que cette architecture soit adaptable a un environement de production.

            Installation et COnfiguration:

      Installation:

Nous allons configurer premièrement configurer le nom d'hôte nous allons choisir "dcm1"

            sudo hostnamectl set-hostname dcm1

Editer le fichier /etc/hosts cela n'est pas obligatoire dans l'immediat de ce fais nous allons automatiser cette tache avec un scrit et un cron a chaque demarage du serveur.

            sudo nano /etc/hosts

            entrer la ligne suivante:

            ip_du_serveur     dcm1.opensourceinfra.ats dcm1

      Installation de samba dc (dans notre cas nous travaillerons avec Ubuntu Server 20.04 LTS)

            sudo apt install samba smbclient winbind libpam-winbind libnss-winbind krb5-kdc libpam-krb5 -y



repondre au question

OPENSOURCEINFRA.ATS


Configuring Kerberos Authentication Kerberos servers for your realm:

sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak

sudo cp /etc/krb5.conf /etc/krb5.conf.bak


sudo systemctl stop smbd nmbd winbind
sudo rm -rf /var/lib/samba/*
sudo rm -rf /etc/samba/smb.conf


 samba-tool domain provision --server-role=dc --use-rfc2307 --dns-backend=SAMBA_INTERNAL --realm=OPENSOURCEINFRA.ATS --domain=OPENSOURCEINFRA --adminpass=P@ssw0rd@


![alt text](prov.png)


sudo systemctl unmask samba-ad-dc
sudo systemctl enable samba-ad-dc
sudo systemctl start samba-ad-dc


sudo cp /var/lib/samba/private/krb5.conf /etc




