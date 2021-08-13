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
Un risque est quelque chose que tu n\'aimerais pas qui se produise, mais parfois, il se produit.
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
### Test file extension Handling for Sensitive Information
Les extensions de fichiers sont très utiles pour connaitre les technologies/langages et plugins utilisés par le serveur web.</br>
Pour tester, il suffit de bruteforce les extensions jusqu'a découvrir les bons. Les extensions suivantes peuvent contenir des 
informations sensibles :
* .asa
* .inc
* .config

### Review old backup and Unreferenced files for Sensitive information
Bien souvent, on peut trouver des fichiers oubliés ou non-référencés sur le site web. Cela peut aller aux fichiers simples jusqu'au 
backup :
* .tar
* .zip
* .gz 
* .bak
* .old
* ~

### Enumerate infrastructure and Application Admin Interfaces
Il est toujours bon de vérifier si il y a une interface pour les administrateurs :
* /admin
* /administrator
Egalement, parfois on a pas accès ce dossier/fichier, mais on a accès plus loins (/admin/test.txt en 200).</br>
A noter que tous les framework web possèdent une interface pour les admins :
* /admin pour WebSphere
* /phpmyadmin pour PHP
* /wp-admin/ pour wordpress
et d'autre pages 111.

### Test HTTP Methods
HTTP permet plusieurs methode d'accès à une ressource suivant ce que l'on veut faire, exemple :
* GET
* POST 
* HEAD
* PUT
* DELETE
* TRACE
Ces commandes peuvent être utilisées pour obtenir pleins d'informations sur le site web (XST par exemple).</br>
#### Arbitrary HTTP methods
Si on tente des méthodes qui n'existent pas, suivant l'erreur retournée par le serveur, nous pouvons tenter des choses (CSRF).</br>
Pages 115/116.

#### Head access control Bypass
Visiter une page qui requiert une authentification nous redirige (302) vers une log page. Néanmoins, si en utilisant HEAD nous avons un 200 OK,
il est possible de faire du CSRF.</br>
Pages 116.

### Test HTPP Strict Transport Security
HSTS header, est un mecanisme qui permet aux sites de communiquer avec les navigateurs en obligeant du HTTPS. Il est reconnu avec le champ :
"Strict-transport-Security: max-ages=15768000; includeSubDomains". Pour tester sa présence, il faut regarder ses réponses.

### Test RIA Cross Domain Policy
Rich Internet Applications est une API qui est executé sur un navigateur web. Depuis qu'elle utilise Adobe crossdomain.xml policy file, il y a 
une possibilité de compromettre un autre domaine à partir du domaine compromit.</br>
Conséquences :
* Permissions cross-domain trop légères dans la policy.
* Generer des réponses serveur qui peuvent être traitées comme des cross-domain policy files.
* Fonctionnalitée Upload qui peut uploader des fichiers considérés en tant que cross-domain policy files.
* Protection CSRF réduite à 0.
* Plus de restrictions/protections. 
Généralement, le fichier est à la racine du site :
* example.com/crossdomain.xml
* example.com/clientaccesspolicy.xml
Exemple de test pages 120.

### Test for Subdomain takeover
Une exploitation reussie permet à l'attaquant de prendre le control d'un sous domaine. Le principe de l'attaque est le suivant :
* Un record DNS du sous-domaine de la victime pointe vers un non-existant/non-actif endpoint/external service ou ressource.
Une fois le takeover effectué, plusieurs attaques peuvent s'y dérouler :
* Malicious content.
* Phishing.
* stealing user session cookies.
* stealing credentials.

Plusieurs exemples page 122+

### Test Cloud Storage
Il arrive que les applications web soient hébergées dans un cloud. De mauvaises permissions peuvent se résoudrent en sensitive information 
exposure, alternation de données ou accès non-authorisé.</br>
Une liste de test :
* Identifier l'URL pour avoir accès aux datas puis :
* Essayer de lire des données.
* Upload un fichier.
Un exemple pour lire et upload un fichier :
```bash
$ curl -X GET https://<cloud-storage-service>/<object>
$ curl -X PUT 'd 'test' 'https://<cloud-storage-service>/test.txt'
```

