# Mes notes pour la LPIC1
------------------- Pour chaque commande, se référer au man pour les options ---------------------

-> Linux est un noyau (kernel en anglais). GNU linux est l'ensemble de l'OS.

-> coco@debian:~$ = nom utilisateur @ nom de la machine ~ est le répertoire courant.

## Commande GNU/unix
-> nomdelacommande -options option (format BSD) --options argument1 "argument 2"</br>

CD = se déplacer (~ repertoire personnel ; / racine ; . répertoire courant ; .. répertoire parent ; - dernier répertoire visité)</br>
LS -al = lister le contenu ( a affiche tous les fichiers ; l affiche le type du fichier, les permissions, le nombre de lien physique, l'horodatage, la taille en octet, le propriétaire et le groupe) </br>
mount -to = monter un système (t pour le type de SDF ; o pour options) (le fichier /etc/fstab contient les info des SDF)
ps -eF = afficher l'ensemble des processus actifs ( e pour )
man 1 <commande> = aide intégré à linux
  1 - Programmes executables ou commandes de l'interpréteur de commandes (shell)
  2 - Appels système
  3 - Appels de bibliothèque (fonctions fournies par les bibliothèques des pro-grammes)
  4 - Fichiers spéciaux (situés généralement dans /dev)
  5 - Formats des fichiers et conventions (ex : /etc/passwd)
  6 - Jeux
  7 - Divers (y compris les macropaquets et les conventions) (ex : man(7), groff(7))
  8 - Commandes de gestion du système (généralement réservées au super utilisateur)
  9 - Sous programmes du noyau
whereis -b <commande> = voir les fichiers liés à une commande
info <commande> = même commande que man
type = type du fichier

-> variable = association d'une clé à une valeur en mémoire. (par défaut : local)  (exemple : mavariable="bonjour" ; echo $mavariable ; echo ${mavariable})

export <référence> = envoi une référence dans l'environnement
unset <reference> = supprime la référence de l'environnement

variables de paramètres : $1, $2, $3 enregistrent les arguments passés à une commande ; $0 enregistre la commande ayant permis de lancer le programme ; $* enregistre tout les arguments ; $# enregistre le nombre d'arguments

-> Une commande est un programme ou une partie d'un programme. (identifié dans la variable d'environnement $PATH)

pwd = savoir ou on est
echo -ne = afficher un message (n pour ne pas faire le saut de ligne final ; e pour interprété les \)
exec [commande [arguments]] = permet de lancer un programme en arrière plan

Nommage : tilde en fin de fichier = fichier de sauvegarde

Globbing = ? * [a-z]

cp = copie d'un fichier
mv = déplacer ou renommer un fichiers
rm -i = supprimer un fichiers
touch = créer un fichier vide
mkdir = créer un répertoire
rmdir = supprimer un répertoire
ln -s = créer un lien symbolique

STDIN = info qu'on donne à un programme
STOUT = info que nous renvoi le programme
STERR = info que nous renvoi les erreurs du programme

Redirections : > stdout vers un fichier ; >> stdout à la suite d'un fichier ; 2> stderr vers un nouveau fichier ; 2>> stderr à la suite d'un fichier ; &> stdout + stderr ; < stdin depuis un fichier ; << stdin à partir d'une chaine de caractère ; <> stdin et stdout vers et depuis le meme fichier

-> fichier sans extension sur GNU linux = fichier texte

