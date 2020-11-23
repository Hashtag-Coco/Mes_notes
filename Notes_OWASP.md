# Notes sur l'OWASP testing guide

## Sommaire :
- [Vocabulaire](#vocabulaire)
- [Passive and Active Testing](#passive-and-active-testing)
  * [Passive Testing](#passive-testing)
  * [Active Testing](#active-testing)
  
## Vocabulaire
Tester = Who performs the testing activities.</br>
Threat = It's anything that can may harm the assets owned by an application.</br>
Vulnerability = It's a flaw or weakness in a operation/implementation/management..</br>
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

```bash
https://www.exploit-db.com/google-hacking-database
```
^ Ce lien nous renvoi sur exploit-db qui regroupe les google dorks efficace pour certaines recherches...</br>
## Information gathering

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
#### Different Base URL
Pour une application web, le point d'entré est www.example.com. Mais parfois il faut bien retenir que certaine application web sont
sous la forme www.example.com/url1 ou www.example.com/url2 directement (redirection).

#### Non-standard ports
Les ports web sont 80 et 443, mais parfois les services peuvent tourner sur d'autre ports (>1024).

#### Virtual Hosts
Important, le DNS peut permettre à une adresse IP d'être associée à plusieurs nom symbollique. En réalisant des transferts de zones DNS,
on peut parfois déterminer les différents noms associés à l'IP.

### Review Webpage Comments and Metadata for information leakage
C'est plutot commun pour les developpeurs d'inclure des commentaires et metadonnées détaillés dans le code source de la page.
Cela peut être une source d'information.

### Identify Application Entry Points
L'énumération de l'application et sa surface d'attaque est primordiale lors du test.</br>
Pour identifier les gates, il faut bien comprendre chaque interaction entre l'application et nous. Il faut faire attention aux 
paramètres et aux inputs que l'on peut avoir sur le site. Également aux paramètres dans une requete POST (paramètres qui peuvent faire du leakage).</br>
In a nutshell, faire attention à :
* Identifier où les GET et POST sont utilisées.
* Identifier les paramètres utilisés en POST (paramètres qui sont issues du form).
* Dans la requête POST, faire attention aux hidden parameters.
* Identifier tous les paramètres dans une GET requête (I.E. URL), en particulier les chaine de caractère de recherche (après un ?).
* Identifier les paramètres dans une requête de recherche, en général par pair (foo=bar) et leur séparateur.
* Faire attention à tout autre header personnalisé (debug=False).
* En réponse, Identifier où les nouveaux cookies sont situés (Set-Cookie header), modifiés ou ajoutés.
* En réponse, Identifier, où sont les redirects (3XX status code), 400 status codes, 403 en particulier et 500.
* En réponse, noter les headers non-communs ("Server: BIG-IP").
</br>
Il existe des softs pour détecter automatiquement les surfaces d'attaques (ASD en java).</br>
Exemples page 69 de l'OWASP testing guide.

### Fingerprint Web Application Framework
Connaitre le Framework que le site utilise peut nous donner des idées sur les vulnérabilités connus pas encore patchées ou encore les 
misconfigurations communes.</br>
Quelques pistes :
* HTTP headers
* Cookies
* HTML source code
* Specific files and folders
* file extension
* Error message
</br>
Plusieurs exemple page 77.

#### HTTP headers
La façon la plus commune pour identifier le framework est le champ **X-Powered-By** dans l'entête HTTP (d'une réponse). Il y a 
egalement le champ **X-Generator**.

#### Cookies 
Suivant le nom qu'est donné au cookie, on peut connaitre le framework qui le gère.

#### HTML source code
Certain pattern de code dans une page HTML peuvent appartenir à un framework bien précis.

#### Spécific files and folders
Le nommage des fichiers et dossiers est différent pour chaque framework, des dictionnaires existent pour les reconnaitres.

#### File extension
Dans l'URL, la plupart du temps nous pouvons savoir si le site utilise du php, aspx, jsp ou autre.</br>
Exemple : www.example.com/index.php?id=12345

#### Error message
Tout simplement, le nom du framework peut s'afficher en grand dans le cadre d'une erreur.

## Configuration and Deployement Management Testing
### Test Network Infrastructure Configuration
### Test Application Platform Configuration
### Test file extension Handling for Sensitive Information
### Review old backup and Unreferenced files for Sensitive information
### Enumerate infrastructure and Application Admin Interfaces
### Test HTTP Methods
### Test HTPP Strict Transport Security
### Test RIA Cross Domain Policy
### Test File Permission
### Test for Subdomain takeover
### Test Cloud Storage


