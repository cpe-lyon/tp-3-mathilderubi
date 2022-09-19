# Compte-rendu TP 3
*Mathilde Rubi*

## Exercice 1. Gestion des utilisateurs et des groupes

1. Pour créer deux groupes dev et infra avec la commande groupadd on fait :
```
#!/bin/bash

sudo groupadd dev
sudo groupadd infra

```
2. Pour créer les 4 utilisateurs avec la commande useradd en demandant la création de leur dossier personnel on peut faire :
```
#!/bin/bash

sudo useradd -m charlie --shell /bin/bash
sudo useradd -m bob --shell /bin/bash
sudo useradd -m dave --shell /bin/bash
sudo useradd -m alice --shell /bin/bash

```
![image1](image/image1.png)
Les utilisateurs sont présents dans le fichier /etc/passwd, ils ont donc bien été créés

3. Pour ajouter les utilisateurs dans les groupes créés on fait :
```
#!/bin/bash

sudo usermod -a -G dev alice
sudo usermod -a -G dev bob
sudo usermod -a -G dev dave
sudo usermod -a -G infra bob
sudo usermod -a -G infra charlie
sudo usermod -a -G infra dave
```
![image2](image/image2.png)
Les utilisasteurs ont bien été ajoutés à des groupes.

4. Pour afficher les membres de infra on peut faire :
```
#!/bin/bash

grep infra /etc/group

ou

cat /etc/group

```
![image3](image/image3.png)
![image4](image/image4.png)

5. Pour faire de dev le groupe propriétaire des répertoires /home/alice et /home/bob et de infra le groupe propriétaire de /home/charlie et /home/dave

```
#!/bin/bash

sudo chgrp dev /home/alice
sudo chgrp dev /home/bob
sudo chgrp infra /home/charlie
sudo chgrp infra /home/dave
```

6. Pour remplacer le groupe primaire des utilisateurs en dev pour alice et bob et en infra pour charlie et dave, on exécute les commandes suivantes :

```
#!/bin/bash

sudo usermod alice -g dev
sudo usermod bob -g dev
sudo usermod charlie -g infra
sudo usermod dave -g infra
```

7. On crée les répertoires avec les lignes :
```
#!/bin/bash

sudo mkdir/home/dev
sudo mkdir/home/infra
```
Ensuite, pour attribuer les droits sur ces dossiers, on fait :
```
#!/bin/bash

sudo chmod 775 /home/dev
sudo chmod 775 /home/infra
```

8. Pour que dans ces dossiers, seul le propriétaire d'un fichier ait le droit de renommer ou suprimer ce fichier, on ajoute un sticky bit, que l'on ajoute avec :
```
#!/bin/bash
chmod +t /home/dev
chmod +t /home/infra
```

9. On ne peut pas ouvrir une session en tant que alice car le compte alice ne possédant pas de password, le compte n'est pass actif.

10. Maintenant que le compte a été activé (avec la commande sudo passwd alice et en mot de passe alice), nous avons pu nous connecter avec son compte
![image5](image/image5.png)

11. On obtient l'uid et le gid de alice en tapant :
```
#!/bin/bash
id
```
![image6](image/image6.png)

12. Pour retrouver l'utilisateur dont l'uid est 1003 on exacute la commande id 1003

![image7](image/image7.png)

13. 

14.

15. La suppression d'alice du groupe infra ne fonctionne pas. Le groupe infra est le groupe primaire d'alice, elle ne peut pas se faire supprimer de son groupe primaire.

16. Pour modifier le compte de dave de sorte que : 
— il expire au 1
er juin 2021
— il faut changer de mot de passe avant 90 jours
— il faut attendre 5 jours pour modifier un mot de passe
— l’utilisateur est averti 14 jours avant l’expiration de son mot de passe
— le compte sera bloqué 30 jours après expiration du mot de passe
on fait :

```
#!/bin/bash

sudo chage dave

```
![image](image/image8.png)

17. L'interpréteur de commande de l'utilisateur root se trouve avec 
```
#!/bin/bash

getent passwd root
```

18. L'utilisateur nobody existe pour lancer des daemons pour, en cas d'utilisation par un utilisateur malveillant, limiter les dégats.

19. Par défaut, la commande sudo conserve le mot de passe en mémoire pendant 15 minutes. On peut forcer sudo à oublier notre mot de passe avec la commande sudo -k

## Exercice 2. Gestion des permissions

1. Les droits sur le dossier test sont visibles avec la commande ls -l. Ils sont 
