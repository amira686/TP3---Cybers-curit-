# Rapport TP3 de Cybersec AARIANE AMIRA

## Attaque 1: BD fuitée et mot de passe

1. Etape 1 : Pour trouver la base de données cachée, j’ai utilisé le programme Process Monitor, qui m’a permis d’identifier quel fichier était modifié rapidement après la création d’un utilisateur. J’ai utilisé le filtrage afin d’afficher uniquement les fichiers liés à consoleApp, ce qui m’a facilité la tâche, et j’ai ainsi trouvé le fichier situé à l’emplacement suivant : C:\Users\nexil\data\cyber.db <img width="975" height="614" alt="image" src="https://github.com/user-attachments/assets/c4dd02d6-588b-4cdc-8ec1-d1dd9d991d87" />

2. Etape 2 : J’ai ensuite ouvert le fichier avec DataGrip pour pouvoir visualiser les informations recueillies par la BD. On peut observer ici les noms d’utilisateur ainsi que le hachage du NAS et du mot de passe.<img width="975" height="607" alt="image" src="https://github.com/user-attachments/assets/0b11449e-bc04-40eb-b4a9-ca2d7e9af429" />

3. Étape 3 : Pour terminer, j’ai utilisé le site web CrackStation pour déhacher les caractères, ce qui permet d’obtenir le mot de passe. Comme on peut le voir ici, le mot de passe du compte nommé “Justin Trudeau” est Passw0rd1!.<img width="975" height="370" alt="image" src="https://github.com/user-attachments/assets/28f97f28-1384-41bc-b2eb-9f566fd752a3" />


### Correctif implanté

Bien que les mots de passe soient hachés, cette méthode n’est pas idéale, car ils peuvent être relativement faciles à casser avec des outils automatisés. Pour améliorer la sécurité, nous utilisons maintenant l’algorithme de hachage bcrypt, qui ajoute un salt et rend le calcul volontairement plus lent. Cela complique fortement les attaques par force brute et rend le hachage beaucoup plus sécuritaire.

<img width="975" height="407" alt="image" src="https://github.com/user-attachments/assets/999f0a0e-845d-4b48-a6ba-0912c3b11459" />
<img width="975" height="137" alt="image" src="https://github.com/user-attachments/assets/a3f6257b-b0c3-4df3-8ed5-b7cd61da6f36" />




## Attaque 2: BD fuitée et encryption

1. Etape 1 : Grâce à l’attaque numéro 1, nous avons pu obtenir le nom d’utilisateur et le mot de passe. Il a ensuite été possible de se connecter directement à l’application avec ces informations et d’utiliser l’option « Voir mon profil » afin d’accéder aux informations sensibles, dont le NAS.
   <img width="900" height="496" alt="image" src="https://github.com/user-attachments/assets/b708847f-877e-4740-bb7e-d8d9d2bb548f" />
   <img width="975" height="574" alt="image" src="https://github.com/user-attachments/assets/0956ca85-6d90-4c4d-aba2-abe1bd717175" />


### Correctif implanté

Le NAS est maintenant chiffré à l’aide d’un algorithme standard (AES) avant d’être enregistré dans la base de données. Ce chiffrement repose sur une clé secrète et empêche toute lecture directe du NAS à partir de la base de données. Par conséquent, l’attaque utilisée précédemment ne permet plus de récupérer cette information sensible.

<img width="975" height="514" alt="image" src="https://github.com/user-attachments/assets/486dee51-a76d-45a7-9b7c-0c33a9c424bd" />
<img width="975" height="516" alt="image" src="https://github.com/user-attachments/assets/2f643f10-c513-4ce4-bb60-4d0474342c7a" />
<img width="975" height="117" alt="image" src="https://github.com/user-attachments/assets/697ea99c-5de6-47d8-b44f-8242097e8c18" />
<img width="975" height="155" alt="image" src="https://github.com/user-attachments/assets/e0bac5f9-33e5-4c47-b40d-f7b78c0c48f3" />


## Attaque 3 Injection SQL

1. Etape 1 : À l’aide de DotPeek, j’ai repéré un point vulnérable où la requête SQL est construite à l’aide de concaténations avec le symbole +, ce qui permet d’injecter du code SQL directement à partir de l’entrée utilisateur. J’ai donc tenté une injection SQL dans le champ du nom d’utilisateur avec la commande
Justin'; UPDATE MUtilisateur SET motDePasse = '$2a$12$91AaQnd7fmZXg8IKwSDh3OEpbWq4ji9qWXnP0zHWpjkk474.7j4Q2' WHERE nom = 'Justin Trudeau';--
afin de modifier le mot de passe de Justin Trudeau. La commande a bien été interprétée par SQLite, ce qui confirme la présence d’une vulnérabilité par injection SQL. Même si la connexion échoue ensuite à cause de la validation bcrypt, cette attaque démontre qu’il est possible d’exécuter des commandes SQL arbitraires, ce qui représente une faille de sécurité majeure.
<img width="975" height="398" alt="image" src="https://github.com/user-attachments/assets/0e75fdc7-bcfa-414c-9941-a757726a75b5" />
<img width="975" height="292" alt="image" src="https://github.com/user-attachments/assets/eb1ebf8d-9c47-45ff-b0a1-e137d12145ca" />
<img width="975" height="645" alt="image" src="https://github.com/user-attachments/assets/1f090c54-bade-46fb-b460-82151a690a3e" />



### Correctif implanté

Description du correctif.

Avant le correctif, les requêtes SQL étaient construites avec des concaténations (+), ce qui permettait d’injecter du code SQL via les champs de saisie.
Le correctif consiste à utiliser des requêtes paramétrées, où les valeurs fournies par l’utilisateur sont traitées comme des données et non comme du code SQL.
Ainsi, même si un utilisateur entre une commande SQL malveillante, elle n’est plus exécutée par la base de données.
<img width="971" height="628" alt="image" src="https://github.com/user-attachments/assets/b5d55a13-a2eb-4160-a499-785c06720f12" />
<img width="975" height="381" alt="image" src="https://github.com/user-attachments/assets/64ed952a-9fcf-4c27-a3f2-e50d6afa0e3e" />
<img width="975" height="591" alt="image" src="https://github.com/user-attachments/assets/cdc8fa36-20c6-42b6-b3f5-6ec76afbb762" />
<img width="975" height="214" alt="image" src="https://github.com/user-attachments/assets/cd82036e-d06a-4588-9c3e-98402155e9f5" />




