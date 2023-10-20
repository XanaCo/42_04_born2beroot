# 42_Born2beroot

## Overview

The "born2beroot" project is an initiative that immerses students into the world of system administration. This project aims to get students familiarized with setting up a virtual machine, installing a Linux distribution from scratch, and configuring it securely with various constraints. They are also tasked with creating a simple monitoring script to provide essential system information.

This project introduces students to the foundational aspects of system administration, server setup, user rights management, and basic security measures, offering a hands-on experience in the day-to-day responsibilities of a system administrator.

## Key Components

1. **Virtual Machine Setup**: Configuring a VM (Virtual Machine) using software like VirtualBox or VMware.

2. **Linux Installation**: Installing a Linux distribution, typically Debian or CentOS, from scratch, without using GUI tools.

3. **Partitioning**: Setting up a logical volume manager (LVM) partitioning system with encryption.

4. **User and Group Management**: Creating specific users and groups, setting permissions, and understanding the principles of the `sudo` command.

5. **Security Enhancements**: Configuring system settings to enhance security, such as setting password policies, disabling root access, and configuring `sudo` settings.

6. **Monitoring Script**: Creating a shell script to display a range of system information, such as OS type, IP address, memory usage, and disk usage.

7. **Additional Services**: Depending on project constraints, setting up services such as SSH, UFW (Uncomplicated Firewall), or others, as required.

## Key Skills Developed

1. **System Administration**: Acquiring foundational knowledge of the roles and responsibilities of a system administrator.

2. **Linux Mastery**: Deepening their understanding of Linux operating systems, filesystems, and user rights management.

3. **Security Best Practices**: Grasping the basics of securing a Linux system, from user permissions to system-wide security policies.

4. **Scripting**: Developing scripting skills, specifically in Bash, to automate and monitor system activities.

5. **Virtualization**: Gaining hands-on experience with virtual machines and understanding their benefits and challenges.

6. **Problem Solving**: Encountering and troubleshooting issues during installation, configuration, and monitoring tasks.

7. **System Monitoring**: Learning the importance of keeping an eye on system metrics and ensuring optimal performance and security.

<!-- # born2beroot

### Mandatory

* Choose between two of the most well-known Linux-based operating systems (CentOS or Debian)
* Create LVM partitions in our new VM
* Ensure SSH services are running on specific ports
* Configure UFW firewall
* Set-up the hostname and a strong password policy for all users
* Set-up a strong configuration for the sudo group
* Create a monitoring script that displays some specific information every 10 minutes

### Bonus

* Set up a specific memory partitioning
* Set up a functional WordPress website with different services
* Set up a service of our own choice, justify that choice


## Concepts

### Unix

**https://fr.wikipedia.org/wiki/Unix**  

#### Origine / Definition

Cree initialement par Bell Labs (dans les annes 70) puis concept repris par AT&T : **systeme d'exploitation multitache et multiutilisateur** qui repose principalement sur un **interpreteur** (aussi appele **un shell Unix** comme *Bourne Shell - sh, Bourne Again Shell - bash, zsh*...) et plusieurs composants utilisables avec des mecanismes de **pipes** et de **redirections**, et des **appels en ligne de commande.**

https://fr.wikipedia.org/wiki/Shell_Unix  
https://fr.wikipedia.org/wiki/Commandes_Unix

Une particularite d'Unix est de considerer de nombreux objets comme des fichiers : les peripheriques d'entree-sortie par exemple.

#### Declinaisons

Ce systeme est celui sur lequel se basent presques tous les systemes d'exploitation PC ou mobile actuels (sauf les Windows NT), appeles **"systemes UNIX"**.

Les principales familles de systemes UNIX sont :
- BSD (Berkeley Software Distribution)
- **GNU** ou aussi appele **GNU/Linux**
- Autres systemes que GNU fonctionnant sur **noyau Linux : Android, macOS**, Solaris, Atari System 5...

#### Developpements paralleles / complementaires

Le **langage C** (auparavant appele *New B*) a ete cree pour la creation de l'UNIX dans le debut des annees 70.

En 1988, le standard de normes **POSIX** a ete cree pour standardiser les interfaces de programmation de logiciels destines a fonctionner sur les variantes d'UNIX. 

Aujourdhui, la marque deposee UNIX est possedee par l'*OpenGroup*, et pour utiliser cette marque pour un OS, il faut qu'il soit conforme a la *Single Unix Specification*.

### Linux

**https://fr.wikipedia.org/wiki/Linux**

#### Origine / Definition

Linux, cree par Linus Torvalds en 1991, n'est pas un systeme d'exploitation. 

*Souvent quand on parle de 'Linux', c'est un abus de langage pour designer plutot soit le systeme d'exploitation GNU (appele couramment GNU/Linux car fonctionnant sur noyau Linux), soit une distribution Linux.*

Linux est un **noyau** de systeme d'exploitation. On voit d'ailleurs par leurs noms les *aspects complementaires du kernel (noyau) et du shell (enveloppe).*

#### Noyau de systeme d'exploitation

Certains (la grande majorite: GNU/Linux, Windows, Mac OS X) systemes d'exploitation ont leur memoire vive physique partitionnee virtuellement en 2 espaces:
- **l'espace noyau**
- **l'espace utilisateur**

Sur ces systemes, **le noyau est un logiciel qui est une portion du systeme d'exploitation**, gerant notamment:
- la gestion des differents **logiciels** (processus / taches)
- la gestion du **materiel** - entrees / sorties (memoire, processeur, peripherique, stockage...)
- **la communication entre les logiciels et le materiel**

Un noyau peut comporter un perimetre plus important que celui cite plus haut (notamment pour les noyaux monolithiques).

