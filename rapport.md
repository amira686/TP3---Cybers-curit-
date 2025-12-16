# Rapport TP3 de Cybersec AARIANE AMIRA

## Attaque 1: BD fuitée et mot de passe

1. Etape 1 : Pour trouver la base de données cachée, j’ai utilisé le programme Process Monitor, qui m’a permis d’identifier quel fichier était modifié rapidement après la création d’un utilisateur. J’ai utilisé le filtrage afin d’afficher uniquement les fichiers liés à consoleApp, ce qui m’a facilité la tâche, et j’ai ainsi trouvé le fichier situé à l’emplacement suivant : C:\Users\nexil\data\cyber.db <img width="975" height="614" alt="image" src="https://github.com/user-attachments/assets/c4dd02d6-588b-4cdc-8ec1-d1dd9d991d87" />

2. Etape 2 : J’ai ensuite ouvert le fichier avec DataGrip pour pouvoir visualiser les informations recueillies par la BD. On peut observer ici les noms d’utilisateur ainsi que le hachage du NAS et du mot de passe.<img width="975" height="607" alt="image" src="https://github.com/user-attachments/assets/0b11449e-bc04-40eb-b4a9-ca2d7e9af429" />

3. Étape 3 : Pour terminer, j’ai utilisé le site web CrackStation pour déhacher les caractères, ce qui permet d’obtenir le mot de passe. Comme on peut le voir ici, le mot de passe du compte nommé “Justin Trudeau” est Passw0rd1!.<img width="975" height="370" alt="image" src="https://github.com/user-attachments/assets/28f97f28-1384-41bc-b2eb-9f566fd752a3" />


### Correctif implanté

Description du correctif.

Preuve que l'attaque ne fonctionne plus avec étapes + copie d'écran


## Attaque 2: BD fuitée et encryption

1. Etape 1 + copie d'écran
2. Etape 2 + copie d'écran
3. etc.

### Correctif implanté

Court descriptif du correctif et lien vers le(s) commit(s).

Preuve que l'attaque ne fonctionne plus avec étapes + copie d'écran

## Attaque 3 Injection SQL

1. Etape 1 + copie d'écran
2. Etape 2 + copie d'écran
3. etc.

### Correctif implanté

Description du correctif.

Preuve que l'attaque ne fonctionne plus avec étapes + copie d'écran
