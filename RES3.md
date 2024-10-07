# Réseaux

## Séance 1 : SSH, SFTP et Mail

### 1. SSH (Secure Shell)
- **Fonction :** Permet la connexion à distance sécurisée à un serveur ou à une autre machine.
- **Port par défaut :** 22
- **Commande principale :** `ssh utilisateur@ip_ou_nom_de_domaine`

### 2. SFTP (SSH File Transfer Protocol)
- **Fonction :** Protocole sécurisé pour le transfert de fichiers, basé sur SSH.
- **Port par défaut :** 22 (comme SSH)
- **Commandes principales :**
  - **Connexion :** `sftp utilisateur@ip_ou_nom_de_domaine`
  - **Transfert de fichiers :**
    - Télécharger un fichier : `get fichier_distant`
    - Envoyer un fichier : `put fichier_local`

### 3. Services Mail (client de messagerie)
La messagerie électronique est un des services fondamentaux d'Internet, permettant la transmission de courriers électroniques (courriels ou e-mails). Ce système repose sur des normes pour identifier les destinataires, transmettre les messages et déposer les courriels dans les boîtes aux lettres électroniques des utilisateurs.

#### Les Entités du Système de Messagerie :

1. **MTA (Mail Transfer Agent)** :
   - **Fonction :** C'est le serveur de transmission des messages électroniques. Il est chargé de trouver le serveur destinataire, de transférer les messages vers celui-ci ou de recevoir des messages d'autres serveurs. 
   - **Protocole :** SMTP (Simple Mail Transfer Protocol).
   - **Rôle pour l'utilisateur :** Correspond au serveur de mail sortant.
   - **Exemple d'utilisation dans le TP :**
     - Dans le domaine `emc.fr`, le MTA envoie le message de Jean-Bob vers le domaine `yahoo.co.uk` après avoir trouvé le serveur MTA du destinataire via une requête DNS.

2. **MDA (Mail Delivery Agent)** :
   - **Fonction :** Le MDA distribue les messages en les déposant dans les boîtes aux lettres des utilisateurs. Il permet aussi aux utilisateurs d'accéder à leurs courriers électroniques.
   - **Protocoles :**
     - **POP (Post Office Protocol) :** Permet de récupérer les e-mails en les téléchargeant sur le client de messagerie et en les supprimant du serveur.
     - **IMAP (Internet Message Access Protocol) :** Permet de gérer les e-mails directement sur le serveur, sans les télécharger ni les supprimer automatiquement.
   - **Rôle pour l'utilisateur :** Correspond au serveur de mail entrant.
   - **Exemple d'utilisation dans le TP :**
     - Lorsque Billy relève son courrier, il envoie une requête POP ou IMAP à son serveur MDA pour récupérer le message envoyé par Jean-Bob.

3. **MUA (Mail User Agent)** :
   - **Fonction :** C'est le logiciel utilisé par l'utilisateur pour lire, écrire et envoyer des courriels. Il représente le client de messagerie (par exemple, Thunderbird, Outlook, etc.).

## Séance 2 : Docker

| **Docker Conteneurs**             | **Machines Virtuelles (VM)**  |
|-----------------------------------|------------------------------|
| Partagent le noyau du système hôte | Chaque VM a son propre OS     |
| Plus légers et démarrent plus vite | Plus lourds et démarrent lentement |
| Isolation au niveau du processus  | Isolation complète au niveau de l'OS |
| Utilisent moins de ressources     | Utilisent plus de ressources  |

### 1. Introduction à Docker

- **Portabilité** : Fonctionne de la même manière sur n'importe quelle machine.
- **Légèreté** : Les conteneurs partagent le noyau du système hôte, réduisant l'utilisation des ressources.
- **Isolation** : Les conteneurs isolent les applications, évitant les conflits de dépendances.
- **Modularité** : Les applications peuvent être décomposées en services (microservices) et gérées indépendamment.

### 2. Principales commandes Docker
- **Chercher une image :**  
  `docker search <nom_image>`
- **Télécharger une image :**  
  `docker pull <nom_image>`
