# Linux
## Connaitre l'OS
```bash
$ cat /etc/issue
$ cat /etc/*-release
$ cat /proc/version
$ uname -a
$ rpm -q kernel
$ dmesg | grep Linux
$ ls /boot | grep vmlinuz-
$ lsb_release -a
```

## Processus 
```bash
$ ps auxww
$ ps -ef
```

## Fichier actuellement ouvert 
```bash
$ lsof -i
```

## Port ouvert
```bash
$ netstat -laputen
```

## Info réseau
```bash
$ cat /etc/network/interfaces
$ cat /etc/sysconfig/network
$ cat /etc/resolv.conf
$ cat /etc/sysconfig/network
$ cat /etc/networks
```

## User
```bash
$ last
$ cat /etc/passwd | cut -d: -f1
$ grep -v -E "^#" /etc/passwd | awk -F: '$3 == 0 { print $1}'
$ ls /home/
```

## Voir les tâches planifiées
```bash
$ crontab -l
$ cat /etc/cron*
```
## Connaitre les permissions 
```bash
$ sudo -l
$ cat /etc/sudoers
```

## Voir les partitions
```bash
$ df -h
```

## Password mining
```bash
$ history
$ cat ~/.bash_history
$ cat ~/.nano_history
$ cat ~/.atftp_history
$ cat ~/.mysql_history
$ cat ~/.php_history
$ ls -l /etc/passwd
$ ls -l /etc/shadow
$ grep -RiIn passw / 2>/dev/null
$ grep -rnw '/' -ie 'pass' --color=always 2>/dev/null | grep -vi binary
$ grep -rnw '/' -ie 'DB_PASS' --color=always 2>/dev/null | grep -vi binary
$ grep -rnw '/' -ie 'DB_PASSWORD' --color=always 2>/dev/null | grep -vi binary
$ grep -rnw '/' -ie 'DB_USER' --color=always 2>/dev/null | grep -vi binary
```
En un bloc si nous pouvons lire passwd et shadow :
```bash
$ cp /etc/passwd .
$ cp /etc/shadow .
$ unshadow passwd shadow > unshadowed
$ john --format=md5crypt unshadowed
```

# Windows
## OS
```bash
> ver
> wmic os get bootdevice, buildnumber, caption, freespaceinpagingfiles, installdate, name, systemdrive, windowsdirectory
```

## Connaitre les drivers
```bash
> DRIVERQUERY
```

## Lister les disques
```bash
> wmic logicaldisk get name, deviceid, volumename, description
```
## Lister les partages
```bash
> wmic share list
```

## Info sur le réseau
```bash
> ipconfig /all
```

## Lister les ports ouverts
```bash
> netstat -ano
```

## Lister les utilisateurs
```bash
> net users
```

## Lister les groupes
```bash
> net localgroup 
```

## Processus
Lister les processus
```bash
> wmic process list brief
```
Créer un processus
```bash
> wmic process call create {commande}
```
Détruire un processus
```bash
> wmic process where processid="{pid}" delete
```

## Lister les taches planifiées
```bash
> schtasks /query /fo LIST /v
```