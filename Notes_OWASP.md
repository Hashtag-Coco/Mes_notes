# Notes sur l'OWASP testing guide
## Sommaire :
- [Vocabulaire](#vocabulaire)
- [Passive and Active Testing](#passive-and-active-testing)
  * [Passive Testing](#passive-testing)
  * [Active Testing](#active-testing)
## Vocabulaire
Tester = Who performs the testing activities.
Threat = It's anything that can may harm the assets owned by an application.
Vulnerability = It's a flaw or weakness in a operation/implementation/management..
Gates = access points of an application.
```bash
Un risque est quelque chose que tu n'aimerais pas qui se produise, mais parfois, il se produit.
Menace : la météorite
bien essentiel : le datacenter
evenement redouté : elle peut porter atteinte au datacenter
scenario : la meteorite tombe sur le datacenter
```
## Passive and Active Testing

### Passive Testing
Durant un test passif, le tester essaye de comprendre le fonctionnement de l'application et l'explore comme un utilisateur.
Il peut mettre en place un proxy HTTP pour observer les requêtes/réponses et ainsi comprendre les accès et paramètres (endpoint, HTTP 
header, parameters, cookies).</br>
Exemple :
```bash
https://www.example.com/login/authentic_form.html
```
^ Ce lien indique une authentification où l'application demande un username & password.
```bash
http://www.example.com/Appx.jsp?a=1&b=1
```
^ Ce lien indique deux paramètres qui sont prit en compte (a et b). Ces 2 gates seront des points à tester. 

### Active Testing
Durant un test actif, le tester va utiliser la methodologie suivante (chaque étapes se décompose en plusieurs tests) :
* Configuration and Deployment Management Testing
* Identity Management Testing
* Authentication Testing
* Authorization Testing
* Session Management Testing
* Input Validation testing
* Error Handling
* Cryptography
* Business Logic Testing
* Client Side Testing
</br>

## Information Gathering
L'information gathering est l'act de récolter des informations contre une victime/un SI.</br>
Google Dork pour optimiser ses recherche :
```bash
site:	limiter les recherches à l'url
inurl:		only result that include keyword in URL
intitle:	only result that include keyword in page title
intext:		only result with keyword in the body of pages
filetype:	only match specific filetype
```
```bash
https://www.exploit-db.com/google-hacking-database
```
^ Ce lien nous renvoi sur exploit-db qui regroupe les google dorks efficace pour certaines recherches...</br>
### Fingerprint WebServer
Cette étape a pour but d'identifier le type et la version du serveur web.</br>
#### Banner Grabbing
On envoi une requête HTPP (via telnet par exemple ou openssl pour du SSL), et on examine la réponse HTTP du serveur web, dans le header, nous avons le champs ETag qui permet d'identifier
le serveur web :
```bash
ETag: "75-591d1d21b6167"   => Apache server
ETag: "5d71489a-75"		   => Nginx server
ETag: "4192788355"		   => lighttpd server
```
#### Sending Malformed requests
On envoi une requête HTTP avec une mauvaise méthode pour examiner l'erreur qui est renvoyée.</br>
Suivant l'erreur renvoyée, on peut en déduire le serveur web.</br>
cf OWASP testing guide page 54 pour des screens.

#### Using Automated Scanning Tools
Les scans automatiques permettent d'identifier le serveur web et sa version, quelques exemples :
* Netcraft (online tool)
* Nikto 
* Nmap
</br>

### Webserver Metafiles for information leakage
Le fichier robots.txt est un fichier qui permet aux sites web de préciser aux crawlers de ne pas indéxer les pages web contenu
dans le robots.txt.</br>

### Enumerate applications on Webserver
Beaucoup d'applications ont des vulnérabilités, il faut donc identifier ces applications.</br>
