# Compte rendu TP3
## Exercice 1 : Gestion des utilisateurs et des groupes

### Question 1 
Pour créer le groupe dev ou infra on utilise la commande ci-dessous
```
-sudo groupadd (dev/infra)
```

### Question 2
Pour créer un utilisateur il faut utiliser cette commande
```
-sudo useradd (dave/charlie/bob/alice)
```

### Question 3 
Cette commande permet d'ajouter des utilisateurs à un groupe
```
-sudo gpasswd -a (alice/bob) dev 
-sudo gpasswd -a (dave/charlie) infra
```

### Question 4 
On peut afficher les membres du group infra avec la commande 
```
-getent group infra
```

### Question 5 
on utilise les commandes suivantes : 
```
-sudo chgrp dev /home/(alice/bob)
-sudo chgrp infra /home/(dave/charlie)
```

### Question6 
on modifie les group primaire avec les commandes suivantes :
```
-sudo usermod -g dev (alice/bob)
-sudo usermod -g infra (charlie/dave)
```

### Question 7 

```
 sudo chmod g=w,o=w /home/infra
 sudo chmod g=w,o=w /home/dev
```

### Question 8
```
	chmod u=rwx
```
	
### Question 9 
Non impossible car son compte n'a pas été paramétrer (mot de passe)

### Question  10
Pour activer son compte  il faut lui créer un mdp avec passwd alice.
Puis l'activer avec la commande passwd --unlock alice.
puis il est possible de se connecter en ssh avec le compte d'alice

### Question 11

pour récupérer l'uid et le gid de alice on peut taper la commande id qui permet de trouver ces différentes informations. uid=1002(alice) gid=1002(dev) groups=1002(dev)

### Question 12
en tapant la commande id 1003 on peut retrouver l'utilisateur qui est bob

### Question 13
pour trouver l'id du groupe dev on peut taper la commande id bob qui permet d'afficher de nombreuses informations notamment l'id du groupe qui est 1002

### Question 14

Le groupe ayant l'id 1002 est le groupe dev

### Question 15
```
gpasswd --delete charlie infra
```

### Question 16
```
usermod -e 2021-06-01 dave
sudo chage -M 90 dave
 sudo passwd -n 5 dave
 sudo chage -W 14 dave
 sudo usermod -f 30 dave
 ```
 
 ### Question 17
 ```
$ cat /etc/passwd | grep root
root: x :0:0:root:/root:/bin/bash
```
C'est /bin/bash

### Question 18 
```
$ cat /etc/passwd | grep nobody
nobody: x :65534:65534:nobody:/nonexistent:/usr/sbin/nologin
```
Il s'agit d'un utilisateur qui ne dispose pas de mot de passe il ne peut donc pas se connecter

### Question 19

Avec la commande sudo -K on peut remarquer que sudo conserve le mot de passe en mémoire pendant 15 minutes.

### Exercice 2 

### Question 1 

Tout d'abord pour créer le dossier on utilise mkdir dossier puis touch fichier pour créer le fichier. La commande chmod nous permet de voir les droits sur le dossier et le fichier.
```
drwxrwxr-x 2 user user 4096 Sep 26 09:05 test
-rw-rw-r-- 1 user user    6 Sep 26 09:05 fichier
```
### Question 2 

Pour se retirer tous les droits on utilise la commande :
```
chmod 000 fichier
```
Puis on remarque qu'en tant que root nous avons toujours accès au fichier.

### Question 3

```
chmod 700 fichier
echo "echo Hello" > fichier
```
Les droits sont bien conservés.

### Question 4 

```
./fichier
```
Cela ne fonctionne pas car il n'est pas exécutable
```
sudo ./fichier
```
Mais avec sudo cela fonctionne car il permet d'exécuter un fichier même s'il n'est pas exécutable

### Question 5 
```
$ chmod -r test
$ ls test
ls: cannot open directory 'test': Permission denied
$ cat test/fichier
salut
```
Il est impossible de lister le contenu du répertoire puisque nous n'avons plus les droits mais il est toujours possible d'afficher le contenu du fichier

Pour se remettre les droits de lecture sur le répertoire test
```
$ chmod +r test
```

### Question 6
```
$ touch test/nouveau
$ mkdir test/sstest
$ chmod -w test/nouveau
$ chmod -w test
$ echo "salut" > test/nouveau
bash: test/nouveau: Permission denied
$ chmod +w test
$ echo "salut" > test/nouveau
$ rm test/nouveau
```
Il est impossible de modifier le fichier nouveau étant donné que nous n'avons pas les droits d'écritures dessus. 
Il est possible de le supprimer si je possède les droits sur le dossier test

### Question 7 
```
$ chmod -x test
$ touch test/nouveau
bash: test/nouveau: Permission denied
$ rm test/nouveau
rm: cannot remove 'test/nouveau': Permission denied
$ echo "salut" > test/nouveau
bash: test/nouveau: Permission denied
$ cd test
bash: cd: test: Permission denied
$ ls test
ls: cannot open directory 'test': Permission denied
```
On peut remarquer que sans les droits d'exécution sur le répertoire toutes les actions sont bloquées.

### Question 8 


### Question 9 
```
$ chmod +x test
$ chmod g+r test/fichier
```




