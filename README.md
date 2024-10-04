# TP1-Unix

##Intro

## 2.1
- nano /etc/ssh/sshd_config
- J'ai remplacer "PermitRootLogin prohibit-password" par "PermitRootLogin yes".
- Ensuite j'ai redémarré le service SSH: systemctl restart ssh.
- Puis sur un autre terminal j'ai pu me connecter à la machine virtuelle avec : ssh root@monAdresseIp

## 2.3
```bash
root@serveur-correction:~# dpkg -l | wc -l
330
```
En tapant la commande dpkg -l | wc -l j'obtiens 330 pacquets.

## 2.4
```bash
root@serveur-correction:~# df -h
| Sys. de fichiers | Taille | Utilisé | Dispo | Uti% | Monté sur     |
|------------------|--------|---------|-------|------|---------------|
| udev             | 4,9G   | 0       | 4,9G  | 0%   | /dev          |
| tmpfs            | 995M   | 572K    | 994M  | 1%   | /run          |
| /dev/sda1        | 9,1G   | 1,6G    | 7,0G  | 19%  | /             |
| tmpfs            | 4,9G   | 0       | 4,9G  | 0%   | /dev/shm      |
| tmpfs            | 5,0M   | 0       | 5,0M  | 0%   | /run/lock     |
| /dev/sda3        | 921M   | 23M     | 835M  | 3%   | /var/log      |
| /dev/sda2        | 3,6G   | 40K     | 3,4G  | 1%   | /tmp          |
| tmpfs            | 995M   | 0       | 995M  | 0%   | /run/user/0   |
```

La racine / représente 1,6 Go d'espace utilisé.

## 2.5
La commande : 
- echo $LANG affiche la langue du systeme.

```bash
root@serveur-correction:~# echo $LANG 
fr_FR.UTF-8
```

- hostname renvoie le nom de l'hote de la machine.
- 
```bash
  root@serveur-correction:~# hostname
  serveur-correction
```
- man hostname renvoi le manuel de la commande hostname ainsi on obtient la commande pour afficher le domaine.
```bash
  NAME
       hostname - show or set the system's host name
       domainname - show or set the system's NIS/YP domain name
```

- La commande cat /etc/apt/sources.list | grep -v -E '^#|^$' affiche les ligne active du fichier source.list
```bash
root@serveur-correction:~# cat /etc/apt/sources.list | grep -v -E '^#|^$'
deb http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware
deb http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware
```

- La commande cat /etc/shadow | grep -vE ’:\*:|:!\*:’ affiche le contenu du fichier etc/shadow en filtrant les lignes pour afficher seulement pour les utilisateurs qui ont un mod de passe valide ( ni vide ni desactivé)
```bash
root@serveur-correction:~# cat /etc/shadow | grep -vE ':\*:|:!\*:'
root:$y$j9T$cGKpM0Fh8WZYM4MlsbdWz0$hO26Ub/deBLYO3CleXEevZ8v/V.ItKMLsZ274x5BMtA:19635:0:99999:7:::
messagebus:!:19635::::::
sshd:!:19998::::::
```

- La commande cat /etc/passwd | grep -vE ’nologin|sync’ affichera toutes les lignes du fichier /etc/passwd pour les utilisateurs qui ont un shell différent de nologin ou qui ne sont pas l'utilisateur sync.

```bash
root@serveur-correction:~# cat /etc/passwd | grep -vE 'nologin|sync'
root:x:0:0:root:/root:/bin/bash
```

- La commande fdisk -l affiche des informations sur les disques et les partitions du système.
```bash
root@serveur-correction:~# fdisk -l et fdisk -x
fdisk: impossible d'ouvrir et: Aucun fichier ou dossier de ce type
fdisk: impossible d'ouvrir fdisk: Aucun fichier ou dossier de ce type
root@serveur-correction:~# fdisk -l 
Disque /dev/sda : 20 GiB, 21474836480 octets, 41943040 secteurs
Modèle de disque : HARDDISK        
Unités : secteur de 1 × 512 = 512 octets
Taille de secteur (logique / physique) : 512 octets / 512 octets
taille d'E/S (minimale / optimale) : 512 octets / 512 octets
Type d'étiquette de disque : gpt
Identifiant de disque : 3ED2EBFD-8995-4690-8EEF-8C65108F2339


| Périphérique | Début    | Fin      | Secteurs  | Taille | Type                          |
|--------------|----------|----------|-----------|--------|-------------------------------|
| /dev/sda1    | 2048     | 19531775 | 19529728  | 9,3 Go | Système de fichiers Linux     |
| /dev/sda2    | 19531776 | 27344895 | 7813120   | 3,7 Go | Système de fichiers Linux     |
| /dev/sda3    | 27344896 | 29298687 | 1953792   | 954 Mo | Système de fichiers Linux     |
| /dev/sda4    | 29298688 | 41940991 | 12642304  | 6 Go   | Partition d'échange Linux     |

```

