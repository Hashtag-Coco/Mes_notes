## Enumeration de dossier et de page d'un site WEB
```bash
$ dirb http://{target}/ /usr/share/wordlists/dirb/big.txt -X .php,.html -o dirb.txt
$ nikto -h http://{target}
$ gobuster -u http://{target} -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 20
$ python3 /git/dirsearch/dirsearch.py -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -e "php,txt,sh,jar,cgi,pl,py,php.swp,~,bak" -r 2 -x 403 -f -t 50 --simple-report=dirsearch -u {TARGET}
```

## Scan d'un site wordpress
```bash
wpscan -u http://{target}/ --enumerate t --enumerate p --enumerate u
wpscan –u http://{target} --username {UserName} --wordlist {wordlist}
```

## DNS faire un transfert de zone et de l'énumeration
```bash
$ dnsrecon -d {domain.com} -t axfr @{domain.com}
$ dnsenum {domain.com}
```

## Enumération des sous-domaines d'un domaine
```bash
$ python sublist3r.py -d {domain.com}
```

## Obtenir des infos sur le serveur RPC distant
```bash
$ rpcinfo -p {target}
```

## netbios scan show logged in users/addresses
```bash
$ nbtscan {target}
$ nbtscan {networkAddr/masq}
```

## SAMBA fingerprint version, énumération des dossiers partagés et users
```bash
$ smbclient -L //{target}
$ nmap -p 445 -vv --script=smb-enum-shares.nse,smb-enum-users.nse <ip>
```

## Check si une liste d'utilisateur existe
La cible enface est un kerberos (port 389)
```bash
$ kerbrute_linux_386 userenum --dc {TARGET_IP} -d {NAME.local} listes_user.txt --safe -v
```

## SAMBA minimal scan / everything
```bash
$ enum4linux {target}
$ enum4linux -a {target}
```

## SAMBA enumerate users
```bash
$ nmap -sU -sS --script=smb-enum-users -p U:137,T:139 {networkAddr/masq}
```

## Scan file type by method (vérifier les méthodes allowed)
```bash
$ davtest -url http://{target}
```

## NFS shares which are available
```bash
$ showmount -e 10.10.10.10
```

## Monter un partage smb distant en utilisant CIFS
```bash
$ mount-t cifs "//<ip>/<targeted share>/" /mnt 
$ smbget -R smb://<ip>/<share>/<path>/<file>
```
```bash
$ mkdir Data
$ mount.cifs //X.X.X.X/Data ./Data -o user=USERNAME
```
### Récupérer plusieurs fichiers/dossiers distant
```bash
smb > mask ""
smb > recurse ON
smb > prompt OFF
smb > mget *
```

## Obtenir un tgt
```bash
python3 GetNPUsers.py nom_de_la_machine/ -no-pass -usersfile user.txt
```

## Basic information
```bash
$ whois domain.com
$ dig {a|txt|ns|mx} domain.com
```

## Email
```bash
$ simplyemail.py -all -e domain.com
```

## Nmap (Shodan est très cool aussi)
```bash
$ nmap -A -T4 -Pn {target}
```
-p {1-65535} = port </br>
-O = OS detection</br>
-sV = version detection</br>
-sU = UDP scan</br>
-sT = tcp scan</br>
-A = OS detection + nmap scripts + traceroute + version</br>
-F = fast scan</br>
-T{0-5} = scan timing slow to fast</br>
-sn {XXX.XXX.XXX.XXX/XX} = ping scan (network scan, disable port scan, assume all hosts up)</br>
-sP {XXX.XXX.XXX.XXX/XX} = ping scan (network scan, skip host discovery, only shows hosts that respond)</br>
-S {ip} = spoof ip address</br>

Dans certain cas, des ports peuvent ne pas apparaitre donc on rajoute l'option p :
```bash
$ nmap -p1-65535 {target}
``` 

## Probing Neighbors
```bash
$ netdiscover -i {interface}
```

## OSINT, ne pas oublier qu'il existe Maltego et les googles dork
```bash
$ theHarvester -d <domain> -l 300 -b all -f output
```

## Info sur l'ip
```bash
$ curl ipinfo.io/{IP]
```

## Info sur un pseudonyme
```bash
$ python3 sherlock.py {pseudonyme}
```

## Récupérer tous les mots d'un site web dans une wordlist
```bash
$ cewl --depth 5 -w nom_wordlist http://8.8.8.8.fr/
```