- **Lister les images téléchargées :**  
  `docker images`
- **Démarrer un conteneur :**  
  `docker run -it --name <nom_conteneur> <nom_image>`
- **Arrêter un conteneur :**  
  `docker stop <nom_conteneur>`
- **Supprimer un conteneur :**  
  `docker rm <nom_conteneur>`
- **Supprimer une image :**  
  `docker rmi <nom_image>`
- **Lister les conteneurs actifs :**  
  `docker ps`
- **Lister tous les conteneurs (actifs ou non) :**  
  `docker ps -a`

### 3. Gestion des volumes et des ports
- **Volumes** : Les volumes permettent de persister des données hors du conteneur. Ils sont utilisés pour partager des fichiers entre l'hôte et le conteneur, ou entre différents conteneurs.
  - Exemple de création d'un volume :  
    `docker run -v /chemin/hôte:/chemin/conteneur <nom_image>`
- **Mapping des ports** : Le mapping des ports permet de rendre un service à l'intérieur d'un conteneur accessible à l'extérieur (depuis l'hôte ou le réseau).
  - Exemple de mapping du port 80 de l'hôte au port 8080 du conteneur :  
    `docker run -p 80:8080 <nom_image>`

### 4. Réseaux Docker
Docker crée automatiquement un réseau par défaut pour les conteneurs (`bridge`). Les conteneurs dans le même réseau peuvent communiquer entre eux, tandis que ceux sur des réseaux différents sont isolés.

- **Lister les réseaux Docker :**  
  `docker network ls`
- **Créer un réseau personnalisé :**  
  `docker network create --driver bridge --subnet 172.18.0.0/16 mon_reseau`
- **Connecter un conteneur à un réseau :**  
  `docker network connect mon_reseau <nom_conteneur>`
- **Inspecter un réseau Docker :**  
  `docker network inspect <nom_reseau>`

#### Concepts réseaux :
- **Bridge** : Réseau par défaut utilisé par Docker. Les conteneurs peuvent communiquer entre eux par leur IP ou nom de conteneur.
- **Host** : Le conteneur partage directement l'interface réseau de l'hôte.
- **Overlay** : Utilisé dans les environnements multi-hôtes pour interconnecter des conteneurs sur différents hôtes Docker.

### 5. Docker Compose
Docker Compose permet de définir et de gérer plusieurs conteneurs comme un ensemble d'applications interconnectées via un fichier `docker-compose.yml`.

- **Démarrer les services définis dans le fichier `docker-compose.yml` :**  
  `docker-compose up`
- **Arrêter et supprimer les conteneurs :**  
  `docker-compose down`

## Séance 3 : DHCP : Fiche de Révision

### 1. Introduction à DHCP
Le protocole DHCP (Dynamic Host Configuration Protocol) est un protocole réseau qui permet à un serveur de fournir automatiquement des informations de configuration IP à des clients (comme la passerelle, le DNS, etc.) aux dispositifs.

- **Faciliter la gestion des adresses IP** en attribuant automatiquement des adresses à des machines.
- **Éviter les conflits d'adresses IP** en centralisant la distribution via un serveur DHCP.
- **Configurer automatiquement** d'autres paramètres réseau essentiels (comme le masque de sous-réseau, les serveurs DNS, etc.).

### 2. Fonctionnement du DHCP

Le processus DHCP fonctionne selon un cycle de 4 messages principaux :
1. **DHCP Discover** : Le client envoie une demande de configuration réseau (broadcast) pour rechercher un serveur DHCP disponible.
2. **DHCP Offer** : Le serveur DHCP répond en offrant une adresse IP et des informations de configuration réseau.
3. **DHCP Request** : Le client sélectionne une offre et envoie une requête au serveur pour confirmer qu'il souhaite utiliser l'adresse IP proposée.
4. **DHCP Acknowledgment (ACK)** : Le serveur confirme la configuration et le client peut commencer à utiliser l'adresse IP.