```bash
root@serveur-correction:~# fdisk -x
Disque /dev/sda : 20 GiB, 21474836480 octets, 41943040 secteurs
Modèle de disque : HARDDISK        
Unités : secteur de 1 × 512 = 512 octets
Taille de secteur (logique / physique) : 512 octets / 512 octets
taille d'E/S (minimale / optimale) : 512 octets / 512 octets
Type d'étiquette de disque : gpt
Identifiant de disque: 3ED2EBFD-8995-4690-8EEF-8C65108F2339
Premier LBA utilisable: 34
Dernier LBA utilisable: 41943006
LBA alternatif: 41943039
LBA de départ des entrées de partition: 2
Entrées de partitions allouées: 128
LBA de fin des entrées de partition: 33


| Périphérique | Début    | Fin      | Secteurs  | Type-UUID                             | UUID                                   | Nom           |
|--------------|----------|----------|-----------|---------------------------------------|----------------------------------------|---------------|
| /dev/sda1    | 2048     | 19531775 | 19529728  | 0FC63DAF-8483-4772-8E79-3D69D8477DE4  | 7202EEDF-B999-47CC-BE80-70C80C2C83B0   | la racine     |
| /dev/sda2    | 19531776 | 27344895 | 7813120   | 0FC63DAF-8483-4772-8E79-3D69D8477DE4  | 346085A8-A5AE-48BA-B6B7-BDA598DD7465   | espace tempo  |
| /dev/sda3    | 27344896 | 29298687 | 1953792   | 0FC63DAF-8483-4772-8E79-3D69D8477DE4  | 8F880167-DE17-4896-BB95-EE5AAC9E2E9A   | les logs      |
| /dev/sda4    | 29298688 | 41940991 | 12642304  | 0657FD6D-A4AB-43C4-84E5-0933C84B4F4F  | 68C18C76-59A6-45DF-A745-F87FD1D412DA   | ma swap       |

```

man fdisk: 

-x, --list-details
           Identique à --list, mais avec plus de détails.

- La commande df -h est utilisée pour afficher l'espace disque utilisé et disponible sur les systèmes de fichiers montés
```bash
root@serveur-correction:~# df -h

| Sys. de fichiers  | Taille | Utilisé | Dispo | Uti% | Monté sur       |
|-------------------|--------|---------|-------|------|-----------------|
| udev              | 4,9G   | 0       | 4,9G  | 0%   | /dev            |
| tmpfs             | 995M   | 572K    | 994M  | 1%   | /run            |
| /dev/sda1         | 9,1G   | 1,6G    | 7,0G  | 19%  | /               |
| tmpfs             | 4,9G   | 0       | 4,9G  | 0%   | /dev/shm        |
| tmpfs             | 5,0M   | 0       | 5,0M  | 0%   | /run/lock       |
| /dev/sda3         | 921M   | 23M     | 835M  | 3%   | /var/log        |
| /dev/sda2         | 3,6G   | 40K     | 3,4G  | 1%   | /tmp            |
| tmpfs             | 995M   | 0       | 995M  | 0%   | /run/user/0     |
```

## 3.1

- Le preseed est un outil pour automatiser et personnaliser l'installation de systèmes d'exploitation Debian. C'est un fichier qui va contenir les reponses aux questions posées lors de l'installation.


## 3.2

- Accèder au menu GRUB lors du démarrage ou redémarrage de la machine.
- Repèrer la ligne qui commence par linux, remplacer ro (lecture seule) par rw (lecture-écriture) et ajouter init=/bin/bash à la fin de la ligne. Cela permettra de démarrer directement en mode shell avec les permissions root.
- Enuite avec les droits root on peut executer la commande passwd pour changer le password de root.
- Puis on redemarre la machine.

## 3.3