## Identity Management Testing
### Test Role Definitions
Les roles définitions se basent sur les droits entre un administrateur, un manager, un staff et un customer.</br>
Test : un utilisateur n'est pas censé aller sur du /admin.

### Testing for Account Enumeration and Guessable User Account
Les usernames sont facilement bruteforcable pour les deviner.</br>
Pour tester :
* Essayer un identifiant et mot de passe correct.
* Essayer un identifiant correct mais pas le mot de passe.
* Essayer un identifiant et mode de passe incorrect.

### Testing for Weak or Unenforced Username Policy
Généralement, les noms d'utilisateurs se ressemblent tous (j.smith ...).

## Authentication Testing
### Testing for Credentials Transported over an Encrypted Channel
Credentials transport veux dire que l'authentification de l'utilisateur est effectué par un canal chiffré au cas ou un hacker intercepte le
traffic.</br>
Test :
* Via la methode HTTP.
* Si dans la requête POST, nous avons un Referer-header en http (cela permet un SSLStrip)

### Testing for Default Credentials
On test simplement le couple identifiant/mot de passe par défaut de l'application.

### Testing for Weak Lock Out Mechanisme
Le mécanisme de Lock out est ce mécanisme qui bloque un compte si il y a trop de tentative pour y acéder. 
La conséquence est le brute force. Après un nombre de tentative considérable, soit le brute force va faire tomber le serveur
soit il va réussir à deviner le mot de passe.

### Testing for Testing for Vulnerable Renember Password
Ici, on parle des mot de passes qui sont en mémoire, soit par la case "rester connecté" ou soit par un password manager.
Test :
* ClickJacking attack
* CSRF attack.

### Testing for Browser cache Weaknesses
Dans cette étape, le tester vérifie si le navigateur web ne contient pas de données sensibles.

### Testing for Weak password Policy
Selon la policy qui est appliqué, nous pouvons essayer de retrouver des mots de passes tels que 123456789 ou password ou motdepasse.
Test :
* Chercher les mots de passes les plus utilisés et les tester.

### Testing for Weak Security Question Answer
Parfois pour reset son mot de passe, un utilisateur utilise une question de sécurité, selon la question,
on peut bruteforcer la réponse ou alors faire de l'OSINT.
Exemple :
* Nom du chien ?
* Un animal ?
* Une ville ?

### Testing for Testing for Weak Password Change or reset Functionalities
Suivant la robustesse de la sécurité du changement de mot de passe de l'utilisateur, une attack CSRF peut avoir lieu.

### Testing for Weaker Authentication in Alternative Channel
Il suffit de configurer un user agent pour se faire passer pour un téléphone, dans certain cas, la sécurité est diminuée.
Un exemple vaut mille mots :
* La sécurité pour accéder à https://www.example.com/myaccount n'est pas la même que http://m.example.com/myaccount

## Authorization Testing
### Testing Directory Traversal File Include
Directory traversal, c'est le principe de pouvoir se déplacer à partir d'une URL, d'un cookie ou autre élément que le serveur web nous as envoyé. </br>
Interesting variable name :
* example.com/index.php?file=content
* example.com/main.cgi?home=index.html
* example.com/getUserProfile.jsp?item=ikki.html

Interresting cookie :
* Cookie: ID=fd4sdfsdf5df5d4:TMP=1324567564:LM=4545646:S=df4df5df45:TEMPLATE=flower
* Cookie: USER=234154:PSTYLE:GreenDotRed 

Testing techniques :
* index.php?file=../../../../etc/passwd
* index.php?file=http://10.10.10.10:8000

URL encoding and double URL encoding :
* %2e%2e%2f représente ../
* %2e%2e/ représente ../
* ..%2f représente ../

### Testing for Privilège Escalation
Un utilisateur lambda qui par misconfiguration du serveur web, peut créer/modifier du contenu qui n'est pas à lui (où qu'il n'était
pas censé voir).</br>
Exemple dans une requête POST.

