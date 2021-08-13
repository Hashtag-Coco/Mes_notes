## TODO : l'indentation et mettre les commandes en gras
# Mes notes pour la LPIC1
------------------- Pour chaque commande, se référer au man pour les options ---------------------

-> Linux est un noyau (kernel en anglais). GNU linux est l'ensemble de l'OS.

-> coco@debian:~$ = nom utilisateur @ nom de la machine ~ est le répertoire courant.

## Commande GNU/unix
-> nomdelacommande -options option (format BSD) --options argument1 "argument 2"</br></br>

CD = se déplacer (~ repertoire personnel ; / racine ; . répertoire courant ; .. répertoire parent ; - dernier répertoire visité)</br>
LS -al = lister le contenu ( a affiche tous les fichiers ; l affiche le type du fichier, les permissions, le nombre de lien physique, l'horodatage, la taille en octet, le propriétaire et le groupe) </br>
mount -to = monter un système (t pour le type de SDF ; o pour options) (le fichier /etc/fstab contient les info des SDF)</br>
ps -eF = afficher l'ensemble des processus actifs ( e pour )</br>
man 1 <commande> = aide intégré à linux </br>
  1 - Programmes executables ou commandes de l'interpréteur de commandes (shell)</br>
  2 - Appels système</br>
  3 - Appels de bibliothèque (fonctions fournies par les bibliothèques des pro-grammes)</br>
  4 - Fichiers spéciaux (situés généralement dans /dev)</br>
  5 - Formats des fichiers et conventions (ex : /etc/passwd)</br>
  6 - Jeux</br>
  7 - Divers (y compris les macropaquets et les conventions) (ex : man(7), groff(7))</br>
  8 - Commandes de gestion du système (généralement réservées au super utilisateur)</br>
  9 - Sous programmes du noyau</br>
whereis -b <commande> = voir les fichiers liés à une commande</br>
info <commande> = même commande que man</br>
type = type du fichier</br></br>

-> variable = association d'une clé à une valeur en mémoire. (par défaut : local)  (exemple : mavariable="bonjour" ; echo $mavariable ; echo ${mavariable})</br></br>

export <référence> = envoi une référence dans l'environnement</br>
unset <reference> = supprime la référence de l'environnement</br></br>

variables de paramètres : $1, $2, $3 enregistrent les arguments passés à une commande ; $0 enregistre la commande ayant permis de lancer le programme ; $* enregistre tout les arguments ; $# enregistre le nombre d'arguments</br></br>

-> Une commande est un programme ou une partie d'un programme. (identifié dans la variable d'environnement $PATH)</br></br>

pwd = savoir ou on est</br>
echo -ne = afficher un message (n pour ne pas faire le saut de ligne final ; e pour interprété les \)</br>
exec [commande [arguments]] = permet de lancer un programme en arrière plan</br></br>

Nommage : tilde en fin de fichier = fichier de sauvegarde</br></br>

Globbing = ? * [a-z]</br></br>

cp = copie d'un fichier</br>
mv = déplacer ou renommer un fichiers</br>
rm -i = supprimer un fichiers</br>
touch = créer un fichier vide</br>
mkdir = créer un répertoire</br>
rmdir = supprimer un répertoire</br>
ln -s = créer un lien symbolique</br></br>

STDIN = info qu'on donne à un programme</br>
STOUT = info que nous renvoi le programme</br>
STERR = info que nous renvoi les erreurs du programme</br></br>

Redirections : > stdout vers un fichier ; >> stdout à la suite d'un fichier ; 2> stderr vers un nouveau fichier ; 2>> stderr à la suite d'un fichier ; &> stdout + stderr ; < stdin depuis un fichier ; << stdin à partir d'une chaine de caractère ; <> stdin et stdout vers et depuis le meme fichier</br></br>

-> fichier sans extension sur GNU linux = fichier texte</br></br>