xargs = permet d'employer chaque sortie d'un programme comme argument d'un autre ( exemple : ls |xargs rm )
` = permet de remplacer de manière itérative un argument par les sorties d'une commande ( exemple : rm `ls` )

cat = voir le contenu d'un fichier
join = fusionne les lignes de deux fichiers
paste = regrouper les lignes de différents fichiers
expand = converti les tabulations en espaces
unexpand = inverse de expand
sort = trier les lignes d'un fichier
split = découper un fichier
tr = traduire ou éliminer des caractères
uniq = élimine les lignes en doublons
fmt = équivalent de cat mais avec un meilleur découpage.
nl = numérote les lignes d'un fichier
head = Affiche les 10 premières lignes d'un fichier
tail = Affiche les 10 dernières lignes d'un fichier
less = Affiche un fichier page par page
cut = supprimer une partie de chaque ligne d'un fichier
wc = afficher le nombre d'octets, de mots et de lignes d'un fichier.
grep -iE = rechercher dans un fichier
sed = modifier le contenu d'un fichier/flux ligne par ligne

## Gestion des logiciels

dpkg -iRGEc --configure = gestionnaire de paquet debian (R mode recursif / G ne pas installer si une version plus récente du paquet est déjà installée / E ne pas installer si déjà présent/ c chercher les paquets partiellement installés)
rpm -iVU --allmatches = gestionnaire de paquet
yum update/upgrade/check-update/localupdate/info/remove/install/clean  = gestionnaire de paquet

apt = gestionnaire de paquet dont la config est /etc/apt/sources.list
apt-cache pkgnames <nom du paquet> = Manipuler le cache des paquets (voir lesquels sont installés)
apt-get update/check/clean/install/remove/dist-upgrade = Manip des paquets
=================================================================================================================================
================================================================================================================================= Configuration du matériel

BIOS : Basic Input Output System, dans la ROM , permet le démarrage du système
IRQ : interruptions matérielles, permet au proc de gérer plusieurs programmes à la fois (permet au proc de suspendre des processus afin de s'occuper d'autre processus)
Port d'E/S : entrées/sorties, est un espace mémoire fixe et unique qui permet la communication entre le CPU et le périphérique (/dev/ttyS0 sous linux)
cat /proc/ioports = voir les adresses port E/S
Adresse DMA : système d'accès direct à la mémoire par les périphériques (disposer comme une zone tampon).
cat /proc/dma = voir les dma

procfs : système de fichier virtuel destiné à la gestion des processus
/proc/acpi /proc/acpi /proc/bus /proc/cpuinfo /proc/interrupts /proc/kcore /proc/meminfo : dossier/fichier avec des informations
lspci = info sur les PCI
swapon -s = résumé par disque de l'utilisation de la swap
free = quantité totale de mémoire & swap libres et utilisées
sysctl = modifier /proc/sys ; paramètres du kernel au lancement
lsmod = voir les modules chargés en mémoire
dmesg = tampon des messages kernel
uname -a = version du système
uptime = depuis combien de temps le sys est lancé

sysfs : pareil que procfs mais une meilleur gestion des parents/enfants
/sys/devices/ /sys/module/ /sys/block/power

udev : fait le lien entre sysfs et les infos données par l'utilisateur
/dev/null /dev/zero /dev/full /dev/random

insmode <chemin vers le module> = charge un seul et unique module
modprobe <nom du module> -vnrl --show-depends = charge un module (v pour verbose ; n pour test ; r pour décharger un module ; l pour lister les modules disponibles)
rmmod <nom du module> -vfw = permet de liberer de la mémoire (v pour verbose ; f force ; w wait)

/dev/sdx : disque dur x

Partageabilité des fichiers/dossiers : shareable (partageable entre ordinateurs) unshareable (informations spécifiques du système)
Fichiers/dossiers : static (modifié uniquement par intervention direct de l'admin) variable ( modifiable par les users, scripts ...)

Dossier linux :
      /bin : contient les binaires, executables et commandes pour tous les utilisateurs
      /sbin : pareil que bin sauf qu'il contient les commandes sensibles (exclusivement avec root).
      /lib : contient les librairies (fonctions partager par un ensemble de commande)
      /boot : Contient les fichiers liés au démarrage (au lancement du système)
      /usr : Contient tous les fichiers non nécéssaire au fonctionnement minimale du système
      /opt : Contient des programmes optionnel
      /etc : contient les fichiers de configurations
      /srv : contient les données nécéssaire pour les services du système
      /home : correspond aux données des utilisateurs spécifiques
      /root : répertoire de l'admin
      /var : contient des données variables (mail, log ...)
      /tmp : fichier temporaire
      /mnt : monter les DD etc
      /media : monter les media amovibles

dd = copie d'un fichier venant d'une image etc ..
losetup = voir les périphérique de type loop

fdisk -dlmnpqtvw = partionnement de disque (d destruction d'une partition ; l liste les types de patitions ; m impression du menu en cours ; n création d'une nouvelle partition ; p affichage des partitions ; q sortie de fdisk ; t modification du type de partiton ; v verif de la table des partitions ; w sauvegarde et quitte fdisk)

Système de fichier : structure de données qui permet au système de lire et modifier les données. Stocker et lire des fichiers via un chemin d'accès.
Format de SDF:
      Petit espace => ext2
      Partition démarrage => ext3 ou 4
      Pour dossier volumineux => reiserfs
      Performance élever dans tous les contextes, meilleur option pour base de données => JFS
      Pour énormément de données => XFS ou ext4
      Format reconnu par tout OS => FAT
      DVD-ROM; blue-ray => UDF

mkfs -t fstype partition = créer un système de fichier
dumpe2fs -h = récupérer des informations (h pour infos général)
tune2fs -c -i -j = modifier certains paramètres (c compteur de verification; i intervalle de verification ; j pour journalisation ; m et r pour les block réservés )
debugfs = dumpe2fs + tune2fs rassemblés (stats ; lsdel ; undel ; stat ; write ; lr ; quit)

fsck -ACVNt = vérifier l'intégrité d'un SDF (A vérifie les SDF marqué "à vérifier" dans /etc/fstab ; C indique une barre de progression ; V verbose ; N test ; t forcer le type de fs)

mount -arvwtLUo = associer un fs avec un répertoire (a all ; r ro; v verbose ; w rw ; t fstype ; L label ; U uuid ; o paramètres)
umount -afrt = démonter le fs (a all ; f force ; r si echec, remonter en ro ; t fstype)
/etc/fstab : configuration automatique de montage d'un FS

## Gestion des fichiers
ls -n = lister les groupes
chown -R = modifier le propriéaire d'un fichier/dossier (R recursif) (ex : chown root:root mondossier/)
chgrp = modifier le groupe d'un fichier/dossier

typecode : - fichier ; d répertoire ; l lien symbolique ; p pipe ; s socket ; b périphérique bloc ; c périphérique caractère
SGID : éxécuter un fichier avec les permissions du groupe propriétaire (n'importe qui)
SUID : éxécuter un fichier avec les permissions du propriétaire (n'importe qui)
sticky bit : différence entre droit d'écriture et de suppression, sur un dossier seul le proprio peut le supprimer.
chmod 777 dossier ; chmod u+x ; chmod g+w ; chmod o-r = Mettre les permissions sur le dossier
chmod 7777 = la colonne tout a gauche représente : sgt (avec les même valeurs octales (4 pour s 2 pour g et 1 pour t)(s pour SUID g pour SGID et t pour le sticky bit))
chmod u+s = met le SUID
chmod +t dossier = met le sticky bit
T ou S sur le fichier => cela veux dire que l'utilisateur a le sticky bit ou SUID MAIS sans le droit d'execution

getfacl = voir les acl d'un fichier
setfacl = créer une acl, voir le MAN (ex : setfacl -m g:GROUPE:rwx fichier ; setfacl -m u:moi:rwx fichier)
setfacl -bkx = supprimer une acl (b toutes les acl ; k uniquement les permissions par défaut ; x une acl)
Masque : droit maximal pour une acl sur un fichier

umask : droit par défaut lors de la création d'un fichier (droit par defaut fichier : 0666 dossier : 0777)
umask -Sp = Afficher les droits par défaut (S pour le format classique ; p pour la forme octal (celle qui sera assigné) )
umask 7777 = modifier l'umask

inode : numéro attribué à chaque fichier, stocké dans la table des inodes, block du DD qui regroupe les informations d'un fichiers.
hard link : pointeur sur des données physiques d'un volume de stockage

Quota : limite de l'espace d'un utilisateur, hard ou soft,
cat /etc/fstab = voir si quota d'un disque est activé
quotacheck -a = Initialiser, mettre a jour, vérifier les quotas (a pour tout les points de montage)
edquota <user> = modifier les quotas
repquota = afficher les quotas déjà mis en place

find -name -perm -size -gid -uuid -maxdepth -type -ok -exec ls; = rechercher des fichiers
#find . \(-name 'test1' -o -name 'test2'\)
locate = rechercher des fichiers, voir son man
updatedb = mettre a jour locate

## Démarage du Système
  
-> BIOS se charge (POST (test de présence et d'intégrité de tout, attribut les ressources nécéssaire) -> MBR (routine de démarrage) -> Bootloader (chargeur d'amorcage) -> kernel + initrd -> linuxrc (chargement des modules et montage de la véritable racine) -> init (lance les processus))
grub-install <disque_ou_partition> = install du grub, généralement /dev/sda ou /dev/sda1
/boot/grub/menu.lst ou grub.conf : fichier de configuration de grub 1/legacy
apt-get install grub-pc = install grub2
apt-get install grub-legacy = passer de grub2 à grub legacy
/etc/default/grub  /boot/grub/device.map  /etc/grub.d  : configuration grub2

init : premier et dernier processus, il charge tout les autres processus.
systemd, upstart, sysVinit : équivalent à init
service/démon  : processus qui s'execute en arrière plan, directement géré par init
/etc/init.d : script bash
service <script> <commande> = arrêter/voir/lancer un service ( ex : service ssh status)
runlevel : détermine quels services sont lancés ou stoppés dans un contexte donné, voir le tableau.
/etc/inittab : config de init
chkconfig --list <service> = lister les associations services/runlevel
chkconfig --level [0123456] service [on/off/reset] = modifier le comportement d'un service pour un ou plusieurs runlevels
chkconfig --add <service>
update-rc.d <service> remove = désactiver un service
update-rc.d <service> defaults = ajouter un service
update-rc.d <service> start XX 2 3 4 5 . stop XX 0 1 6 = modifier le comportement d'un service pour un ou plusieurs runlevels (XX est la priorité)
runlevel = affiche le runlevel
init <0123456Qq>  //  telinit <0123456Qq> = changer de runlevel
shutdown [-rhc] time ["Warning Message"]   //    halt / # reboot / # poweroff  = eteindre ou redemarrer (ex : shutdown -h +60 "Attention l'ordi va stopper")

## Gestion des processus

processus : programme en cours d'execution
pstree f -wfljuv = voir les processus actifs sous formes d'arbre père/fils (f pour forest ; w ne pas tronquer ; -f full ; l long ; j job control ; u orienté utilisateur ; v mémoire virtuelle)
ps -Uu <user> = filtrer par utilisateur (-U = Real User ID ; -u = Effective User ID)
ps -c <cmdlist> = filtre par commande
ps -o speclist = spécificateurs standards de format (voir man)

top -dpn = afficher les processus (d delay ; p pid ; n iter)
jobs = afficher les processus de la session
<commande> & = lance la commande en arrière plan
fg = passer le dernier processus en avant plan
renice priority -pgu = modifier la priorité d'un processus (p pids ; g gid ; u user)

kill -l = voir les signaux
man 7 signal = liste des signaux avec description

nohup <commande> = lancer un programme persistant, continue à fonctionner même après déconnection

##  Configuration de l'environnement graphique
  
Présentation : Kernel > système de fenêtrage (X window system)(Xorg) > gestionnaire de fenetre (WM)(metacity, openbox) > Environnement de bureau (DE)(KDE, gnome) > interface graphique (gnome shell, unity kde plasma)

serveur x : fonctionne en client/serveur via le protocole XDMCP
    serveur x : gestion de l'affichage et des entrées
    client x : chaque application affichant un ou des fenêtres

/etc/X11/xorg.conf : fichier de conf Xorg
xorg -configure = génère un fichiers
xdpyinfo =
xwininfo = info sur une fenetre
/etc/X11/xdm/ : configuration de XDM (c'est un display manager)
  xdm-config : conf generale
  xaccress : hotes autorisés pour une connection XDMCP distante
  xservers : hotes (serveurs x) déléguant l'invite d'authentification à notre machine
  xressources : propriétés X utilisées par les composants visuels
/etc/X11/gdm : configuration de gdm (c'est un display manager)
  gdmconfig = fais la conf

Session à distance :
    iptable -F  = laisse passer tout le trafic
    xhost +<adresse IP> = rajoute l'hote distant aux hotes acceptés
    export DISPLAY=<adresse IP> = sur l'hote client


## Gestion des imprimantes et impressions

Ghostscript : interpreteur PS et PDF, conversion vers le format natif des imprimantes
lpr -P -# n -J job -m -hr <fichier> = commande d'impression (P imprimante ; r supprimer le fichier après impréssion ; h pas de page de garde ; J précise le nom de tâche ; m mail après impression ; # n nombre de copie)
cups : gestionnaire d'impression (c'est lui qui convertit)
lpr > spooling (file d'attente (mémoire tampon)) > cupsd > impression
cupsd : démon de cups
lpstats -h -p = voir le nom de l'imprimante (h hostname ; p imprimante)
lpq -P <nom> = informations sur une file d'impression

apt-get install cups-pdf = installer une imprimante virtuelle
lprm -P - = annuler une tâche d'impression (P spécifier un spool ; - tout supprimer)

lpadmin -dpx destination -v = configurer les imprimantes (-d defaut ; p ajouter ou modifié ; x supprimer ; -v adresse de l'imprimante)
serveur web d'administration : http://localhost:631

cupsenable <printer> = activer une imprimante
cupsdisable <printer> = désactiver l'imprimante

fichier PPD : description d'une imprimante postscript
/etc/cups/cupsd.conf : fichier de configuration de cups


## Administration système

newgrp <groupe> = changer d'identifiant de groupe en cours de session
groups = afficher le groupe principal puis les groupes auquels on appartient
UID et GID : 0-99 outils et fonctions spécifiques système ; 100-500 ou 1000 : fonctions spécifiques liées à la distribution. (ex : GID 100 = users par défaut)
cat /etc/passwd = voir l'uid et le gid d'un utilisateur
cat /etc/shadow = fichier contenant les mots de passes utilisateurs
cat /etc/gshadow = fichier contenant les mots de passes des groupes

useradd = ajouter un utilisateur (voir man)
usermod = modifier un utilisateur (voir man)
passwd = modifier le mot de passe
chage = modification des paramètres
userdel = supprimer un utilisateur
groupadd = ajouter un groupe
groupmod = modifier un groupe
gpasswd = modifier le mot de passe du groupe
groupdel = supprimer un groupe

klogd : log pour le kernel
syslogd : log pour les applications
rsyslog : klogd + syslogd
debug,info,notice,warning,err,crit,alert,emerg : importance du message
authpriv,cron,kern,lpr,mail,news,syslog,user,uucp,daemon,local : définie l'origine générant le message

/etc/syslog.conf : configuration de syslogs
/var/log  : dossier qui détient plein de fichier log

logger = faire des logs manuels

Horloge matériel : dans la carte mère avec la pile.
Horloge système : au démarrage, il se cale sur l'horloge matériel et il sera utilisé par le système d'exploitation
UTC : temps universel, GMT c'est basé sur Greenwich
/etc/localtime : configuration de l'heure
/etc/timezone : fichier en plus sur debian (doit avoir Europe/Paris)
date -u = modifier et consulter l'horloge système (-u temps universel)
Protocole NTP : protocole de synchronisation d'heure dans un réseau
hwclock = afficher l'heure matérielle
hwclock --set --date=date = modifier l'heure matérielle (date au format "01/01/13 00:00")
hwclock -s = mettre l'heure système à l'heure de l'horloge machine
hwclock -W = mettre l'heure matérielle à l'heure système

cron : faire une tâche planifié ()
/etc/crontab = mettre en place des tâches planifiées pour les tâches d'administrations
### tar -cvzf <destination> /home
crontab -l = voir les tâches planifier de l'utilisateur courant
crontab -e = fichier config des tache planifier pour l'utilisateur courant
/etc/init.d/cron : service

anacron : lancer des tâche tous les jours/semaines/mois
/etc/anacrontab : fichier de configuration d'anacron

at : plus simple pour mettre une tâche planifiée
atq = voir les tâches de l'utilisateur courant
at <heure date> = faire une tâche planifié (at 20:00 12/25/13), écrire les commandes, puis ctrl+D
atrm <id> = supprimer la tâche planifiée
atd : démon de at


## Administration réseaux

ifconfig = ancienne commande
ip [OPTIONS] OBJECT {COMMAND | help} = Commande centralisé pour de l'administration réseau
ip a s = lister les interfaces dispo
ip link set dev <interface_name> address <mac_address> = modifier son adresse mac
ip link set dev <interface_name> up = active l'interface réseau spécifiée
interface : ethernet(eth ou em ou p<slot>p<port>), wifi(wlan ou ra ou ath), virtuelle de tunneling(tun ou tap), boucle locale(lo), modem/3G(ppp ou pppoe), virtualbox(vboxnet)
iwlist wlan0 scan = lister les réseaux accéssibles
iwconfig = afficher la configuration actuelle des interfaces réseaux
iwconfig wlan0 essid <SSID> = s'associer à un réseau
iwconfig wlan0 key open = se connecter à un réseau ouvert
iwconfig wlan0 key <clé wep> = se connecter à un réseau avec une clef wep
wpa_supplicant -c mon_wpa.conf -i wlan0 = se connecter à un réseau WPA
contenu du mon_wpa.conf :
  network={
    ssid="<ssid du réseau>"
    proto=WPA RSN
    key_mgmt=WPA-PSK
    psd="<mot de passe>"
  }

dhclient <interface> = mettre l'interface en dhcp
dhcpcd = client deamon DHCP
dhcpd = serveur daemon de DHCP
ifconfig <interface> <adresse IP> netmask <masque> = mettre une adresse ip à une interface
ip addr add <adresse IP>/<netmask> dev <interface>
ip addr del <adresse IP>/<netmask> dev <interface>
/etc/network/interfaces : fichier de configuration réseau permanent

ip route get 8.8.8.8 = savoir par ou passent les paquets pour aller à 8.8.8.8
route -n = voir les routes déjà configurées
ip route add default via <adresse IP> dev <interface> = ajouter une route
ip route d default = supprimer une route par defaut
ip route change default via <adresse IP> dev <interface> mtu 500 hoplimit 10 = changer le mtu et ttl d'une route
ip route show = voir les routes

arp -s <adrese IP> <adresse mac> = ajout d'une entrée statique dans la table arp
arp -d <adresse IP> = supprimer une entrée de la table arp
arp -va = lister les entrées
ip neigh show = voir la table arp en iproute2
ip neigh add <adresse ip> dev <interface> lladdr <adresse mac> = ajouter une entrée arp en iproute2
ip neigh del <adresse ip> dev <interface> = supprimer une entrée en iproute2

/etc/hosts : fichier de configuration du dns local
/etc/host.conf : contient les manières de résolution de nom (ordre lors d'une demande)
hostname = affiche le nom d'hote
hostname <nom> = change de nom d'hote temporaire
/etc/hostname = changer le nom d'hote mais de façon persistente
/etc/resolv.conf : spécifier les serveurs dns


## Connaissances complémentaires (script bash, BDD, mailing)

mavariable="valeur"
paramètres de position : $0, $1, $2, $3...
valeur de sortie de la dernière commande : $?
PID du processus de script : $$
Shebang : indique d'un fichier est un script
test = pour faire des tests en cmdline
expr ou let = calcul mathématique
commande : séquentielle (cmd1 ; cmd2), parallèle(cmd1 & cmd2), sur erreur(cmd1 || cmd2), sur succès(cmd1 && cmd2)
PATH=$PATH:/home/nom/bin : modifier la variable d'environnement PATH

apt-get install mysql-server mysql-client = installer MySQL
mysqld : démon mysql
mysql -u root -p = se connecter à la base de données
apt-get install postgresql postgresql-client = installer PostgreSQL
GESTION DES BASES DE DONNEES :
    CREATE DATABASE nom;  créer la base de données nom
    SHOW DATABASES;  afficher les bases de données
    USE nom;  utiliser la base de données nom
    SHOW TABLES;  afficher les tables de la base courante
    CREATE TABLE tbl_name;  créer la table tbl_name
    INSERT INTO tbl_name VALUES ;  ajouter du contenu dans la table
    SELECT colonne FROM table;  affiche le contenu d'une table
    UPDATE tabl_name SET col_name1=valeur1;  modifier des enregistrements
    DELETE FROM table_name;  supprimer des enregistrements

MUA : client mail (ex : Thunderbird)
MAA : mail acess agent, permet la récupération de mail en imap ou pop
MTA : mail transfere agent, serveur de transmission
MSA : mail submission agent, s'occupe de l'adressage, de la validité de l'adresse, des corrections sur l'en-tête
MDA : mail delivery agent, se charge de répartir les mails dans les boites mails des utilisateurs
Protocole LMTP : permet d'envoyer les mails du MTA au MDA
Protocole POP (mails couper et coller sur l'util) ou IMAP (mails toujours sur le serveurs): permet d'envoyer les mails du MDA au MUA
Sendmail, Postfix, Exim, qmail : Solutions coté serveur linux (MTA)
mail <adresse> = envoyer un mail
mail = voir les mails reçus
mailq = vérifier la liste d'attente
/etc/aliases ou /etc/mail/aliases : Redirections

## Sécurité

nmap -sT -sU : Rechercher les ports ouverts (sT TCP ; sU UDP)
nestast = afficher les connections actives
sysVinit & runlevels : désactiver les services inutiles
Super serveur (service dispatcheur) : permet de lancer sur commande un service, il se base sur Inetd et Xinetd
  Inetd :
  Xinetd : Plus sécurisé que Inetd
type de socket :
  TCP = stream
  UDP = dgram (datagram)
  ICMP = ro

tcp wrapper : outils qui permet de controler les accès aux démons d'un serveur
  En gros, vu de loin par un aveugle : Deux fichiers pour allow ou deny des hosts/réseaux sur un protocole /etc/hosts.allow et /etc/hosts.deny

Bonne pratique mot de passe : Changer régulièrement / compliqué / ne pas avoir de sens
Limiter l'accès root : su -c "commande"
Configurer sudo et voir quel user peut lancer quelles commandes : /etc/sudoers
Limiter l'usage des ressources : pam_limits
configurer pam_limits = /etc/security/limits.conf
ulimit = prévenir les problèmes accidentel
/etc/nologin = interdit la connexion à tout autre utilisateur que root


------------------- GPG
Chiffrement par clefs symétriques : Même clef pour l'emetteur et le recepteur, même clef pour chiffrer et déchiffrer.
  gpg -c <fichier>
  gpg -o <fichier> -d <fichier.gpg>
Chiffrement par clefs asymétriques : Permet a la fois de chiffrer et de signé. Système de clef publique (n'importe qui pourra chiffrer) et de clef privé (nous seuls)
  gpg --gen-key
La signature : Vérifier qu'on est bien la personne qui envoie la données
certificat de révocation : permet de remplacer une clé publique ne devant plus être utilisée (pour cause d'expiration ou de vol ..)
  gpg --output revoke.asc --gen-revoke name
fingerprint : empreinte digitale d'une clé publique (résumé)
  gpg --fingerprint <Nom>
Gestion des clés :
  gpg --export --armor <nom> > gpg.pub = exporter une clé (armor pour que çe soit lisible)
  gpg --import <filename> = importer une clé
  gpg --list-keys = lister les clés
  gpg --delete-key <name> = supprimer la clé
Signature :
  signer = gpg --clearsign <original-file>
  import = gpg --verify <received-file>