### Testing for Insecure Direct Object References
"IDOR occur when an application provides direct access to objects based on user-suplied input." Cette vulnérabilité permet à l'attaquant
de bypasser une authentification en accédant directement à une ressource en modifiant l'URL.</br>
Exemple :
* example.com/somepage?invoice=12345 to invoice=4567

## Session Management Testing
### Testing for Session Management Schema
La "session management" est un mécanisme qui "retient" la connection de l'utilisateur sur un site web. Le cookie a était créé pour cela.</br>
Suivant la sécurité mise en place, le tester peut vérifier le cookie et le token de session qui sont créés d'une manière secure et imprévue.
Cependant, un attaquant qui est capable de prédir et créer le cookie, peut facilement faire un hijacking de session.</Br>
Voici les différentes étapes lors d'une attaque de cookie :
* cookie collection : collection of a sufficient number of cookie samples.
* cookie reverse engineering : analysis of the cookie generation algorithm.
* cookie manipulation : forging of a valid cookie in order to perform the attack. This last step might require a large number of attempts, depending on how the cookie is created (cookie brute-force attack).

### Testing for Session Fixation
Lorsque l'application ne semble pas renouveller le cookie de session après une authentification reussie, c'est possible de trouver 
une "session fixation vulnerability" et de forcer un user à utiliser le cookie connu de l'attaquant.
Comment est caractérisée la "session fixation vulnerability" :
* Une application web authentifie un utilisateur sans la première validation si l'ID est existant, et donc continue d'utiliser l'ID de session qui est déjà attribué à quelqu'un.
* Un attaquant est capable de forcer un ID de session sur un user, donc l'attaquant peut avoir accès à sa session. 

Test :
* Faire une requête GET
* Récupérer l'ID de session et l'envoyé dans une nouvelle requête POST.
* Si c'est un succès, alors la vulnerabilité est présente.

Exemple page 194.

### Testing for Cross Site Request forgery
La CSRF est l'attaque où l'attaquant force l'utilisateur à effectuer une action sur un site web.</br>
Elle se repose sur :
* L'attaquant doit envoyer un lien à un utilisateur.
* L'utilisateur clique sur le lien.
Page 200 pour plus d'info.

### Testing for Session Puzzling/Overloading
Ce principe repose sur l'utilisation d'une même variable afin d'avoir plusieurs utilitées :</br>
https://medium.com/@maheshlsingh8412/session-puzzling-attack-bypassing-authentication-29f4ff2fd4f5

## Input Validation Testing
### Testing for Reflected Cross Site Scripting
Reflected Cross Site Scripting, plus connu sous le nom de XSS, se produit lors d'une execution de code lors de l'affichage d'une page web.</br>
Il existe plusieurs types :
* XSS Reflected : La plus fréquente, souvent dans une URL, elle n'est pas persistente.
* XSS stored : La stored est persistente, souvent dans un espace commentaire d'un site.
* DOM XSS

Test :
* Les inputs utilisateurs : on peut tester avec du javascript : <script>alert(123)</script> ou encore "><script>alert(document.cookie)</script>

Plusieurs exemples de bypass sont présents pages 214+

### Testing for Stored Cross Site Scripting



### Testing for HTTP Verb Tampering
### Testing for HTPP Parameter Pollution
### Testing for SQL Injection
#### Testing for Oracle
#### Testing for Mysql
#### Testing for SQL Server
#### Testing for PostGRESQL
#### Testing for MS Access
#### Testing for NoSQL Injection
#### Testing for ORM Injection
#### Testing for Client Side
### Testing for LDAP Injection
### Testing for XML Injection
### Testing for SSI Injection
### Testing for XPath Injection
### Testing for IMAP SMTP Injection
### Testing for Code Injection
#### Testing for Local File Inclusion
#### Testing for Remote File Inclusion
### Testing for Command Injection
### Testing for Buffer Overflow
#### Testing for Heap Overflow
#### Testing for Stack Overflow
#### Testing for Format string
### Testing for Incubated Vulnerability
### Testing for HTTP Splitting Smuggling
### Testing for HTTP Incoming Requests
### Testing for Host Header Injection
### Testing for Server Side Template Injection
