# Installation-Serveur-IRCU2
Documentation sur l'installation et la configuration de Ircu2 sous 24.04.3 LTS

# 1. Installation des prérequis

- Ubuntu 24.02.3 LTS
- root access

# 1.2 Mise à jour
```bash 
root@mail:~# apt update
root@mail:~# apt upgrade
root@mail:~# apt install build-essential
root@mail:~# apt install wget git libssl-dev openssl bison libreadline-dev zlib1g-dev automake make flex byacc
```

# 2. Installation de Ircu2

Création du nouvelle utilisateur afin de jail le service (Spécifier le mot de passe souhaiter)
```bash
root@mail:~# adduser ircd
```

Connection au nouvelle utilisateur depuis le root
```bash
root@mail:~# su - ircd
```

Clonage de Ircu2 à la racine de l'utilisateur ircd
```bash
ircd@mail:~$ git clone https://github.com/UndernetIRC/ircu2
```

Accès au répertoire nouvellement crée par le clonage depuis github
```bash
ircd@mail:~$ cd ircu2/
```

Préparation du projet pour la compilation futur
⚠️ Si vous avez un utilisateur diférent de "*ircd*", veuillez changer le chemin /home/{votre username}/ircd
```bash
ircd@mail:~/ircd$ ./configure --prefix=/home/ircd/ircd --with-maxcon=1024
```

Lancement de la compilation du projet..
```bash
ircd@mail:~/ircd$ make
```

Installation du projet sur le système
```bash
ircd@mail:~/ircd$ make install
```

Retour à la racine de l'utilisateur
```bash
ircd@mail:~/ircd$ cd
```

Accès au répertoire incluant la config de l'ircu
```bash
ircd@mail:~/ircd$ cd ircd/lib
```

Création d'une backup de la config avant la modification de celle-ci
```bash
ircd@mail:~/ircd$ cp example.conf ircd.conf
```

# 3. Configuration de ircd.conf

*⚠️ Si vous ne trouvez pas le fichier, veuillez retourner à la commande précedente et verifier pour des erreurs.* 

Maintenant que l'ircu est installer nous allons devoir le configurer afin qu'il puisse ce lancer.
Pour cela nous allons l'ouvrir avec l'éditeur de texte de votre choix. (Seulement les plus connue sont réferencer dans cette documentation)

## 3.1. Ouvrir le fichier

### 3.1.1. Avec nano
⚠️ L'installation de celui-ci est nécessaire:
```bash
apt install nano
```
Pour ouvrir le fichier :
```bash
nano ircd.conf
```
Une documentation sur nano arrive bientôt en attendant se referencer ici: https://linuxize.com/post/how-to-use-nano-text-editor/ 

### 3.1.2. Avec vim
Vim est preinstaller sur Ubuntu 24.04.3 LTS donc pas besoin de l'installer.

Pour ouvrir le fichier: 
```bash
vim ircd.conf
```

## 3.2. La config
Dans ce fichier vous pourrez configurer beaucoup d'option et comme je ne peut pas faire une documentation de 30 pages sur une config je ne montrerais que les parties essentiel au bon fonctionnement de l'ircd.

### 3.2.1. Général
Vous trouverez dans le fichier ircd.conf une section prennant cette forme:
```conf
General {
    name = "London.UK.Eu.UnderNet.org";
    description = "University of London, England";
    numeric = 1;
};
```
Dans cette section nous voyons 3 paramètres:

```name``` : Ici vous pouvez spécifier le nom de votre node ircu, cela reste une simple recomendation mais je peut vous conseillez si vous avez un domaine de suivre la forme suivante:

```conf
ville.pays.votre.domaine
``` 

Si vous n'avez pas de domaine :

```conf
ville.pays[.eu].undernet.org
```

⚠️ Je vous déconseille également de mettre des majuscules / des charactères spéciaux.

```description```: Description de votre serveur, les charactères '[' et ']' ne doivent pas etre utiliser pour la compatibilité avec les anciens serveurs.

```numeric``` : Cette valeur doit être un nombre **unique** sur le réseaux sur lequel tourne le serveur ircd il peut etre compris entre 0 et 4095. Il n'est pas mis à jour lors d'un rehash, un restart du serveur est requis ! 

# 4. Lancement du serveur
Maintenant que la config est prête vous pouvez lancer la commande à l'aide de la commande suivante:
```
ircd@mail:~/ircd/lib$ cd
ircd@mail:~$ cd ircd/bin/
ircd@mail:~/ircd/bin$  ./ircd -f ../lib/ircd.conf
```

# 5. Pour aller plus loin

## Configuration du firewall
Un tuto arrivera bientôt sur ce sujet. 

## Client IRC
Un tuto arrivera bientôt sur ce sujet.
