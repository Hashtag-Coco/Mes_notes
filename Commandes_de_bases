###################################################################### Linux
#### Connaitre l'OS
cat /etc/issue
cat /etc/*-release
cat /proc/version
uname -a
rpm -q kernel
dmesg | grep Linux
ls /boot | grep vmlinuz-
lsb_release -a

#### Processus 
ps auxww
ps -ef

#### Fichier actuellement ouvert 
lsof -i

#### Port ouvert
netstat -laputen

#### Info réseau
cat /etc/network/interfaces
cat /etc/sysconfig/network
cat /etc/resolv.conf
cat /etc/sysconfig/network
cat /etc/networks

#### User
last
cat /etc/passwd | cut -d: -f1
grep -v -E "^#" /etc/passwd | awk -F: '$3 == 0 { print $1}'
ls /home/

#### Voir les tâches planifiées
crontab -l
cat /etc/cron*

#### Connaitre les permissions 
sudo -l
cat /etc/sudoers

#### Voir les partitions
df -h

#### Password mining
history
cat ~/.bash_history
cat ~/.nano_history
cat ~/.atftp_history
cat ~/.mysql_history
cat ~/.php_history
ls -l /etc/passwd
ls -l /etc/shadow
grep -RiIn passw / 2>/dev/null
grep -rnw '/' -ie 'pass' --color=always 2>/dev/null | grep -vi binary
grep -rnw '/' -ie 'DB_PASS' --color=always 2>/dev/null | grep -vi binary
grep -rnw '/' -ie 'DB_PASSWORD' --color=always 2>/dev/null | grep -vi binary
grep -rnw '/' -ie 'DB_USER' --color=always 2>/dev/null | grep -vi binary

[[[ cp /etc/passwd .
cp /etc/shadow .
unshadow passwd shadow > unshadowed
john --format=md5crypt unshadowed ]]]

###################################################################### Windows
#### OS
ver
wmic os get bootdevice, buildnumber, caption, freespaceinpagingfiles, installdate, name, systemdrive, windowsdirectory

#### Connaitre les drivers
DRIVERQUERY

#### Lister les disques
wmic logicaldisk get name, deviceid, volumename, description

#### Lister les partages
wmic share list

####Info sur le réseau
ipconfig /all

#### Lister les ports ouverts
netstat -ano

#### Lister les utilisateurs
net users

#### Lister les groupes
net localgroup 

#### Lister les processus / créer un processus / détruire un processus
wmic process list brief
wmic process call create {commande}
wmic process where processid="{pid}" delete

#### Lister les taches planifiées
schtasks /query /fo LIST /v