La communication entre l'espace utilisateur et l'espace noyau (= quand une fonction appelee par un programme de l'espace utilisateur demande un traitement et une execution interne au noyau puis renvoie le resultat dans le programme utilisateur) se fait par des **appels systemes**.

**Les appels systemes sont tres lourds en nombre d'instructions primitives** compares a des appels de fonctions classiques, c'est pourquoi certaines fonctions utilises souvent et de maniere intenses sont deplacees dans l'espace noyau pour plus d'efficacite (exemple: pilotes de peripheriques tres sollicites comme celui du disque dur).

On peut resumer les differentes architectures de noyaux en 2 grandes categories contraires: les noyaux monolithiques VS les micro-noyaux. 

Un **noyau monolithique (non-modulaire)** regroupe l'ensemble des fonctions du systeme et des pilotes dans son noyau sous la forme d'un seul bloc de code compilable en un seul binaire. Les premieres versions de Linux etaient a noyau monolithique non-modulaire.

A l'inverse un **systeme a micro-noyau** fait porter le minimum du perimetre au noyau appele cette fois micro-noyau, et beaucoup de fonctionnalites systeme de l'OS sont deplacees hors du noyau, en espace utilisateur, pour former le **micro-noyau enrichi**. 

**Dans la pratique, un compromis est souvent trouve entre ces 2 architectures.**   
Ainsi les versions recentes de Linux sont a **noyau monolithique modulaire:** seules les parties fondamentales du systeme sont regroupees dans un code unique, et les autres fonctions (comme les pilotes materiels) sont regroupees/separees dans differents codes/binaires, permettant une flexibilite de configuration.  
Et Windows et Mac OS sont plutot des architectures dites "**hybrides**", proches d'une architecture a micro-noyau enrichi mais en integrant tout de meme certaines choses supplementaires dans le micro-noyau pour des raisons de performances d'appels systeme. 

https://fr.wikipedia.org/wiki/Noyau_de_syst%C3%A8me_d%27exploitation

#### Distributions Linux

Une distribution est une sorte de declinaison d'OS prete a l'emploi (avec un certains nombres de logiciels -libres ou non- integres, des elements de configuration...) tout en laissant la possibilite de changer certains elements comme le noyau par exemple.

https://fr.wikipedia.org/wiki/Distribution_Linux

#### Debian

Debian est une des distributions Linux historiques (mais il existe aussi des distributions Debian basees sur d'autres noyaux que Linux), **entierement libre** (c'est plus precisement une distribution GNU/Linux), et sur laquelle se basent d'autres distributions populaires comme Ubuntu.

Avantages:
- tres adapte pour des serveurs, mais est aussi bien adapte pour des PCs ou telephones
- tres bonne securite par transparence du code source

https://fr.wikipedia.org/wiki/GNU
https://fr.wikipedia.org/wiki/Debian

Debian, comme d'autres systemes bases sur GNU, gere ses programmes sous forme de paquets (archives contenant tout ce dont le logiciel a besoin pour fonctionner), installables grace a un gestionnaire de paquets.

Pour Debian, les paquets sont au format `.deb`, ce sont des **archives**.

### Virtualisation

**https://fr.wikipedia.org/wiki/Virtualisation**

#### Definition

La virtualisation consiste a executer sur une machine hote **dans un environnement isole** des systemes d'exploitation (**virtualisation systeme**) ou des applications (virtualisation applicative).

La virtualisation peut entre autres servir pour:
- **optimiser la charge d'utilisation** d'un parc de machines physiques / **economie par mutualisation** (une machine pouvant heberger plusieurs machines virtuelles en fonction de leur charge, utile pour les serveurs, aui consomment presque la meme chose si utilises a 90% ou a 10%)
- installation, deploiement et migration facilites d'une machine physique a une autre dans un **contexte de mise en production**
- **securisation**: tests critiques / cassage sans incidence sur le systeme d'exploitation hote
- flexibilite et **scalabilite**
- allocation dynamique de puissance de calcul

Contraintes:
- performances amoindries par rapport a un mode natif
- si la machine hote tombe en panne, toutes ses machines virtuelles aussi (mais de la redondance est facilement implementable)
- mise en oeuvre complexe au depart

#### Types de virtualisation

- **Isolateur / conteneur**: avec Linux uniquement, un type de virtualisation qui n'en est est pas completement une car les conteneurs ne sont pas entierement isoles. Exemple: **Docker**
- **Hyperviseur de type 2**: logiciel qui virtualise et/ou emule le materiel pour les OS invites, de sorte que ces OS croient communiquer directement avec le materiel. Exemple: **Oracle Virtualbox**
- **Hyperviseur de type 1**: comme un noyau systeme tres leger et optimise pour gerer les acces des noyaux des OS invites a l'architecture materielle. Ex: Microsoft Hyper-V Server, KVM.

### SSH et cryptographie asymetrique

#### SSH - Secure Shell

https://fr.wikipedia.org/wiki/Secure_Shell

https://fr.wikipedia.org/wiki/OpenSSH


SSH (Secure shell) est a la fois un programme et un protocole de communication, generalement utilise pour ouvrir un shell dans un hote distant et communiquer de maniere cryptee avec cet hote au sein d'un environnement non/peu securise.  

C'est le programme de reference pour l'acces distant sur Unix et Linux.

SSH permet l'authentification ou la communication confidentielle sans mot de passe ou phrase secrete, grace a la cryptograhie asymetrique. 

#### Cryptographie asymetrique: principe

https://fr.wikipedia.org/wiki/Cryptographie_asym%C3%A9trique

Le principe de la **cryptographie asymetrique** - aussi appele **cryptographie a clef publique** - repose sur l'utilisation de **2 clefs distinctes** (pas de secret partage donc) pour le client et le serveur: 
- une **cle publique** pour chiffrer: une **fonction a sens unique** (fonction tres difficile a inverser)
- une **cle privee** pour dechiffrer: une **breche secrete** de la fonction a sens unique (le moyen d'inverser la fonction)

#### Cryptographie asymetrique pour la confidentialite

https://fr.wikipedia.org/wiki/Cryptographie_asym%C3%A9trique#Principe_g%C3%A9n%C3%A9ral

L'utilisateur qui souhaite recevoir des messages (le serveur) genere un couple cle privee / cle publique. Il conserve la cle privee pour lui seul et communique librement la cle publique. 

Tout message crypte chiffre via cette cle publique ne pourra donc etre compris que par le serveur possedant la cle privee associee, la confidentialite du message est garantie. 

Par rapport au chiffrement symetrique:
- avantages: Le chiffrement symetrique repose sur un partage prealable de la cle, qui doit donc etre communiquee entre les 2 interlocuteurs. Si ce partage est effectue dans un environnement non securise ("en clair"), cette cle peut etre compromise !
- inconvenients: moins performant (temps de traitements plus longs), et cle doivent etre plus longues pour un niveau de securite equivalent

=> au vu des inconvenients et avantages respectifs du chiffrement symetrique et asymetrique, il est generalement interessant de **combiner les 2: utiliser une premiere fois le chiffrement asymetrique pour proceder a la phase de partage de cle du chiffrement symetrique, puis poursuivre le reste de l'echange avec le chiffrement symetrique, plus rapide.**

#### Cryptographie asymetrique pour l'authentification

https://fr.wikipedia.org/wiki/Cryptographie_asym%C3%A9trique#M%C3%A9canismes_d'authentification

On a vu que pour un couple cle publique / cle privee genere, **on peut utiliser la cle publique pour chiffrer et la cle privee pour dechiffrer, mais l'inverse est aussi vrai.** 

Ainsi la cryptographie peut etre utilisee (et meme combinee avec le chiffrement de confidentialite) a des fins d'**authentification**: cela permet au serveur de reconnaitre l'expediteur du message. 

Pour cela, le client genere aussi son propre couple cle privee / cle publique, et communique cette derniere au serveur. Au moment d'envoyer le message, le client chiffre donc une premiere fois en utilisant sa cle privee, avant de le chiffrer avec la cle publique du serveur. 

Ainsi a la reception du message, apres avoir dechiffre une premiere fois avec sa propre cle privee, c'est la cle publique du client qui va pouvoir dechiffrer le message final: le client est donc reconnu par le serveur.

### Gestion de paquets - APT

https://fr.wikipedia.org/wiki/Advanced_Packaging_Tool
https://en.wikipedia.org/wiki/APT_(software)

Les systemes GNU/Linux (et d'autres) ont leur logiciels geres sous forme de **paquets**: ce sont des archives contenant les fichiers, informations et procedures necessaires a l'installation du logiciel sur un systeme d'exploitation, en s'assurant de la coherence fonctionelle du systeme modifie. 

**Sous Debian et ses derives, les paquets sont des fichiers `.deb`**

Un **gestionnaire de paquets** permet:
- **installation, mise a jour, desinstallation**
- **verification de l'integrite** des paquets
- verification des dependances logicielles
- **resolution de dependances** pour certains (APT en fait partie)

Sous Debian, le gestionnaire **APT (Advanced Packaging Tool)** est present en natif dans le systeme, et la commande `apt` est utilisee pour interagir avec.

APT est un **gestionnaire de haut niveau construit sur la base du logiciel `dpkg`** a la base des gestions de paquets Debian (https://fr.wikipedia.org/wiki/Dpkg).

**Aptitude** est une surcouche encore plus haut niveau qu'APT, qui propose notamment une interface semi-graphique (Text-based User Interface - TUI).

APT a l'avantage d'**automatiquement installer les dependances necessaires a l'installation du logiciel vise.** 

Une autre qualite d'APT est qu'il va chercher ses paquets dans des **depots APT** (qui sont des remote repositories - https://fr.wikipedia.org/wiki/D%C3%A9p%C3%B4t_(informatique) - https://doc.ubuntu-fr.org/depots), qui peuvent etre regulierement mis a jour par les constructuers de logiciels.
Ces depots sont listes dans le fichier de configuration **`/etc/apt/sources.list`** (https://manpages.ubuntu.com/manpages/xenial/man5/sources.list.5.html).    
**=> Contrairement a Windows, pas besoin de telecharger et d'installer nous-meme le logiciel, apt va le chercher dans le depot de sa source!**

APT peut donc aussi facilement verifier dans les depots si des mises a jour de logiciels existent. 

La **commande `apt`** regroupe de maniere simplifiee et mois specialisee des usages des comandes **`apt-get`** et **`apt-cache`** (https://manpages.ubuntu.com/manpages/xenial/man8/apt.8.html).

Commandes usuelles:
https://doc.ubuntu-fr.org/apt-get

```man apt``` => https://manpages.ubuntu.com/manpages/xenial/man8/apt.8.html

- ```apt[-get] update```: rechercher quels packages/dependances sont a jour ou non par rapport a leur depots listes dans le fichier `sources.list`

- ```apt[-get] upgrade```: installe les mises a jour identifiees par `apt update` si cela est possible sans supprimer des paquets ou dependances intalles. En revanche de nouvelles dependances peuventetre installees si cela n'implique pas de suppression / downgrade de packages installes => C'est une upgrade "minimale et safe"

- ```apt[-get] full-upgrade```: comme upgrade mais s'autorise a supprimer des packages si necessaire pour mettre a jour l'ensemble. 

- ```apt[-get] install <package_name>[=<version>]```: installe le package a partir de son depot.

- ```apt[-cache] show <package_name>```: montre un resume des informations sur le package (dependances, taille de telechargement, sources depuis lesquelles le package est disponible, description du contenu...)

- ```apt[-cache] policy <package_name>```: pour voir de quel depot provient un package.

- ```apt list --installed```: liste tous les packages installes

- ```apt[-get] remove <package_name>```: desinstalle un package sans supprimer ses fichiers de configuration

- ```apt[-get] purge <package_name>```: desinstalle et supprime les fichiers de configuration du package

- ```apt[-get] autoremove```: utile pour avoir un setup clean apres avoir desinstalle un package -> desinstalle les dependances de ce package qui ne sont plus requises une fois le package desisntalle.

### Ports et adresses IP

https://fr.wikipedia.org/wiki/Port_(logiciel)

https://fr.wikipedia.org/wiki/Adresse_IP

Une adresse IP permet d'identifier un peripherique au sein d'un reseau. 

Un port est un moyen d'identifier un logiciel qui utilise le reseau.

*Analogie grossiere: l'adresse IP est l'adresse d'un immeuble, et le port est le numero d'appartement. => on a donc besoin de connaitre les 2 pour acheminer des informations* 

https://fr.wikipedia.org/wiki/Redirection_de_port#L'utilit%C3%A9_des_ports

Dans certains cas, comme quand un port est deja occupe ou qu'on a intercale un routeur entre le reseau exterieur et le reseau local, on va avoir besoin d'effectuer un **port forwarding ou port mapping** : https://fr.wikipedia.org/wiki/Redirection_de_port 

La commande **`ip addr`** va notamment lister les adresses IP utilisees par la carte reseau ainsi que l'adresse de loopback et celle de broadcast.

L'adresse de 

Voir aussi:
- **Masque de sous-reseau** : https://fr.wikipedia.org/wiki/Sous-r%C3%A9seau
- **Gateway (passerelle)**: https://fr.wikipedia.org/wiki/Passerelle_(informatique)

### Loopback et Localhost

https://fr.wikipedia.org/wiki/Loopback

https://fr.wikipedia.org/wiki/Localhost

https://fr.wikipedia.org/wiki/Domain_Name_System

Une **interface loopback (abregee 'lo' sous Unix)** est une interface virtuelle d'un materiel reseau, ainsi qu'une adresse associee a cette interface, permettant au materiel, en la contactant, de **boucler sur lui-meme.**

Les adresses loopback locales en IPv4 (127.0.0.1) et IPv6 (::1) sont accessibles via le nom de domaine **localhost**, permettant la plupart de temps de **tester un comportement client-serveur sans utiliser plusieurs machines.**

### Routage

https://fr.wikipedia.org/wiki/Routage

https://fr.wikipedia.org/wiki/Table_de_routage

**Le routage est le mecanisme par lequel des chemins sont selectionnes dans un reseau pour acheminer des donnes d'un expediteur vers un ou plusieurs destinataires.**

Ce mecanisme est utilise notamment dans le reseau telephonique ainsi que les transports ou internet.

**Sa performance est capitale dans les reseaux decentralises** comme internet.

Pour afficher la routing table, executer `route -n` ou bien `netstat -rn` apres avoir installe net-tools (`apt install net-tools`), ou encore `ip route`.

### DHCP - Dynamic Host Configuration Protocol

https://fr.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol

**Le DHCP consiste a attribuer des adresses IP non fixes dans un reseau** (par exemple utilise par les FAI ayant a leur disposition moins d'adresses IP que d'abonnes, mais dont ces derniers ne sont jamais tous connectes en meme temps). 

Le process DHCP apparait dans la VM comme une connexion **UDP** (User Datagram Protocol, cf https://fr.wikipedia.org/wiki/User_Datagram_Protocol) au port 68 : c le resultat de `ss -ptunel`.

### Firewall / Pare-feu

https://fr.wikipedia.org/wiki/Pare-feu_(informatique)

Un pare-feu est un logiciel qui permet d'appliquer une politique d'acces aux ressources reseau.

Son role principal est de controler le trafic entre differentes zones de confiance, en filtrant les donnes, qui y transitent.

Le filtrage peut se faire selon des criteres d'origine, de destination, de donnees (taille, pattern...), d'utilisateurs...

Voir aussi: **TCP** - https://fr.wikipedia.org/wiki/Transmission_Control_Protocol

### Traitement de streams avec AWK

https://en.wikipedia.org/wiki/AWK

https://connect.ed-diamond.com/GNU-Linux-Magazine/glmf-131/awk-le-langage-script-de-reference-pour-le-traitement-de-fichiers

**AWK (`awk`)** est un langage dedie (https://fr.wikipedia.org/wiki/Langage_d%C3%A9di%C3%A9), sorti un peu apres `sed`, qui permet de traiter des **streams de texte** pour en extraire des donnees structurees. 

AWK travaille avec en entree des fichiers, qui peuvent etre le resultat de commandes pipees. 

Un vocabulaire est a connaitre pour utiliser correctement awk:
- **Record: portion du fichier d'entree aui va faire l'objet du filtrage par conditions** (par defaut la separation des records se fait par le newline character -> un record est dans ce cas une ligne)
- **Field: portion du record** (par defaut la separation se fait par des espaces / tab), les fields correspondent a la sortie d'un split.

Ainsi par defaut un fichier va etre vu comme cela par AWK: 
```
field1 field2 ... fieldN1 <= record1
... 
field1 field2 ...  ... fieldNN <= recordN
```

La structure d'un script AWK est une serie de couples conditions / actions sous la forme

```
condition { action }
condition { action }
...
```

Pour executer directement une commande awk, la syntaxe de la ligne de commande doit etre:

```
awk '<program text>'
```


- Une **condition** peut etre une condition booleenne sous forme de **"awk expression"**, ou bien **`BEGIN`** ou **`END`** (pour executer l'action associee avant ou apres lecture de tous les records). L'operateur **`~`** permet de matcher une **regex** plutot qu'une string.
**Cette condition va filtrer les records respectant cette condition et realiser l'action associee.**  
La syntaxe de condition **`<expr1>, <expr2>`** rend une condition vraie a partir du moment ou `expr1` est vraie, jusqu'au moment ou `expr2` est vraie inclus, puis ce schema se reproduit. 
_La condition par default est de matcher tous les records._

- Une **action** est une serie de **commandes**, qui peuvent etre des appels de fonctions, des assignations de variables, calculs etc.  
_L'action par defaut est de print le record._

Commandes usuelles:
- `print` ou `print $0`: affiche le record
- `print $<i>`: affiche le field i du record
- `print $<i>, $<j>`: affiche le field i et le field j du record, separes par un OFS (par default un espace)
- `printf <args>`: comme printf dans C

**Note: on peut egalement creer des user-defined functions avec la meme syntaxe que C.**

Variables courantes:
- **FNR**: File Number of Records -> nombre de records lu jusqu'a present dans le fichier courant (remis a zero quand on change de fichier d'input)
- **NR**: Number of Records -> nombre total de records lu jusqu'a present
- **NF**: nombre de fields du record courant
- **FILENAME**: nom du fichier d'input courant
- **FS**: Field Separator (defaut: whitespace" - sequence de spaces et tabs)
- **RS**: Record Separator (defaut : newline)
- **OFS**: Output Field Separator (defaut: space)
- **ORS**: Output Record Separator (defaut: newline)
- **OFMT**: Output Format pour les outputs numeriques (defaut: "%.6g")

### Centralisation des logs avec journalctl

https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs-fr#filtrer-par-interet-des-messages

`journalctl` est un programme associe a `systemed` qui permet de centraliser les logs de tous les processus du noyau et de l'espace utilisateur. 

### Cron et Crontab

https://fr.wikipedia.org/wiki/Cron

`cron` est le programme qui permet de manager les `crontab`, qui sont une contraction de "chrono table", faites pour une **execution periodique et systematique de commandes** (grace au daemon `crond`). 

**Chaque crontab est un fichier propre a chaque utilisateur, et il est deconseille de l'editer directement en accedant a son chemin.** 

**=> Il vaut mieux utiliser pour cela la commande `crontab`:**

- Pour editer:
```
crontab -u <user> -e
```

- Pour consulter:
```
crontab -u <user> -l
```

## Creer son Serveur Debian avec Virtualbox

https://fr.wikipedia.org/wiki/Oracle_VM_VirtualBox

- creer une nouvelle machine virtuelle et allouer 1Go de RAM. Pour info, commande pour connaitre la memoire totale de la machine: `grep MemTotal /proc/meminfo`.
- Creation du Disque Dur Virtuel:
	- Type de hard disk file: image VDI (le format d'images par defaut de Virtualbox). Une image VDI est le fichier cree par Virtualbox quand on cree une machine virtuelle (https://www.eugenetoons.fr/utiliser-un-fichier-vdi-dans-virtualbox/). **Une image systeme est une archive qui stocke l'etat entier d'un ordinateur** (a des fins de duplication ou de backup). **Utiliser directement une image VDI prete a l'emploi permet de s'affranchir de certaines etapes prealables a l'installation de l'OS invite.**
	- **Taille fixe**: elle ne pourra plus etre augmentee, mais a l'avantage de fournir des performances proches d'un disque natif, la ou les performances sont degradees au fur et a mesure de l'augmentation de l'espace d'un disque dynamiquement alloue (car des operations d'augmentation de capacite precedent les operations d'ecriture). La creation d'un disque de taille fixe estp lus longue mais le temps perdu au depart est gagne a l'utilisation (https://superuser.com/questions/381351/fixed-size-disk-vs-dynamically-allocated-is-there-a-performance-difference-on-a)
	- choisir la taille fixe a allouer (depend si l'on fait les bonus du sujet ou pas) et confirmer l'emplacement d'enregistrement de l'image vdi.

- VM eteinte, **changer le Graphics Controller de VMSVGA vers VBoxVGA** dans Settings/Display pour eviter des messages d'erreur (sans gravite) au demarrage de l'OS a cause d'un bug de VMSVGA: https://www.virtualbox.org/ticket/19168#comment:4
- aller chercher **l'image iso "netinst" pour PC 64 bits**, telechargee via https://www.debian.org/distrib/. 
- **Monter l'image VDI dans Optical Disk pour booter sur l'installeur Debian:**  

	![capture](img/optical_disk.png)
- Lancer la machine

### Installation de Debian

https://www.debian.org/releases/stable/s390x/ch06s03.fr.html

- Install Debian
- choisir la lange, la localisation, la locale, le type de clavier...
- donner un hostname a la machine: "acostes42"
- donner un nom de domaine: laisser vide
- creer le mot de passe root, un utilisateur principal (acostes) et definir son mot de passe
- pour faire les bonus, passer a un setup manuel des partitions

### Strategie de partitionnement

https://www.debian.org/releases/stable/s390x/apcs01.fr.html  
https://www.debian.org/releases/stable/s390x/apcs02.fr.html

![arborescence de fichiers](img/folder_architecture.png)

Sans partitionnement, tous les dossiers ci-dessus sont places dans le dossier racine `/` (a ne pas confondre avec `root`).
**Un partitionnement permet plus de securite** (si une partition est endommagee/corropmupe/surchargee de contenu, les autres ne le sont pas forcement).

**Le seul inconvenient est qu'il peut etre difficile de savoir quel espace allouer a l'avance a chaque partition, et repartitionner exige d'ecraser les donnees existantes.**

### LVM

https://fr.wikipedia.org/wiki/Gestion_par_volumes_logiques  
https://unix.stackexchange.com/questions/87300/differences-between-volume-partition-and-drive
https://tldp.org/HOWTO/LVM-HOWTO/whatisvolman.html

Un moyen de gerer le partitionnement de maniere plus flexible en etant moins dependant des limites de chaque disque physique est d'utiliser un **LVM (Logical Volume Manager)**. 

Un LVM permet de **regrouper plusieurs volumes physiques en groupes de volumes VG, qui peuvent ensuite etre subdivises en volumes logiques LV**, equivalents a des pseudos-partitions.

On peut ensuite faire evoluer la taille et la repartition de ces partitions logiques quasiment a loisir.

### Obtenir le partitionnement demande dans le sujet

#### Objectif et notations

https://en.wikipedia.org/wiki/Disk_partitioning

**ATTENTION: SI LE VDI EST STOCKE SUR SGOINFRE, DIMINUER LA TAILLE DE LA VM CAR SGOINFRE SUPPRIME REGULIEREMENT LES CONTENUS SUPERIEURS A 30GB!** https://meta.intra.42.fr/articles/sgoinfre-s-rules

Pour des conseils sur les tailles usuelles mnecessaires de partitions, cf https://www.debian.org/releases/bullseye/amd64/apds02.en.html.

Le sujet demande (dans les bonus) d'avoir une structure de partitionnemt comme suit quand on execute la commade `lsblk` ('list block devices' - cf `man lsblk` et https://unix.stackexchange.com/questions/259193/what-is-a-block-device): 

![partitioning](img/goal_partitioning.png)

- `sd<lettre>`: la lettre numerote les differents **disques physiques** (type: 'disk')

	- `sda<chiffre>`: le chiffre numerote la **partition** du disque physique 'a' (type: part)

`sda5_crypt` indique que la partition 5 est **cryptee** (type: 'crypt'): cela permet en cas de vol du materiel de ne pas acceder aux donnes (besoin de connaitre la **key** du proprietaire - dans notre cas via une **passphrase**)

sda5 est divisee en plusieurs **volumes logiques (LV)** dans un **groupe de volumes (VG)** appele 'LVMGroup'.

sda2 est cree automatiquement pour heberger les volumes logiques de sda5, c'est pourquoi il ne contient que tres peu d'espace: 1K - correspondant a 2 blocs de 512 octets - a priori 1 bloc pour l'**Extended Boot Record** (cf https://en.wikipedia.org/wiki/Extended_boot_record) et 1 bloc supplementaire pour en avoir un nombre pair (cf https://tldp.org/LDP/sag/html/partitions.html).
En effet, **pour creer une logical partition ou logical volume, il faut d'abord creer une extended partition** parmi les 4 partitions autorisees pour les contenir (https://help.ubuntu.com/community/HowtoPartition/PartitioningBasics et https://tldp.org/HOWTO/Partition/requirements.html#number).   
Dans notre cas sda2 est une extended partition contenant les blocs des partitions logiques, on le voit en executant la commande `fdisk -l` (cf https://unix.stackexchange.com/questions/71821/mystery-of-a-small-1k-hard-disk-partition-and-is-it-safe-or-malware-on-ubuntu-1).

*Attention: lsblk et VirtualBox raisonnent en termes de taille dedisque en utilisant des GiB, Mib etc, c'est a dire en base 2 (cf. https://en.wikipedia.org/wiki/Byte#Units_based_on_powers_of_2), tandis que l'installeur Debian raisonne en base 10. => 1 GiB = 1.024 * 1.024 * 1.024 GB. Il faut donc realiser la conversion en choisissant les tailles de partition dans l'installeur.*

#### Setup de la partition table lors de l'installation de Debian

- Definir une installation manuelle
- creer une partion primaire sda1, avec systeme de fichiers ext4, et mountpoint /boot (*Pas besoin de definir de bootflag car GRUB va se charger de la gestion du boot.* cf https://en.wikipedia.org/wiki/Boot_flag#:~:text=A%20boot%20flag%20is%20a,Any%20other%20value%20is%20invalid)
- creer un encrypted volume pour le reste de l'espace (le contenu du disque va etre efface avant pour assurer une meilleure securite)
- configurer un LVM pour la partition cryptee
- creer un groupe de volumes qu'on appellera 'LVMGroup' 
- ajouter les LVM un a un en les nommant sans la partie "LVMGroup-" apparaissant dans le resultat de `lsblk`, leur nom sera automatiquement prepend du nom de groupe auquel ils appartiennent
- definir un systeme de fichiers ext4 pour tous les volumes logiques sauf swap, qui doit juste etre definie comme "swap area" dans son use case, et definir leur mountpoint (sauf pour swap)

**Une Swap Area est une portion de disque dur qui peut etre utilisee en cas de depassement de la memoire RAM.** https://web.mit.edu/rhel-doc/5/RHEL-5-manual/Deployment_Guide-en-US/ch-swapspace.html#:~:text=Swap%20space%20in%20Linux%20is,a%20replacement%20for%20more%20RAM.

### Finalisation de l'installation de Debian

- Deselectionner tous les sofwares optionnels pour ne pas les installer
- Installer **GRUB boot loader** sur la partition primaire

### Modifications du partitionnement si besoin

Les commandes de `lvm2` peuvent servir a divers choses comme renommer des VG (`vgrename oldname newname`) et des LV (`lvrename vg oldname newname`). 

![rename](img/lvrename.png)

*Pour pouvoir utiliser lvm il faut ajouter /sbin a la variable PATH (cf plus loin).*

Pour examiner le resultat on peut utiliser la commande `lsblk` ou bien `fdisk -l`. 

*Note : Pour scroller dans un resultat de terminal dans la VM, il faut installer screen (`apt install screen` en tant que superuser), y ouvrir une session de terminal (`screen`) et utiliser le raccourci clavier de la commande copy (https://www.gnu.org/software/screen/manual/screen.html#Copy)*

## Dernieres installations et administration

### Installations facultatives mais utiles

- `apt install man[-db]`
- `apt install screen`

### Ajout permanent de /sbin a la variable PATH

*Note: pour verifier depuis quel chemin s'execute un programme, faire `which <program_name>`.*

La ligne suivante permet d'ajouter `/sbin` a la variable PATH pour executer certaines commandes comme `adduser`, `deluser`, `visudo`, `lvm` (...) et ses derives meme quand on n'a pas demarre une session en tant que root: 

```
export PATH=/sbin:$PATH
```

Mais **cette action n'est pas persistante**, une fois la session utilisateur redemarree, la variable retourne a son etat initial. 

**Pour modifier cette variable de maniere permanente et pour tous les utilisateurs, il faut aller modifier le script `/etc/profile` qui s'execute a chaque demarrage de session.** (https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix)

On voit d'ailleurs dans ce fichier que par defaut au demarrage de session, le script verifie si on est en tant que root (le userID est 0 pour root) pour determiner quelle variable PATH utiliser (et inclut bien deja sbin si on demarre la session en tant que root).

### Mettre en place une Password Policy

https://www.server-world.info/en/note?os=Ubuntu_20.04&p=password

- s'assurer que les passwords acutellement choisis pour les utilisateurs existants (incluant root) sont corrects au vu de la policy choisie, sinon le PASS_MIN_DAYS peut etre bloquant une fois modifie par `chage`. 

- modifier PASS_MAX_DAYS, PASS_MIN_DAYS et PASS_WARN_AGE dans `/etc/login.defs/` (cf `man login.defs`)

- **ATTENTION**: les changements precedents ne s'appliquent qu'aux nouveaux utilisateurs (https://unix.stackexchange.com/questions/193593/password-policy-on-existing-accounts-not-updated-after-making-changes-to-login-d). Pour les appliquer a un user existant, executer:
	```
	chage -m <PASS_MIN_DAYS> -M <PASS_MAX_DAYS> -W <PASS_WARN_AGE> <user>
	```
	(ne pas oublier de le faire galement pour root)

- Pour verifier le resultat sur un utilisateur, executer ```chage -l <user>```

- installer la lib PAM pwquality: `apt install libpam-pwquality`

- identifier les parametres a modifier en les cherchant dans `man pam_pwquality` (astuce si on ne se rappelle plus du nom du man: ecrire `man pam` puis faire `TAB`): 'retry', 'minlen', 'ucredit', 'dcredit', 'lcredit', 'maxrepeat', 'usercheck', 'difok', 'enforce_for_root'.

- modifier les parametres precedents dans le fichier `/etc/security/pwquality.conf`

- Pour changer le password de l'utilisateur courant afin d'appliquer la nouvelle password policy: `passwd`.

- Pour changer le password root, se connecter via `su` ou `sudo` etexecuter`passwd`. 

### Parametrages d'utilisateurs

#### Modifications

- pour ajouter un utilisateur: `adduser <user>`. Cette commande est plus haut niveau, plus pratique et simple que `useradd` (https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/). En effet elle automatise la demande de creation de password, l'entre d'informations utilisateur, la copie de certains dossiers...)

- de meme, pour le supprimer: `deluser --remove-home <user>`.

- pour ajouter un groupe: `addgroup <group>` et `delgroup <group>` pour le supprimer

- pour ajouter un utilisateur a un groupe existant: `adduser <user> <group>` (*ou bien `usermod -aG <group> <user>`, plus bas niveau*)

- pour enlever un utilisateur d'un groupe: `deluser <user> <group>`

*Creer un nouvel utilisateur est l'occasion de verifier que la password policy s'applique.*

**Ne pas oublier de creer le groupe 'user42' et d'ajouter le user principal a ce groupe, comme demande dans le sujet.**

#### Consultation

https://devconnected.com/how-to-list-users-and-groups-on-linux/#:~:text=In%20order%20to%20list%20groups,groups%20available%20on%20your%20system.

Les informations sur les groupes et les utilisateurs sont stockees respectivement dans les fichiers de configuration `/etc/group` et `/etc/passwd`. Un moyen de les lister sans en connaitre le chemin est d'utiliser la commande **`getent`**(cf`man getent`), a laquelle on peut piper un `grep`, `cut` ou `awk` pour acceder aux infos sur un utilisateur ou groupe en particulier.

Une maniere de faire apparaitre les infos utilisateur de maniere plus directement lisible est d'utiliser la commande **`id [<user>]`**. Cette commande va afficher les id puis noms respectifs de l'utilisateur, de son groupe principal et de tous les autres groupes auxquels il appartient.

### Superuser, su, sudo

**https://documentation.suse.com/sles/15-SP2/html/SLES-all/cha-adm-sudo.html**

**La page du man de sudoers contient toutes les infos et explications necessaires a une bonne configuration de sudo: https://manpages.ubuntu.com/manpages/xenial/en/man5/sudoers.5.html**

La commande `su` permet de se logger en superuser ou 'root', possedant tous les droits d'administration possibles. Comme l'utilisation generalisee d'un tel profil est tres dangereuse, on peut choisir de se mettre en superuser uniquement pour l'execution d'une seule commande, en precedant cette commande de `sudo`. 

Pour cela il faut au prealable installer sudo: `apt install sudo`.

Si l'on s'est logge en superuser avec `su`, pour sortir de ce mode, faire CTRL+D ou taper `exit`.

Pour executer sudo, il faut faire partie des **sudoers**. Les utilisateurs ou groupes peuvent etre ajoutes aux sudoers soit en modifiant directement le fichier `/etc/sudoers`, ou bien en les ajoutant dans un nouveau fichier que l'on cree et place dans `/etc/sudoers.d/.` (cf `less /etc/sudoers.d/README`)  
**L'avantage de creer des nouveaux fichier dont les effets vont s'ajouter au fichier sudoers initial est que si l'on veut faire revenir la configuration sudo a son etat d'origine, il suffit de supprimer ces fichiers, sans alterer le fichier sudoers d'origine.**  

https://www.hostinger.com/tutorials/sudo-and-the-sudoers-file/#:~:text=Sudoers%20File%20Syntax,-You%20can%20open&text=%ADmin%20ALL%3D(ALL)%20ALL,privileges%20to%20run%20any%20command

Exemple de syntaxe de base pour ajouter des droits via un fichier sudoers:

- a un utilisateur: 
	```
	<user> ALL=ALL
	```  
- a un groupe:
	```
	%<group> ALL=ALL
	```
ou le premier ALL veut dire "all hosts" et le deuxieme "for all commands"

Pour plus de details sur la syntaxe des fichiers sudoers, voir https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file et `man sudoers`, et se rappeler de la regle enoncee par le man de sudoers: 

__*The basic structure of a user specification is “who where = (as_whom) what”.*__ 

**_Note: Une erreur de syntaxe dans un fichier sudoers peut avoir de lourdes consequences. Il est donc preferable d'editer ces fichiers via la commande `visudo` en tant que root, qui integre une verification de lasyntaxe sudo avant l'enregistrement._**

Quand on affiche le contenu du fichier sudoers d'origine, on remarque une ligne: 

```
# Allow members of group sudo to execute any command
%sudo	ALL=(ALL:ALL) ALL
```

**Une maniere plus simple (et plus robuste, car on peut plus facilement retirer les droits a l'utilisateur si besoin) d'accorder tous les droits via sudo a un utilisateur est de l'ajouter au groupe existant 'sudo'** (voir plus haut comment ajouter un user a un groupe). On peut consulter la liste des users appartenant au groupe sudo en executant `grep sudo /etc/group`, ou verifier a quels groupes appartient l'utilisateur logge via la commande `groups`, ou bien `getent group | grep sudo`.

_Attention: parfois, pour que les changements soient applicables, il faut se relogger: `logout` puis se logger de nouveau_

Pour definir la strict policy exigee par le sujet pour sudo, creer un fichier sudoers (`visudo /etc/sudoers.d/my_sudoers_conf` en tant que root) contenant:

_Pour trouver sur quels parametres on peut jouer dans un fichier de config sudoers, cf `man [5] sudoers` puis rechercher `SUDOERS OPTIONS` (utiliser `/` pour la recherche puis `n` et `SHIFT+n`)_

```
Defaults	env_reset
Defaults	passwd_tries=3
Defaults	badpass_message="Bad password. FOCUS PLEASE!"
Defaults	logfile=/var/log/sudo/sudo.log
Defaults	log_input, log_output
Defaults	iolog_dir=/var/log/sudo/
Defaults	iolog_file=%{user}/XXXXXX
Defaults	requiretty
```

Le `logfile` se charge des logs de sudo (indiqunt seulement qui a tente d'utiliser quelle commande avec sudo, et c'est aussi la que sont logges les avertissements de depassement e `passwd_tries`), c'est donc differents des logs d'I/O (voir ci-dessous). *Ces "**sudo logs**" sont optionnels, pas demandes dans le sujet.* 

Les logs d'entree/sortie (I/O) sont geres par les variables `log_input`, `log_output`, `iolog_dir` et `iolog_file`. Cette fois, ils recordent toutes les entrees/sorties des commandes utilisees via sudo. Ils ne produisent pas un seul fichier de log contrairement aux sudo logs, mais un dossier par commande, contenant differents fichiers. Les plus importants ici sont: 
**- `log`: contient le log d'input**
**- `ttyout`: contient le log d'output, doit etre decompresse avec zcat ou zless**

On peut choisir la structuration qu'on veut pour ces logs. Ici j'ai choisi que chaque structure de log d'I/O sera non pas stockee dans le dossier par defaut `/var/log/sudo-io` mais dans le dossier `/var/log/sudo`. 

Ensuite, la structure de chaque log est determinee par `iolog_file` comme suit: `%{user}` permet de rassembler tous les dossiers de log d'actions sudo executees par un utilisateur dans un dossier portant comme nom son login, puis chaque commande loggee de cet utilisateur sera stockee sous la forme d'un sous-dossier cree automatiquement sous la forme d'une chaine de 6 caracteres (mis en place par le `XXXXXX` a la fin de la variable, cf le man de sudoers). *En effet, si le dossier de log d'une commande existe deja, il sera ecrase, donc ne pas ajouter les `XXXXXX` a la fin reviendrait a ne logger que la derniere commande sudo effectuee par chaque utilisateur.*

Chaque sous-dossier contient alors l'architecture de logs citee plus haut (`log`, `log.json`, `stdin`, `stdout`, `stderr`, `ttyin`, `ttyout`...). 

**Un moyen de revoir visuellement en "temps reel" l'execution d'une commande sudo dont les I/O ont ete loggees est d'executer `sudoreplay -d <iolog_dir> <iolog_file du log que l'on veut voir>`.**

*Note: Si on ne se rappelle plus des noms de sous-dossiers produits par iolog_file, on peut auparavant executer la commande `sudoreplay -d <iolog_dir> -l` pour lister les differentes commandes loggees et leurs iolog_files associes.*

*Note2: si jamais on veut securiser plus l'utilisation de sudoreplay afin qu'il ne risque pas de boucler sur lui-meme si on l'utilise via sudo (meme si je n'ai pas reussi a reproduire ce probleme), on peut suivre la procedure permettant de ne pas inclure les commandes sudoreplay dans les logs: https://yojimbosecurity.ninja/sudo-logging-2/)*

**Pour les raisons de securitepoussant a setup requiretty (c'est notamment le fait d'interdire d'acceder programmatiquement a sudo):**
https://stackoverflow.com/questions/67985925/why-would-i-want-to-require-a-tty-for-sudo-whats-the-security-benefit-of-requi

La variable `Defaults	secure_path` du fichier sudoers d'origine permet de s'assurer que lors de l'execution de sudo, la variable PATH est temporairement remplacee par celle-ci.

Derniere modification pour plus de securite (pas demande dans le sujet): interdire aux utilisateurs sudo d'executer la commande `sudo su`. En effet cette commande permet de passer en mode root sans meme rentrer une seule fois le mot de passe du root ! Pour cela, editer le sudoers general: 

```
sudo visudo
```

Puis remplacer la ligne donnant les permissions au groupe sudo par:

```
%sudo	ALL=(ALL:ALL) ALL, !/bin/su
```

A vrai dire, Michael W Lucas explique que cette securite peut etre contournee simplement en copiant au prealable `/bin/su/' dans un autre emplacement puis en executant ce dernier, et donc plus generalement que **ca ne sert a rien d'exclude/negate des commandes dans sudoers'** 😕

*__Autres bonnes/mauvaises pratiques pour sudo par Michael W Lucas: https://www.bsdcan.org/2014/schedule/attachments/283_2014-04-29%20sudo%20tutorial%20-%20bsdcan%202014.pdf__*

### systemctl

https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units-fr

`systemctl`est la commande pour interagir avec **systemd**, un gestionnaire de systemes, et comportant notamment un systeme d'initialisation pour Linux (https://fr.wikipedia.org/wiki/Systemd).

systemd permet notamment de decrire quels **services/daemons** (cf. https://fr.wikipedia.org/wiki/Daemon_(informatique)) sont appeles au demarrage ou bien quelles sont leur dependances.  

Commandes usuelles:

-  `systemctl start <service>[.service]`: demarre un service
- `systemctl stop <service>[.service]`: arrete un service en cours d'execution
- `systemctl restart <service>[.service]`: redemarre un service
- `systemctl reload <service>[.service]`: si le service le permet, applique les changements effectues aux fichiers de configurations du service sans le redemarrer
- `systemctl reload-or-restart <service>[.service]`: reload si le service le permet, sinon restart.
- `systemctl enable <service>[.service]`: lance un service au demarrage => cela va creer un lien symbolique du fichier de service du systeme dans le dossier ou systemd cherche les fichiers de demarrage automatique (dans `/etc/systemd/system/<target>.target.wants`, ou ,<target> est la target qui "wants" le service)
- `systemctl disable <service>[.service]`: desactive le demarrage automatique d'un service
- `systemctl status <service>[.service]`: affiche l'etat general d'un service
- `systemctl is-enabled <service>[.service]`: affiche si le service est lance automatiquement au demarrage
- `systemctl cat <service>[.service]`: affiche le fichier de l'unite tel que reconnu par systemd (cf `man 5 systemd.service`)

### AppArmor

AppArmor est un logiciel de securite GNU pour Linux permet d'utiliser le **Mandatory Access Control (MAC)**, en complement du modele de Discretionary Access Control (DAC) implemente sous Unix.

Le controle d'acces obligatoire doit etre utilise quand la politique de securite SI exige que **les decisions de protection ne doivent pas etre prises par le proprietaire des objets concernes, mais doivent lui etre imposees par le systeme.**
https://fr.wikipedia.org/wiki/Contr%C3%B4le_d%27acc%C3%A8s_obligatoire

Au contraire, dans le cas d'un controle d'acces discretionnaire, un utilisateur ayant une certaine autorisation d'acces a un element peut transmettre cette permission (directement ou indirectement) a n'importe qui d'autre. https://fr.wikipedia.org/wiki/Contr%C3%B4le_d%27acc%C3%A8s_discr%C3%A9tionnaire

Pour verifier qu'AppArmor s'execute bien au demarrage:

```
systemctl status apparmor
```

ou 

```
systemctl is-enabled apparmor
```

Pour voir le statut des profils AppArmor: 

```
aa-status
```

Pour plus d'infos sur l'utilisation d'AppArmor:
- https://medium.com/information-and-technology/so-what-is-apparmor-64d7ae211ed

- https://documentation.suse.com/sles/15-SP1/html/SLES-all/cha-apparmor-commandline.html#:~:text=32.7.,-3.6%20aa%2Denforce&text=The%20enforce%20mode%20detects%20violations,permit%20them%2C%20use%20complain%20mode.

### Setup du serveur SSH

**SSH est le client et SSHD (SSSH Daemon) est le serveur.**

Installation du package: `apt[-get] install ssh` ou `apt[-get] install openssh-server`

Documentation serveur SSH: `man sshd` et `man sshd_config`

Documentation client SSH: `man ssh` et `man ssh_config`

1. Configuration cote serveur: editer le fichier `/etc/ssh/sshd_config` (https://doc.ubuntu-fr.org/ssh#configuration_du_serveur_ssh) => decommenter et changer le port a "4242" et le PermitRootLogin a "no".

3. Application des changements: `systemctl restart ssh`

3. Verification: `systemctl status ssh` en tant que root.

4. Autre verification: `ss -ptunel`, qui affiche les ports sous la forme suivante:
	- p: affiche les process
	- t: affiche les connexions tcp
	- u: affiche les connexions udp
	- n: affiche les ports au format numerique
	- e: affiche des informations etendues
	- l: affiche les ports en ecoute ("listening")

*__Pas besoin dans notre cas__ (cf. https://serverfault.com/questions/343533/changing-ssh-port-should-i-modify-only-sshd-config-or-also-ssh-config -*
*Configuration du port par default utilise cote client: editer le fichier `/etc/ssh/ssh_config` (https://doc.ubuntu-fr.org/ssh#configuration_du_client_ssh) => decommenter et changer le port a "4242"*

### UFW (Uncomplicated FireWall)

UFW est un frontend rendant plus facile l'utilisation du programme **iptables**.

iptables est le programme grace auxquel l'admin systeme peut configurer les chaines et regles dans le **pare-feu Netfilter** en espace noyau Linux (cf https://fr.wikipedia.org/wiki/Iptables et https://fr.wikipedia.org/wiki/Netfilter)

Documentation: `man ufw`

https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands-fr

1. Installation: `apt[-get] install ufw`

2. Activation au demarrage + redemarrage: `ufw enable`

3. Autorisation des connexions ssh (port 4242): `ufw allow 4242`

4. Verifier les regles ([en montrant leurs NUM]): `ufw status [numbered]` 

Si besoin de supprimer une regle: `ufw delete <RULE>` ou `ufw delete <NUM>`

### Se connecter a la VM depuis la machine hote

Commande client SSH pour se connecter a un shell dans une machine guest: 

```
ssh <user>@<guest_ip> -p <port>
```

Ici:
- guest_ip = localhost ou 127.0.0.1 (cf `ip addr`)
- port = 4242

Pour l'instant ca ne va pas fonctionner car avec Virtualbox il faut oblgatoirement creer un **port forwarding / port mapping**: 

1. Dans Virtualbox, VM eteinte, aller dans Settings -> Network -> Advanced -> Port forwarding et ajouter une regle de port mapping. *Par exemple, pour ssh, ajouter une regle 'ssh' avec pour host port 4141 (pas 4242 car deja utilisee sur les machines 42) et pour guest port 4242.*

Note: pour verifier sur la machine hote si un port est deja utilise, executer la commande `ss -ptunel | grep <port>` et verifier que le resultat est vide (note : ss remplace netstat, cf `man ss`).

2. relancer la commande `ssh <user>@localhost -p <host port>` apres avoir relance la VM.

3. s'assurer au'on n'a pas le droit de se logger depuis l'exterieur en root: `ssh root@localhost -p <host port>` (not: par contre, une fois logge, un utilisateur autorise connaissant le mot de passe root pourra toujours executer `su`)

_**Si besoin, on peut aussi transferer des fichiers depuis la machine hote vers la VM via SSH grace a la commande `scp`: cf le chapitre "Transfert du script de la machine hote vers la VM via SSH")**_

### Annuler le DHCP et passer a une IP statique

https://www.it-connect.fr/comment-configurer-une-adresse-ip-fixe-sur-debian-11/

Documentation: `man interfaces`

Dans la VM:

1. Noter l'addresse IP de la carte reseau (**"enpXsX" signifie Ethernet Network Peripheral X Serial X"**) suite a la commande `ip addr`: par exemple 10.0.2.15/24 (note: ici /24 est le masque de sous-reseau en notation CIDR)

2. Noter l'adresse de passerelle par defaut (Default Gateway, qui correspond a la Gateway de la ligne 'Default' quand on entre `route` sans le '-n'. Par exemple 10.0.2.2

3. Noter le name server (https://en.wikipedia.org/wiki/Name_server) en affichant `cat /etc/resolv.conf`: par exemple 10.0.2.3

4. modifier le fichier `etc/network/interfaces`:
	```
	iface enp0s3 inet static
 	address <address>
 	gateway <default_gateway>
 	dns-nameservers <name_server>
	```

5. Ajouter si besoin les DNS publics de google si jamais notre premier DNS ne fonctionne plus, en ajoutant dans `/etc/resolv.conf` les lignes:
	```
	nameserver 8.8.8.8
	nameserver 8.8.4.4
	```

6. redemarrer le service reseau: 
	```
	systemctl restart networking
	```

7. rebooter la machine:
	```
	reboot
	```

8. Tester l'acces a internet en envoyant un ping au serveur de google: `ping -c 10 8.8.8.8` (cf https://fr.wikipedia.org/wiki/Google_Public_DNS et https://www.whatsmydns.net/articles/8-8-8-8.html)

9. Verifier que la ligne DHCP a disparu en resultat de `ss -tunlp`

10. Tester cette fois l'acces a internet via des noms de domaine: `ping -c 10 www.google.com`. Si ca ne fonctionne pas, rebooter et reessayer.

### Broadcasting periodique du monitoring

Objectif: broadcaster toutes les 10 minutes sur tous les terminaux des infos sous la forme: 

![](img/monitoring_script.png)

#### Creation du script

Pour des raisons de portabilite (en fonction du systeme, l'emplacement du programme pour executer le script n'est pas toujours au meme endroit), demarrer le script par un **shebang** en premiere ligne (https://fr.wikipedia.org/wiki/Shebang):

```
#! /usr/bin/env bash
```
=> Le script `monitoring.sh` s'executera donc via le programme `bash` trouve dans l'emplacement propre au systeme (grace a la commande `env`).    

Commandes utiles pour le script:
- `uname -a`: affiche toutes les informations systeme
- `cat /proc/cpuinfo`: affiche les infos CPUs
- `free`: affiche les infos memoire
- `df`: ("disk free") affiche les infos espace disque
- `top -bn1`: affiche les informations de performances a l'instant t
- `who`: affiche des infos de logging et de boot
- `lsblk`: affiche la table de partitionnement
- `ss -t`: affiche les connexions TCP
- `users`: affiche les utilisateurs logges
- `ip address`: affiche des infos IP
- `journalctl`: affiche des logs de process (systemd journal) **- a lancer en tant que root -**

Liens utiles:
- que faire de "udev" et "tmpfs" dans `df`: https://askubuntu.com/questions/1150434/what-is-udev-and-tmpfs
- que veulent dire "niced" et "un-niced" dans le `man top`: https://askubuntu.com/questions/812144/what-exactly-is-meant-by-a-niced-and-an-un-niced-user-process/812160#812160
- comment considerer la charge CPU dans `top`: https://www.howtouselinux.com/post/cpu-utilization-us-sy-wa-means-in-ubuntu-linux-linux-performance
- syntaxe des `if` en bash: https://buzut.net/maitriser-les-conditions-en-bash/
- utilisation de `journalctl`: https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs-fr#filtrer-par-interet-des-messages

#### Transfert du script de la machine hote vers la VM via SSH

Une commande ssh permet de transferer des fichiers entre 2 machines connectees.

Si on a cree le script sur la machine hote, on peut donc le transferer en utilisant la commande `scp`:

```
scp -P <port> <host_path> <user>@<guest_ip>:<destination_path>
``` 

Pour rappel ici:
- guest_ip = localhost
- port = 4141

Il faut choisir un destination_path qui n'est pas seulemet reserve au root (car on a interdit le logging via root en ssh). 

On peut alors se logger dans la VM via `ssh` puis se mettre en root pour deplacer le fichier vers un emplacement pertinent (par exemple /usr/sbin - cf `man hier`).

#### Edition de la crontab

Le script doit etre execute par root pour un bon fonctionnement de sa commande `journalctl`. Les crontab etant propres a chaque utilisateur, il nous faut donc **editer la crontab de l'utilisateur root**:

```
crontab -u root -e
```

Entrer la ligne suivante pour executer le script de monitoring toutes les 10 minutes: 

```
*/10 * * * * bash /usr/sbin/monitoring.sh
```

Pour verifier que la crontab est bien a jour: 
```
crontab -u root -l
```
## Bonus: creation d'un serveur web et d'un site Wordpress

### Prerequis

https://fr.wordpress.org/support/article/before-you-install/

https://fr.wordpress.org/about/requirements/

#### Setup de PHP

https://www.php.net/manual/en/install.unix.debian.php

Installer php:

```
apt[-get] install php
```

Suite a cela, php installe generalement des dependances Apache2 qu'il va falloir desinstaller pour utiliser lighttpd a la place:

Pour verifier la presence du service Apache2: `systemctl status apache2`

Desinstaller le package apache2:

```
apt purge apache2
```

Desisntaller ses dependances inutiles:
```
apt autoremove
```

S'assurer que le service apache2 n'existe plus:
```
systemctl status apache2
```

Et s'assurer qu'aucun de ses packages n'est plus present:
```
apt list --installed | grep apache
```

Si besoin, supprimer les dependances restantes avec `apt purge` et `apt autoremove` 

Checker la version de PHP:
```
php -v
```

#### Ajout d'eventuels modules PHP

https://make.wordpress.org/hosting/handbook/server-environment/#php-extensions

Checker la liste des modules php installes:
```
apt list --installed | grep php
```
et installer des modules manquants si necessaire.   
*Verifier au cas ou que ces dependances ne reinstallent pas des packages apache2.*

**Notamment, pour utiliser le module fastcgi-php de lighttpd, on a besoin d'installer `php-cgi`**

#### Setup du serveur HTTP: Lighttpd

Vu qu'on a desinstalle apache, il nous faut installer le serveur HTTP qui va le remplacer: **Lighttpd** (prononce 'lighty'):

```
apt install lighttpd
```
*(possibilite de faire un `apt autoremove` ensuite si suggere lors de l'installation)*

Verfier avec `systemctl` que le service lighttpd est active et enabled. 

https://fr.wikipedia.org/wiki/Hypertext_Transfer_Protocol

https://www.techopedia.com/definition/15709/port-80

Le port 80 est le port utilise pour echanger des donnees via HTTP. Il faut donc l'autoriser dans UFW pour que le serveur fonctionne:

```
ufw allow http
```

Verfier la bonne prise en compte:

```
ufw status
```

Ne pas oublier d'effectuer un port-mapping dans Virtualbox vers le port 80 (par exemple depuis le port 4343).

Tester le resultat en verifiant qu'une placeholder page s'affiche bien en tapant dans le navigateur de la machine hote:

```
localhost:<host_port>
``` 

Activer comme recommande le module FastCGI (https://fr.wikipedia.org/wiki/FastCGI) pour permettre d'utiliser des pages web dynamiques (https://fr.wikipedia.org/wiki/Page_web_dynamique), et le module fastcgi-php pour autoriser le php:

- ```
	lighty-enable-mod fastcgi
	lighty-enable-mod fastcgi-php
	```
- ```
	service lighttpd force-reload
	```
- ```
	systemctl status lighttpd
	```

- Tester avec une page simple utilisant du php, en creant un fichier `/var/www/html/info.php` contenant:
	```
	<?php
	phpinfo();
	?>
	```

Recharger la page pour tester.

*En cas de probleme, aller voir les logs dans `/var/log/lighttpd/error.log`.*

#### Setup de la BDD: MariaDB

La BDD est indispensable pour pouvoir utiliser Wordpress (cf. https://fr.wordpress.org/support/article/how-to-install-wordpress/#etape-2-creer-une-base-de-donnees-et-un-utilisateur)

https://www.digitalocean.com/community/tutorials/how-to-install-mariadb-on-ubuntu-18-04

- ```
	apt install mariadb-server
	```
- ```
	systemctl status mariadb
	```

- ```
	mysql_secure_installation
	```

- repondre "y" a toutes les questions (sauf le "change root password ?")

*Plus d'info sur l'unix-socket authentification: https://mariadb.com/kb/en/authentication-plugin-unix-socket/*

- entrer dans MariaDB en tant que root: 
	```
	mysql -u root
	```

- Creer une nouvelle base et un utilisateur admin avec tous les droits:
	```
	MariaDB [(none)]> CREATE DATABASE wordpress_db;
	MariaDB [(none)]> CREATE USER 'admin'@'localhost' IDENTIFIED BY 'WPpassw0rd';
	MariaDB [(none)]> GRANT ALL ON wordpress_db.* TO 'admin'@'localhost' IDENTIFIED BY 'WPpassw0rd' WITH GRANT OPTION;
	MariaDB [(none)]> FLUSH PRIVILEGES;
	MariaDB [(none)]> EXIT;
	```
- Retourner dans MariaDB en root (`mysql -u root`) et verifier la creation de la BDD:
	```
	MariaDB [(none)]> show databases;
	```

### Instalation de WordPress

https://fr.wordpress.org/support/article/how-to-install-wordpress/#instructions-detaillees

- Installer `wget` pour telecharger les fichiers d'installation: `apt install wget`

- Installer `tar` pour decompresser les fichiers:
`apt install tar`

- Telecharger wordpress dans la VM: `wget https://wordpress.org/latest.tar.gz`

- Decompresser l'archive: `tar -xzvf latest.tar.gz`

- Deplacer le contenu du dossier wordpress genere dans le dossier de notre page: `mv wordpress/* /var/www/html/`
- Supprimer les fichiers d'installation: `rm -rf latest.tar.gz wordpress/`

- Dans le navigateur de la machine hote, charger la page de configuration de WordPress: `http://localhost:4343/wp-admin/install.php`   
*(si php-mysql n'est pas installe, un message apparaitra. l'installer - `apt install php-mysql`, sortir de la page et revenir)*

- remplir les champs avec les elemts utilises pour la creation de la BDD pour la creation auto du fichier `/var/www/html/wp-config.php`. Si config auto impossible, creer et remplir le fichier directement dans la VM (recuperer la forme en copiant `/var/www/html/wp-config-sample.php`):
	```
	<?php
	/* ... */
	/** The name of the database for WordPress */
	define( 'DB_NAME', 'wordpress_db' );

	/** Database username */
	define( 'DB_USER', 'admin' );

	/** Database password */
	define( 'DB_PASSWORD', 'WPpassw0rd' );

	/** Database host */
	define( 'DB_HOST', 'localhost' );
	?>
	```

- changer le proprietaires des fichiers contenus dans `/var/www/html` puis les droits:
`chown -R www-data:www-data /var/www/html/` puis `chmod -R 755 /var/www/html/` (cf https://doc.ubuntu-fr.org/lighttpd#php)

- Restart lighttpd: `systemctl restart lighttd`

- poursuivre l'installation dans le navigateur

- setup le site Wordpress, qui sera directement accessible via `localhost:<host_port>`

### Installer un autre service: Docker

Suivre les instructions dans:
https://docs.docker.com/engine/install/debian/

Puis tester avec 
```
docker run hello-world
```

## Generer la signature de la VM

https://en.wikipedia.org/wiki/Sha1sum

https://en.wikipedia.org/wiki/SHA-1

**ATTENTION: SHA-1 n'est plus considere comme suffisament safe aujourd'hui.**

La commande `sha1sum` permet de calculer et verifier les **valeurs de hachage** / empreintes **SHA-1**.

SHA-1 est une **fonction de hachage cryptographique**, qui permet d'**associer des donnees de taille arbitraire a des donnes de taille fixe** grace a une **fonction a sens unique**, et donc d'**attester efficacement et rapidement de l'integrite / non-alteration de donnees, sans acceder a celles-ci**. 

![](img/hash_example.png)

Pour generer le SHA-1 de notre VM:
```
sha1sum <path_to_VM>`
```

Enregistrer ensuite ce SHA-1 dans `signature.txt` du dossier de rendu.

## Autres commandes utiles
- `shutdown -r now`: fermer correctement la machine
- `hotsnamectl` si besoin de changer le hostname
- `logout` : terminer une session
- `reboot` : redemarre la machine
- `du --si [-c] [<directory>]`: ("disk usage") indique la taille occupee (en quantite d'octets base 10, sinon remplacer `--si` par `-h` pour une base 2), dans le dossier <directory> (ou si non precise, dans le dossier courant), en cumule (pour du detail, enlever `-c`). Cf https://phoenixnap.com/kb/show-linux-directory-size#:~:text=The%20du%20command%20stands%20for,default%20in%20most%20Linux%20distributions.&text=The%20system%20should%20display%20a,of%20the%20object%20in%20kilobytes.
C'est un outil meilleur que `df` quand on veut regarder dans un dossier particulier (https://www.redhat.com/sysadmin/du-vs-df#:~:text=The%20(very%20complicated)%20answer%20can,a%20given%20directory%20or%20subdirectory.) -->