xargs = permet d'employer chaque sortie d'un programme comme argument d'un autre ( exemple : ls |xargs rm )</br>
\` = permet de remplacer de manière itérative un argument par les sorties d'une commande ( exemple : rm `ls` )</br></br>

cat = voir le contenu d'un fichier</br>
join = fusionne les lignes de deux fichiers</br>
paste = regrouper les lignes de différents fichiers</br>
expand = converti les tabulations en espaces</br>
unexpand = inverse de expand</br>
sort = trier les lignes d'un fichier</br>
split = découper un fichier</br>
tr = traduire ou éliminer des caractères</br>
uniq = élimine les lignes en doublons</br>
fmt = équivalent de cat mais avec un meilleur découpage.</br>
nl = numérote les lignes d'un fichier</br>
head = Affiche les 10 premières lignes d'un fichier</br>
tail = Affiche les 10 dernières lignes d'un fichier</br>
less = Affiche un fichier page par page</br>
cut = supprimer une partie de chaque ligne d'un fichier</br>
wc = afficher le nombre d'octets, de mots et de lignes d'un fichier.</br>
grep -iE = rechercher dans un fichier</br>
sed = modifier le contenu d'un fichier/flux ligne par ligne</br></br>

## Gestion des logiciels

dpkg -iRGEc --configure = gestionnaire de paquet debian (R mode recursif / G ne pas installer si une version plus récente du paquet est déjà installée / E ne pas installer si déjà présent/ c chercher les paquets partiellement installés)</br>
rpm -iVU --allmatches = gestionnaire de paquet</br>
yum update/upgrade/check-update/localupdate/info/remove/install/clean  = gestionnaire de paquet</br></br>

apt = gestionnaire de paquet dont la config est /etc/apt/sources.list</br>
apt-cache pkgnames <nom du paquet> = Manipuler le cache des paquets (voir lesquels sont installés)</br>
apt-get update/check/clean/install/remove/dist-upgrade = Manip des paquets</br></br>

## Configuration du matériel

BIOS : Basic Input Output System, dans la ROM , permet le démarrage du système</br>
IRQ : interruptions matérielles, permet au proc de gérer plusieurs programmes à la fois (permet au proc de suspendre des processus afin de s'occuper d'autre processus)</br>
Port d'E/S : entrées/sorties, est un espace mémoire fixe et unique qui permet la communication entre le CPU et le périphérique (/dev/ttyS0 sous linux)</br>
cat /proc/ioports = voir les adresses port E/S</br>
Adresse DMA : système d'accès direct à la mémoire par les périphériques (disposer comme une zone tampon).</br>
cat /proc/dma = voir les dma</br></br>

procfs : système de fichier virtuel destiné à la gestion des processus</br>
/proc/acpi /proc/acpi /proc/bus /proc/cpuinfo /proc/interrupts /proc/kcore /proc/meminfo : dossier/fichier avec des informations</br>
lspci = info sur les PCI</br>
swapon -s = résumé par disque de l'utilisation de la swap</br>
free = quantité totale de mémoire & swap libres et utilisées</br>
sysctl = modifier /proc/sys ; paramètres du kernel au lancement</br>
lsmod = voir les modules chargés en mémoire</br>
dmesg = tampon des messages kernel</br>
uname -a = version du système</br>
uptime = depuis combien de temps le sys est lancé</br></br>

sysfs : pareil que procfs mais une meilleur gestion des parents/enfants</br>
/sys/devices/ /sys/module/ /sys/block/power</br></br>

udev : fait le lien entre sysfs et les infos données par l'utilisateur</br>
/dev/null /dev/zero /dev/full /dev/random</br></br>

insmode <chemin vers le module> = charge un seul et unique module</br>
modprobe <nom du module> -vnrl --show-depends = charge un module (v pour verbose ; n pour test ; r pour décharger un module ; l pour lister les modules disponibles)</br>
rmmod <nom du module> -vfw = permet de liberer de la mémoire (v pour verbose ; f force ; w wait)</br></br>

/dev/sdx : disque dur x</br></br>

Partageabilité des fichiers/dossiers : shareable (partageable entre ordinateurs) unshareable (informations spécifiques du système)</br>
Fichiers/dossiers : static (modifié uniquement par intervention direct de l'admin) variable ( modifiable par les users, scripts ...)</br></br>

Dossier linux :</br>
      /bin : contient les binaires, executables et commandes pour tous les utilisateurs</br>
      /sbin : pareil que bin sauf qu'il contient les commandes sensibles (exclusivement avec root).</br>
      /lib : contient les librairies (fonctions partager par un ensemble de commande)</br>
      /boot : Contient les fichiers liés au démarrage (au lancement du système)</br>
      /usr : Contient tous les fichiers non nécéssaire au fonctionnement minimale du système</br>
      /opt : Contient des programmes optionnel</br>
      /etc : contient les fichiers de configurations</br>
      /srv : contient les données nécéssaire pour les services du système</br>
      /home : correspond aux données des utilisateurs spécifiques</br>
      /root : répertoire de l'admin</br>
      /var : contient des données variables (mail, log ...)</br>
      /tmp : fichier temporaire</br>
      /mnt : monter les DD etc</br>
      /media : monter les media amovibles</br></br>

dd = copie d'un fichier venant d'une image etc ..</br>
losetup = voir les périphérique de type loop</br></br>

fdisk -dlmnpqtvw = partionnement de disque (d destruction d'une partition ; l liste les types de patitions ; m impression du menu en cours ; n création d'une nouvelle partition ; p affichage des partitions ; q sortie de fdisk ; t modification du type de partiton ; v verif de la table des partitions ; w sauvegarde et quitte fdisk)</br></br>

Système de fichier : structure de données qui permet au système de lire et modifier les données. Stocker et lire des fichiers via un chemin d'accès.</br>
Format de SDF:</br>
      Petit espace => ext2</br>
      Partition démarrage => ext3 ou 4</br>
      Pour dossier volumineux => reiserfs</br>
      Performance élever dans tous les contextes, meilleur option pour base de données => JFS</br>
      Pour énormément de données => XFS ou ext4</br>
      Format reconnu par tout OS => FAT</br>
      DVD-ROM; blue-ray => UDF</br></br>

mkfs -t fstype partition = créer un système de fichier</br>
dumpe2fs -h = récupérer des informations (h pour infos général)</br>
tune2fs -c -i -j = modifier certains paramètres (c compteur de verification; i intervalle de verification ; j pour journalisation ; m et r pour les block réservés )</br>
debugfs = dumpe2fs + tune2fs rassemblés (stats ; lsdel ; undel ; stat ; write ; lr ; quit)</br></br>

fsck -ACVNt = vérifier l'intégrité d'un SDF (A vérifie les SDF marqué "à vérifier" dans /etc/fstab ; C indique une barre de progression ; V verbose ; N test ; t forcer le type de fs)</br></br>

mount -arvwtLUo = associer un fs avec un répertoire (a all ; r ro; v verbose ; w rw ; t fstype ; L label ; U uuid ; o paramètres)</br>
umount -afrt = démonter le fs (a all ; f force ; r si echec, remonter en ro ; t fstype)</br>
/etc/fstab : configuration automatique de montage d'un FS</br></br>

## Gestion des fichiers
ls -n = lister les groupes</br>
chown -R = modifier le propriéaire d'un fichier/dossier (R recursif) (ex : chown root:root mondossier/)</br>
chgrp = modifier le groupe d'un fichier/dossier</br></br>

typecode : - fichier ; d répertoire ; l lien symbolique ; p pipe ; s socket ; b périphérique bloc ; c périphérique caractère</br>
SGID : éxécuter un fichier avec les permissions du groupe propriétaire (n'importe qui)</br>
SUID : éxécuter un fichier avec les permissions du propriétaire (n'importe qui)</br>
sticky bit : différence entre droit d'écriture et de suppression, sur un dossier seul le proprio peut le supprimer.</br>
chmod 777 dossier ; chmod u+x ; chmod g+w ; chmod o-r = Mettre les permissions sur le dossier</br>
chmod 7777 = la colonne tout a gauche représente : sgt (avec les même valeurs octales (4 pour s 2 pour g et 1 pour t)(s pour SUID g pour SGID et t pour le sticky bit))</br>
chmod u+s = met le SUID</br>
chmod +t dossier = met le sticky bit</br>
T ou S sur le fichier => cela veux dire que l'utilisateur a le sticky bit ou SUID MAIS sans le droit d'execution</br></br>

getfacl = voir les acl d'un fichier</br>
setfacl = créer une acl, voir le MAN (ex : setfacl -m g:GROUPE:rwx fichier ; setfacl -m u:moi:rwx fichier)</br>
setfacl -bkx = supprimer une acl (b toutes les acl ; k uniquement les permissions par défaut ; x une acl)</br>
Masque : droit maximal pour une acl sur un fichier</br></br>

umask : droit par défaut lors de la création d'un fichier (droit par defaut fichier : 0666 dossier : 0777)</br>
umask -Sp = Afficher les droits par défaut (S pour le format classique ; p pour la forme octal (celle qui sera assigné) )</br>
umask 7777 = modifier l'umask</br></br>

inode : numéro attribué à chaque fichier, stocké dans la table des inodes, block du DD qui regroupe les informations d'un fichiers.</br>
hard link : pointeur sur des données physiques d'un volume de stockage</br></br>

Quota : limite de l'espace d'un utilisateur, hard ou soft,</br>
cat /etc/fstab = voir si quota d'un disque est activé</br>
quotacheck -a = Initialiser, mettre a jour, vérifier les quotas (a pour tout les points de montage)</br>
edquota <user> = modifier les quotas</br>
repquota = afficher les quotas déjà mis en place</br></br>

find -name -perm -size -gid -uuid -maxdepth -type -ok -exec ls; = rechercher des fichiers</br>
#find . \(-name 'test1' -o -name 'test2'\)</br>
locate = rechercher des fichiers, voir son man</br>
updatedb = mettre a jour locate</br></br>

## Démarage du Système
  
-> BIOS se charge (POST (test de présence et d'intégrité de tout, attribut les ressources nécéssaire) -> MBR (routine de démarrage) -> Bootloader (chargeur d'amorcage) -> kernel + initrd -> linuxrc (chargement des modules et montage de la véritable racine) -> init (lance les processus))</br>
grub-install <disque_ou_partition> = install du grub, généralement /dev/sda ou /dev/sda1</br>
/boot/grub/menu.lst ou grub.conf : fichier de configuration de grub 1/legacy</br>
apt-get install grub-pc = install grub2</br>
apt-get install grub-legacy = passer de grub2 à grub legacy</br>
/etc/default/grub  /boot/grub/device.map  /etc/grub.d  : configuration grub2</br></br>

init : premier et dernier processus, il charge tout les autres processus.</br>
systemd, upstart, sysVinit : équivalent à init</br>
service/démon  : processus qui s'execute en arrière plan, directement géré par init</br>
/etc/init.d : script bash</br>
service <script> <commande> = arrêter/voir/lancer un service ( ex : service ssh status)</br>
runlevel : détermine quels services sont lancés ou stoppés dans un contexte donné, voir le tableau.</br>
/etc/inittab : config de init</br>
chkconfig --list <service> = lister les associations services/runlevel</br>
chkconfig --level [0123456] service [on/off/reset] = modifier le comportement d'un service pour un ou plusieurs runlevels</br>
chkconfig --add <service></br>
update-rc.d <service> remove = désactiver un service</br>
update-rc.d <service> defaults = ajouter un service</br>
update-rc.d <service> start XX 2 3 4 5 . stop XX 0 1 6 = modifier le comportement d'un service pour un ou plusieurs runlevels (XX est la priorité)</br>
runlevel = affiche le runlevel</br>
init <0123456Qq>  //  telinit <0123456Qq> = changer de runlevel</br>
shutdown [-rhc] time ["Warning Message"]   //    halt / # reboot / # poweroff  = eteindre ou redemarrer (ex : shutdown -h +60 "Attention l'ordi va stopper")</br></br>

## Gestion des processus

processus : programme en cours d'execution</br>
pstree f -wfljuv = voir les processus actifs sous formes d'arbre père/fils (f pour forest ; w ne pas tronquer ; -f full ; l long ; j job control ; u orienté utilisateur ; v mémoire virtuelle)</br>
ps -Uu <user> = filtrer par utilisateur (-U = Real User ID ; -u = Effective User ID)</br>
ps -c <cmdlist> = filtre par commande</br>
ps -o speclist = spécificateurs standards de format (voir man)</br></br>

top -dpn = afficher les processus (d delay ; p pid ; n iter)</br>
jobs = afficher les processus de la session</br>
<commande> & = lance la commande en arrière plan</br>
fg = passer le dernier processus en avant plan</br>
renice priority -pgu = modifier la priorité d'un processus (p pids ; g gid ; u user)</br></br>

kill -l = voir les signaux</br>
man 7 signal = liste des signaux avec description</br></br>

nohup <commande> = lancer un programme persistant, continue à fonctionner même après déconnection</br></br>

##  Configuration de l'environnement graphique
  
Présentation : Kernel > système de fenêtrage (X window system)(Xorg) > gestionnaire de fenetre (WM)(metacity, openbox) > Environnement de bureau (DE)(KDE, gnome) > interface graphique (gnome shell, unity kde plasma)</br></br>

serveur x : fonctionne en client/serveur via le protocole XDMCP</br>
    serveur x : gestion de l'affichage et des entrées</br>
    client x : chaque application affichant un ou des fenêtres</br></br>

/etc/X11/xorg.conf : fichier de conf Xorg</br>
xorg -configure = génère un fichiers</br>
xdpyinfo =</br>
xwininfo = info sur une fenetre</br>
/etc/X11/xdm/ : configuration de XDM (c'est un display manager)</br>
  xdm-config : conf generale</br>
  xaccress : hotes autorisés pour une connection XDMCP distante</br>
  xservers : hotes (serveurs x) déléguant l'invite d'authentification à notre machine</br>
  xressources : propriétés X utilisées par les composants visuels</br>
/etc/X11/gdm : configuration de gdm (c'est un display manager)</br>
  gdmconfig = fais la conf</br></br>

Session à distance :</br>
    iptable -F  = laisse passer tout le trafic</br>
    xhost +<adresse IP> = rajoute l'hote distant aux hotes acceptés</br>
    export DISPLAY=<adresse IP> = sur l'hote client</br></br>


## Gestion des imprimantes et impressions

Ghostscript : interpreteur PS et PDF, conversion vers le format natif des imprimantes</br>
lpr -P -# n -J job -m -hr <fichier> = commande d'impression (P imprimante ; r supprimer le fichier après impréssion ; h pas de page de garde ; J précise le nom de tâche ; m mail après impression ; # n nombre de copie)</br>
cups : gestionnaire d'impression (c'est lui qui convertit)</br>
lpr > spooling (file d'attente (mémoire tampon)) > cupsd > impression</br>
cupsd : démon de cups</br>
lpstats -h -p = voir le nom de l'imprimante (h hostname ; p imprimante)</br>
lpq -P <nom> = informations sur une file d'impression</br></br>

apt-get install cups-pdf = installer une imprimante virtuelle</br>
lprm -P - = annuler une tâche d'impression (P spécifier un spool ; - tout supprimer)</br></br>

lpadmin -dpx destination -v = configurer les imprimantes (-d defaut ; p ajouter ou modifié ; x supprimer ; -v adresse de l'imprimante)</br>
serveur web d'administration : http://localhost:631</br></br>

cupsenable <printer> = activer une imprimante</br>
cupsdisable <printer> = désactiver l'imprimante</br></br>

fichier PPD : description d'une imprimante postscript</br>
/etc/cups/cupsd.conf : fichier de configuration de cups</br></br>


## Administration système

newgrp <groupe> = changer d'identifiant de groupe en cours de session</br>
groups = afficher le groupe principal puis les groupes auquels on appartient</br>
UID et GID : 0-99 outils et fonctions spécifiques système ; 100-500 ou 1000 : fonctions spécifiques liées à la distribution. (ex : GID 100 = users par défaut)</br>
cat /etc/passwd = voir l'uid et le gid d'un utilisateur</br>
cat /etc/shadow = fichier contenant les mots de passes utilisateurs</br>
cat /etc/gshadow = fichier contenant les mots de passes des groupes</br></br>

useradd = ajouter un utilisateur (voir man)</br>
usermod = modifier un utilisateur (voir man)</br>
passwd = modifier le mot de passe</br>
chage = modification des paramètres</br>
userdel = supprimer un utilisateur</br>
groupadd = ajouter un groupe</br>
groupmod = modifier un groupe</br>
gpasswd = modifier le mot de passe du groupe</br>
groupdel = supprimer un groupe</br></br>

klogd : log pour le kernel</br>
syslogd : log pour les applications</br>
rsyslog : klogd + syslogd</br>
debug,info,notice,warning,err,crit,alert,emerg : importance du message</br>
authpriv,cron,kern,lpr,mail,news,syslog,user,uucp,daemon,local : définie l'origine générant le message</br></br>

/etc/syslog.conf : configuration de syslogs</br>
/var/log  : dossier qui détient plein de fichier log</br></br>

logger = faire des logs manuels</br></br>

Horloge matériel : dans la carte mère avec la pile.</br>
Horloge système : au démarrage, il se cale sur l'horloge matériel et il sera utilisé par le système d'exploitation</br>
UTC : temps universel, GMT c'est basé sur Greenwich</br>
/etc/localtime : configuration de l'heure</br>
/etc/timezone : fichier en plus sur debian (doit avoir Europe/Paris)</br>
date -u = modifier et consulter l'horloge système (-u temps universel)</br>
Protocole NTP : protocole de synchronisation d'heure dans un réseau</br>
hwclock = afficher l'heure matérielle</br>
hwclock --set --date=date = modifier l'heure matérielle (date au format "01/01/13 00:00")</br>
hwclock -s = mettre l'heure système à l'heure de l'horloge machine</br>
hwclock -W = mettre l'heure matérielle à l'heure système</br></br>

cron : faire une tâche planifié ()</br>
/etc/crontab = mettre en place des tâches planifiées pour les tâches d'administrations</br>
### tar -cvzf <destination> /home</br>
crontab -l = voir les tâches planifier de l'utilisateur courant</br>
crontab -e = fichier config des tache planifier pour l'utilisateur courant</br>
/etc/init.d/cron : service</br></br>

anacron : lancer des tâche tous les jours/semaines/mois</br>
/etc/anacrontab : fichier de configuration d'anacron</br></br>

at : plus simple pour mettre une tâche planifiée</br>
atq = voir les tâches de l'utilisateur courant</br>
at <heure date> = faire une tâche planifié (at 20:00 12/25/13), écrire les commandes, puis ctrl+D</br>
atrm <id> = supprimer la tâche planifiée</br>
atd : démon de at</br></br>

## Administration réseaux

ifconfig = ancienne commande</br>
ip [OPTIONS] OBJECT {COMMAND | help} = Commande centralisé pour de l'administration réseau</br>
ip a s = lister les interfaces dispo</br>
ip link set dev <interface_name> address <mac_address> = modifier son adresse mac</br>
ip link set dev <interface_name> up = active l'interface réseau spécifiée</br>
interface : ethernet(eth ou em ou p<slot>p<port>), wifi(wlan ou ra ou ath), virtuelle de tunneling(tun ou tap), boucle locale(lo), modem/3G(ppp ou pppoe), virtualbox(vboxnet)</br>
iwlist wlan0 scan = lister les réseaux accéssibles</br>
iwconfig = afficher la configuration actuelle des interfaces réseaux</br>
iwconfig wlan0 essid <SSID> = s'associer à un réseau</br>
iwconfig wlan0 key open = se connecter à un réseau ouvert</br>
iwconfig wlan0 key <clé wep> = se connecter à un réseau avec une clef wep</br>
wpa_supplicant -c mon_wpa.conf -i wlan0 = se connecter à un réseau WPA</br>
contenu du mon_wpa.conf :</br>
  network={
    ssid="<ssid du réseau>"
    proto=WPA RSN
    key_mgmt=WPA-PSK
    psd="<mot de passe>"
  }</br></br>

dhclient <interface> = mettre l'interface en dhcp</br>
dhcpcd = client deamon DHCP</br>
dhcpd = serveur daemon de DHCP</br>
ifconfig <interface> <adresse IP> netmask <masque> = mettre une adresse ip à une interface</br>
ip addr add <adresse IP>/<netmask> dev <interface></br>
ip addr del <adresse IP>/<netmask> dev <interface></br>
/etc/network/interfaces : fichier de configuration réseau permanent</br></br>

ip route get 8.8.8.8 = savoir par ou passent les paquets pour aller à 8.8.8.8</br>
route -n = voir les routes déjà configurées</br>
ip route add default via <adresse IP> dev <interface> = ajouter une route</br>
ip route d default = supprimer une route par defaut</br>
ip route change default via <adresse IP> dev <interface> mtu 500 hoplimit 10 = changer le mtu et ttl d'une route</br>
ip route show = voir les routes</br></br>

arp -s <adrese IP> <adresse mac> = ajout d'une entrée statique dans la table arp</br>
arp -d <adresse IP> = supprimer une entrée de la table arp</br>
arp -va = lister les entrées</br>
ip neigh show = voir la table arp en iproute2</br>
ip neigh add <adresse ip> dev <interface> lladdr <adresse mac> = ajouter une entrée arp en iproute2</br>
ip neigh del <adresse ip> dev <interface> = supprimer une entrée en iproute2</br></br>

/etc/hosts : fichier de configuration du dns local</br>
/etc/host.conf : contient les manières de résolution de nom (ordre lors d'une demande)</br>
hostname = affiche le nom d'hote</br>
hostname <nom> = change de nom d'hote temporaire</br>
/etc/hostname = changer le nom d'hote mais de façon persistente</br>
/etc/resolv.conf : spécifier les serveurs dns</br></br>


## Connaissances complémentaires (script bash, BDD, mailing)

mavariable="valeur"</br>
paramètres de position : $0, $1, $2, $3...</br>
valeur de sortie de la dernière commande : $?</br>
PID du processus de script : $$</br>
Shebang : indique d'un fichier est un script</br>
test = pour faire des tests en cmdline</br>
expr ou let = calcul mathématique</br>
commande : séquentielle (cmd1 ; cmd2), parallèle(cmd1 & cmd2), sur erreur(cmd1 || cmd2), sur succès(cmd1 && cmd2)</br>
PATH=$PATH:/home/nom/bin : modifier la variable d'environnement PATH</br></br>

apt-get install mysql-server mysql-client = installer MySQL</br>
mysqld : démon mysql</br>
mysql -u root -p = se connecter à la base de données</br>
apt-get install postgresql postgresql-client = installer PostgreSQL</br>
GESTION DES BASES DE DONNEES :</br>
    CREATE DATABASE nom;  créer la base de données nom</br>
    SHOW DATABASES;  afficher les bases de données</br>
    USE nom;  utiliser la base de données nom</br>
    SHOW TABLES;  afficher les tables de la base courante</br>
    CREATE TABLE tbl_name;  créer la table tbl_name</br>
    INSERT INTO tbl_name VALUES ;  ajouter du contenu dans la table</br>
    SELECT colonne FROM table;  affiche le contenu d'une table</br>
    UPDATE tabl_name SET col_name1=valeur1;  modifier des enregistrements</br>
    DELETE FROM table_name;  supprimer des enregistrements</br></br>

MUA : client mail (ex : Thunderbird)</br>
MAA : mail acess agent, permet la récupération de mail en imap ou pop</br>
MTA : mail transfere agent, serveur de transmission</br>
MSA : mail submission agent, s'occupe de l'adressage, de la validité de l'adresse, des corrections sur l'en-tête</br>
MDA : mail delivery agent, se charge de répartir les mails dans les boites mails des utilisateurs</br>
Protocole LMTP : permet d'envoyer les mails du MTA au MDA</br>
Protocole POP (mails couper et coller sur l'util) ou IMAP (mails toujours sur le serveurs): permet d'envoyer les mails du MDA au MUA</br>
Sendmail, Postfix, Exim, qmail : Solutions coté serveur linux (MTA)</br>
mail <adresse> = envoyer un mail</br>
mail = voir les mails reçus</br>
mailq = vérifier la liste d'attente</br>
/etc/aliases ou /etc/mail/aliases : Redirections</br></br>

## Sécurité

nmap -sT -sU : Rechercher les ports ouverts (sT TCP ; sU UDP)</br>
nestast = afficher les connections actives</br>
sysVinit & runlevels : désactiver les services inutiles</br>
Super serveur (service dispatcheur) : permet de lancer sur commande un service, il se base sur Inetd et Xinetd</br>
  Inetd :</br>
  Xinetd : Plus sécurisé que Inetd</br>
type de socket :</br>
  TCP = stream</br>
  UDP = dgram (datagram)</br>
  ICMP = ro</br></br>

tcp wrapper : outils qui permet de controler les accès aux démons d'un serveur</br>
  En gros, vu de loin par un aveugle : Deux fichiers pour allow ou deny des hosts/réseaux sur un protocole /etc/hosts.allow et /etc/hosts.deny</br></br>

Bonne pratique mot de passe : Changer régulièrement / compliqué / ne pas avoir de sens</br>
Limiter l'accès root : su -c "commande"</br>
Configurer sudo et voir quel user peut lancer quelles commandes : /etc/sudoers</br>
Limiter l'usage des ressources : pam_limits</br>
configurer pam_limits = /etc/security/limits.conf</br>
ulimit = prévenir les problèmes accidentel</br>
/etc/nologin = interdit la connexion à tout autre utilisateur que root</br></br>

------------------- GPG</br>
Chiffrement par clefs symétriques : Même clef pour l'emetteur et le recepteur, même clef pour chiffrer et déchiffrer.</br>
  gpg -c <fichier></br>
  gpg -o <fichier> -d <fichier.gpg></br>
Chiffrement par clefs asymétriques : Permet a la fois de chiffrer et de signé. Système de clef publique (n'importe qui pourra chiffrer) et de clef privé (nous seuls)</br>
  gpg --gen-key</br>
La signature : Vérifier qu'on est bien la personne qui envoie la données</br>
certificat de révocation : permet de remplacer une clé publique ne devant plus être utilisée (pour cause d'expiration ou de vol ..)</br>
  gpg --output revoke.asc --gen-revoke name</br>
fingerprint : empreinte digitale d'une clé publique (résumé)</br>
  gpg --fingerprint <Nom></br>
Gestion des clés :</br>
  gpg --export --armor <nom> > gpg.pub = exporter une clé (armor pour que çe soit lisible)</br>
  gpg --import <filename> = importer une clé</br>
  gpg --list-keys = lister les clés</br>
  gpg --delete-key <name> = supprimer la clé</br>
Signature :</br>
  signer = gpg --clearsign <original-file></br>
  import = gpg --verify <received-file></br>