### 3. Paramètres attribués par DHCP
Un serveur DHCP peut fournir diverses informations au client :
- **Adresse IP** : Adresse unique attribuée au client.
- **Masque de sous-réseau** : Détermine le réseau auquel le client appartient.
- **Passerelle par défaut** : Routeur à utiliser pour accéder à des réseaux extérieurs.
- **Serveurs DNS** : Adresses des serveurs DNS à utiliser pour la résolution de noms de domaine.
- **Durée de bail** : Durée pendant laquelle le client peut utiliser l'adresse IP avant qu'elle ne doive être renouvelée.

### 4. Configuration d'un serveur DHCP

#### Exemple de fichier de configuration DHCP (`dhcpd.conf`) :
```
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option routers 192.168.1.1;
  option domain-name-servers 8.8.8.8, 8.8.4.4;
  option domain-name "mon-domaine.local";
  default-lease-time 600;
  max-lease-time 7200;
}
```

- **range** : Plage d'adresses IP à attribuer aux clients.
- **option routers** : Adresse de la passerelle par défaut.
- **option domain-name-servers** : Serveurs DNS utilisés par les clients.
- **default-lease-time** : Durée par défaut du bail (en secondes).
- **max-lease-time** : Durée maximale du bail (en secondes).

## Séance 4: Introduction au DNS
Le DNS (Domain Name System) est un service essentiel d'Internet qui permet de traduire des noms de domaine lisibles par l'homme (comme `www.example.com`) en adresses IP utilisables par les machines (comme `192.168.1.1`).

- **Résolution de noms** : Traduire un nom de domaine en adresse IP.
- **Structure hiérarchique** : Organiser les domaines en une hiérarchie (racine, TLD, domaines, sous-domaines).
- **Gestion décentralisée** : Répartir la gestion des noms de domaine à différents niveaux de la hiérarchie.

### 1. Types d'enregistrements DNS

