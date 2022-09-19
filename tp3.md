# Compte-rendu TP 3
*Mathilde Rubi*

## Exercice 1. Gestion des utilisateurs et des groupes

1. 
```
#!/bin/bash

sudo groupadd dev
sudo groupadd infra

```
2. 
```
#!/bin/bash

sudo useradd -m charlie --shell /bin/bash
sudo useradd -m bob --shell /bin/bash
sudo useradd -m dave --shell /bin/bash
sudo useradd -m alice --shell /bin/bash

```
![image1](image/image1.png)
Les utilisateurs sont présents dans le fichier /etc/passwd, ils ont donc bien été créés

3. 
```
#!/bin/bash

sudo usermod -a -G dev alice
sudo usermod -a -G dev bob
sudo usermod -a -G dev dave
sudo usermod -a -G infra bob
sudo usermod -a -G infra charlie
sudo usermod -a -G infra dave
```
