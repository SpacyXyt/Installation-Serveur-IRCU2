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