- **A (Address)** : Associe un nom de domaine à une adresse IPv4.
- **AAAA (IPv6 Address)** : Associe un nom de domaine à une adresse IPv6.
- **CNAME (Canonical Name)** : Alias d'un autre nom de domaine (redirection vers un autre nom d'hôte).
- **MX (Mail Exchange)** : Spécifie les serveurs de messagerie pour la réception des e-mails.
- **NS (Name Server)** : Indique les serveurs DNS autoritaires pour un domaine.
- **PTR (Pointer)** : Utilisé pour la résolution inverse (traduction d'adresse IP en nom de domaine).
- **SOA (Start of Authority)** : Fournit des informations sur la zone DNS, y compris le serveur DNS principal.

### 2. Configuration d'un serveur DNS avec BIND

#### Exemple de fichier de configuration de zone (`db.example.com`) :
```
$TTL 86400
@   IN  SOA ns1.example.com. admin.example.com. (
        2023100201 ; Serial
        3600       ; Refresh
        1800       ; Retry
        1209600    ; Expire
        86400 )    ; Minimum TTL
@   IN  NS  ns1.example.com.
@   IN  A   192.168.1.1
www IN  A   192.168.1.1
mail IN  MX 10 mail.example.com.
mail IN  A   192.168.1.2
```

- **SOA** : Définit le serveur DNS principal et les paramètres de la zone.
- **NS** : Spécifie les serveurs de noms pour la zone.
- **A** : Associe un nom d'hôte à une adresse IP.
- **MX** : Définit les serveurs de messagerie pour le domaine.

#### Exemple de fichier `named.conf` pour BIND :
```
options {
    directory "/var/named";
    forwarders { 8.8.8.8; 8.8.4.4; };
    allow-query { any; };
};
zone "example.com" {
    type master;
    file "db.example.com";
};
```

- **directory** : Définit le répertoire où se trouvent les fichiers de zone.
- **forwarders** : Indique des serveurs DNS à interroger en cas de requête non résolue localement.
- **allow-query** : Définit qui peut interroger le serveur.
- **zone** : Définit les zones pour lesquelles le serveur est autoritaire.

### 3. Résolution DNS locale

Pour tester la résolution DNS en local (par exemple, après avoir configuré votre serveur DNS avec BIND), vous pouvez utiliser la commande `dig` ou `nslookup`.

#### Exemple d'utilisation de `dig` :
`dig @192.168.1.1 www.example.com`

- **@192.168.1.1** : Spécifie l'adresse IP du serveur DNS à interroger.
- **www.example.com** : Nom de domaine pour lequel on souhaite obtenir l'adresse IP.

#### Exemple d'utilisation de `nslookup` :
`nslookup www.example.com 192.168.1.1`

- **www.example.com** : Nom de domaine à résoudre.
- **192.168.1.1** : Adresse IP du serveur DNS à interroger.

## Séance 5 : Le Pare-feu (iptables)

Un pare-feu (firewall) est un dispositif de sécurité qui surveille le trafic réseau entrant et sortant et décide de l'autoriser ou de le bloquer en fonction d'un ensemble de règles de sécurité prédéfinies. Sous Linux, `iptables` est l'outil principal utilisé pour configurer un pare-feu. Il permet de définir des règles précises pour contrôler le trafic à travers différents points du réseau.

### Chaînes et tables dans iptables

Dans `iptables`, les **chaînes** sont des ensembles de règles qui décident du traitement des paquets. Il existe trois chaînes principales :
- **INPUT** : Gère les paquets entrants vers le serveur.
- **OUTPUT** : Gère les paquets sortants depuis le serveur.
- **FORWARD** : Gère les paquets traversant le serveur (lorsque le serveur agit comme un routeur).
- **PREROUTING** : Appliquée avant le routage des paquets.
- **POSTROUTING** : Appliquée après le routage des paquets.

Les **tables** sont des structures dans lesquelles les règles sont stockées et appliquées. Les tables les plus couramment utilisées sont :
- **filter** : Table par défaut pour le filtrage des paquets.
- **nat** : Utilisée pour la translation d'adresses réseau (NAT).
- **mangle** : Utilisée pour modifier les paquets.

### iptables

```bash
iptables [-t <nom-table>] <commande> <nom-chaîne> [-i <if-in>] [-o <if-out>] [-s <@IP-src>] [-d <@IP-dst>] [-p <protocole>] [<parametre> <option>]* -j <cible> [<parametre> <option>]
```

- `<nom-table>` est l'une des trois tables (filter, nat, mangle). filter par défaut.
- `<commande>` -A pour ajouter, -I pour insérer à un endroit précis dans la table, -D pour supprimer, -P pour définir la politique globale,
- `<nom-chaîne>` C'est INPUT, OUTPUT ou FORWARD...
- `<if-in>/<if-out>` est le nom de l'interface par laquelle le datagramme arrive à/sort de la machine
- `<@IP-src>/<@IP-dst>` est l'adresse IP de la source/du destinataire (peut être une adresse réseau, peut être en notation slashée précisant la taille du masque)
- `<protocole>` précise le protocole au dessus de IP (tcp, udp ou icmp) contenu dans le datagramme. Permet ensuite de préciser:
    - `<parametre>` paramètre supplémentaire souvent dépendant du protocole sélectionné. Par exemple avec -p tcp on accède aux paramètres --dport et --sport permettant de spécifier le numéro de port TCP destination ou source
    - `<option>` valeur du paramètre supplémentaire précise qu'on peut avoir plusieurs occurrences des paires <parametre> <option> pour ajouter plusieurs critères supplémentaires
- `<cible>` désigne ce qu'on fait avec le datagramme correspondant aux critères précédents (ACCEPT, DROP, REJECT, LOG...).
- la paire `<parametre> <option>` qui suit la cible apporte des précisions sur le comportement de la cible. Par exemple, --reject-with permet de choisir le message ICMP qui sera envoyé à l'émetteur en cas de rejet (pour les types possibles consulter le paragraphe sur le cible REJECT de la documentation)


### DMZ

Une DMZ (Demilitarized Zone) est un réseau périmétrique qui expose les services accessibles depuis l'extérieur (comme des serveurs web, mail, DNS) tout en protégeant le réseau interne. L'idée est d'ajouter une couche de sécurité en isolant ces serveurs publics du reste du réseau.