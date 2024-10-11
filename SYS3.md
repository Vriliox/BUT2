# SYS3 - Les appels systèmes

## Gestion des Fichiers

## 1. `open`

- **Prototype**: `int open(const char *pathname, int flags[, mode_t mode]);`
- **Paramètres**:
  - `pathname`: Chemin du fichier à ouvrir.
  - `flags`: Indique le mode d'ouverture (`O_RDONLY`, `O_WRONLY`, `O_RDWR`, `O_CREAT`).
  - `mode`: Permissions si `O_CREAT` est utilisé (ex: `S_IRUSR | S_IWUSR`).
- **Valeur de retour**: Un descripteur de fichier (> 0) en cas de succès, `-1` en cas d'erreur.
- **Exemple**:

  ```c
  int fd = open('file.txt', O_RDONLY | O_CREAT, S_IRUSR | S_IWUSR);
  ```

> [!NOTE]
> Modes d'ouverture (flag):
>
> - `O_RDONLY` : Lecture seule.
> - `O_WRONLY` : Écriture seule.
> - `O_RDWR` : Lecture et écriture.
> - `O_CREAT` : Crée un fichier s'il n'existe pas.
> - `O_EXCL` : Échoue si le fichier existe déjà (avec O_CREAT).
> - `O_TRUNC` : Tronque le fichier.
> - `O_APPEND` : Écriture à la fin du fichier.  
>
> Permissions (mode) :
>
> - `S_IRUSR`: Lecture pour le propriétaire.
> - `S_IWUSR` : Écriture pour le propriétaire.
> - `S_IRGRP`, `S_IROTH`, etc. : Permissions pour groupe/les autres.

## 2. `close`

- **Prototype**: `int close(int fd);`
- **Paramètres**:
  - `fd`: Le descripteur de fichier à fermer.
- **Valeur de retour**: `0` en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `if (close(fd) == -1) perror('close');`

## 3. `read`

- **Prototype**: `ssize_t read(int fd, void *buf, size_t count);`
- **Paramètres**:
  - `fd`: Le descripteur de fichier à lire.
  - `buf`: Le buffer où stocker les données.
  - `count`: Nombre d'octets à lire.
- **Valeur de retour**: Nombre d'octets lus, `0` si fin de fichier, `-1` en cas d'erreur.
- **Exemple**:
  `ssize_t bytes = read(fd, buffer, sizeof(buffer));`

## 4. `write`

- **Prototype**: `ssize_t write(int fd, const void *buf, size_t count);`
- **Paramètres**:
  - `fd`: Le descripteur de fichier où écrire.
  - `buf`: Les données à écrire.
  - `count`: Nombre d'octets à écrire.
- **Valeur de retour**: Nombre d'octets écrits, `-1` en cas d'erreur.
- **Exemple**:
  `ssize_t written = write(fd, 'Hello', 5);`

## 5. `dup`

- **Prototype**: `int dup(int oldfd);`
- **Paramètres**:
  - `oldfd`: Le descripteur de fichier à dupliquer.
- **Valeur de retour**: Nouveau descripteur de fichier, `-1` en cas d'erreur.
- **Exemple**:
  `int newfd = dup(oldfd);`

## 6. `dup2`

- **Prototype**: `int dup2(int oldfd, int newfd);`
- **Paramètres**:
  - `oldfd`: Le descripteur à dupliquer.
  - `newfd`: Nouveau descripteur où copier `oldfd`. Si `newfd` est déjà ouvert, il est fermé.
- **Valeur de retour**: `newfd` en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `dup2(fd, STDOUT_FILENO);`

---

## Gestion des Processus

## 7. `fork`

- **Prototype**: `pid_t fork(void);`
- **Paramètres**: Aucun.
- **Valeur de retour**:
  - `0` pour le processus enfant.
  - PID du processus enfant pour le processus parent.
  - `-1` en cas d'erreur.
- **Exemple**:
  `pid_t pid = fork();`

## 8. `pipe`

- **Prototype**: `int pipe(int pipefd[2]);`
- **Paramètres**:
  - `pipefd`: Tableau de deux entiers (`pipefd[0]` pour la lecture, `pipefd[1]` pour l'écriture).
- **Valeur de retour**: `0` en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `pipe(pipefd);`

## 9. `execlp`

- **Prototype**: `int execlp(const char *file, const char *arg, ...);`
- **Paramètres**:
  - `file`: Nom du programme à exécuter.
  - `arg...`: Liste d'arguments terminée par `NULL`.
- **Valeur de retour**: Ne retourne pas en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `execlp('ls', 'ls', '-l', NULL);`

## 10. `execve`

- **Prototype**: `int execve(const char *pathname, char *const argv[], char *const envp[]);`
- **Paramètres**:
  - `pathname`: Chemin du programme à exécuter.
  - `argv[]`: Tableau d'arguments.
  - `envp[]`: Tableau de variables d'environnement.
- **Valeur de retour**: Ne retourne pas en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `execve('/bin/ls', argv, envp);`

## 11. `exit`

- **Prototype**: `void exit(int status);`
- **Paramètres**:
  - `status`: Code de retour à transmettre au processus parent.
- **Valeur de retour**: Ne retourne pas (termine le processus).
- **Exemple**:
  `exit(0);`

## 12. `system`

- **Prototype**: `int system(const char *command);`
- **Paramètres**:
  - `command`: Chaîne de caractères contenant la commande à exécuter.
- **Valeur de retour**: Code de statut renvoyé par le shell, `-1` en cas d'erreur.
- **Exemple**:
  `system('ls -l');`

## Gestion des sockets

## **TCP (Transmission Control Protocol)**

### **Serveur TCP**

1. **Création de la socket** (`socket()`): Le serveur crée une socket en spécifiant le domaine (`AF_INET` pour IPv4), le type de socket (`SOCK_STREAM` pour TCP) et le protocole.
2. **Attachement à une adresse** (`bind()`): Le serveur associe la socket à une adresse IP et un port spécifiques.
3. **Écoute des connexions** (`listen()`): La socket est mise en mode écoute pour les connexions entrantes.
4. **Acceptation d'une connexion** (`accept()`): Une fois qu'un client tente de se connecter, le serveur accepte la connexion et obtient un nouveau descripteur de socket pour communiquer avec ce client.
5. **Échange de données** (`send()` / `recv()` ou `write()` / `read()`): Le serveur et le client échangent des données via la nouvelle connexion.
6. **Fermeture de la connexion** (`close()`): Une fois la communication terminée, la connexion est fermée.

### **Client TCP**

1. **Création de la socket** (`socket()`): Le client crée une socket de type `SOCK_STREAM` pour TCP.
2. **Connexion au serveur** (`connect()`): Le client tente de se connecter à l'adresse IP et au port du serveur.
3. **Échange de données** (`send()` / `recv()` ou `write()` / `read()`): Une fois connecté, le client échange des données avec le serveur.
4. **Fermeture de la connexion** (`close()`): Après l'échange, le client ferme la connexion.

### **Résumé des étapes TCP**

- **Serveur** : `socket()` → `bind()` → `listen()` → `accept()` → `send()/recv()` → `close()`
- **Client** : `socket()` → `connect()` → `send()/recv()` → `close()`

## **UDP (User Datagram Protocol)**

### **Serveur UDP**

1. **Création de la socket** (`socket()`): Le serveur crée une socket en spécifiant le domaine (`AF_INET` pour IPv4) et le type de socket (`SOCK_DGRAM` pour UDP).
2. **Attachement à une adresse** (`bind()`): Le serveur associe la socket à une adresse IP et à un port spécifiques.
3. **Réception de données** (`recvfrom()`): Le serveur attend la réception de datagrammes de n'importe quel client.
4. **Envoi de réponse** (`sendto()`): Après avoir reçu des données, le serveur peut répondre au client.
5. **Fermeture de la socket** (`close()`): La socket est fermée une fois que le serveur n'a plus besoin de recevoir ou d'envoyer de données.

### **Client UDP**

1. **Création de la socket** (`socket()`): Le client crée une socket de type `SOCK_DGRAM` pour UDP.
2. **Envoi de données** (`sendto()`): Le client envoie un datagramme à l'adresse IP et au port du serveur.
3. **Réception de la réponse** (`recvfrom()`): Le client peut recevoir une réponse du serveur (si besoin).
4. **Fermeture de la socket** (`close()`): Une fois l'échange terminé, la socket est fermée.

### **Résumé des étapes UDP**

- **Serveur** : `socket()` → `bind()` → `recvfrom()` → `sendto()` → `close()`
- **Client** : `socket()` → `sendto()` → `recvfrom()` → `close()`

---

## 1. `socket`

- **Prototype**: `int socket(int domain, int type, int protocol);`
- **Paramètres**:
  - `domain`: Domaine d'adresse (ex: `AF_INET` pour IPv4).
  - `type`: Type de socket (`SOCK_STREAM` pour TCP, `SOCK_DGRAM` pour UDP).
  - `protocol`: Protocole utilisé (généralement `0` pour automatique).
- **Valeur de retour**: Un descripteur de socket en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `int sockfd = socket(AF_INET, SOCK_STREAM, 0);`

> [!NOTE]
> Domaine d'adresse:  
>
> - `AF_INET` pour IPv4
> - `AF_INET6` pour iPv6  
>
> Type de socket:  
>
> - `SOCK_STREAM` pour TCP.
> - `SOCK_DGRAM` pour UDP.

## 2. `bind`

- **Prototype**: `int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);`
- **Paramètres**:
  - `sockfd`: Descripteur de socket.
  - `addr`: Structure `sockaddr` contenant l'adresse à attacher.
  - `addrlen`: Taille de la structure `sockaddr`.
- **Valeur de retour**: `0` en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `bind(sockfd, (struct sockaddr *)&addr, sizeof(addr));`

## 3. `listen` (TCP uniquement)

- **Prototype**: `int listen(int sockfd, int backlog);`
- **Paramètres**:
  - `sockfd`: Descripteur de socket.
  - `backlog`: Nombre maximum de connexions en attente.
- **Valeur de retour**: `0` en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `listen(sockfd, 5);`

## 4. `connect`

- **Prototype**: `int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen);`
- **Paramètres**:
  - `sockfd`: Descripteur de socket.
  - `addr`: Structure `sockaddr` du serveur à contacter.
  - `addrlen`: Taille de la structure `sockaddr`.
- **Valeur de retour**: `0` en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `connect(sockfd, (struct sockaddr *)&server_addr, sizeof(server_addr));`

## 5. `accept`

- **Prototype**: `int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);`
- **Paramètres**:
  - `sockfd`: Descripteur de socket.
  - `addr`: Pointeur vers une structure `sockaddr` qui recevra l'adresse du client.
  - `addrlen`: Taille de la structure `sockaddr`.
- **Valeur de retour**: Un nouveau descripteur de socket en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `int new_sock = accept(sockfd, (struct sockaddr *)&client_addr, &addrlen);`

## 6. `send`

- **Prototype**: `ssize_t send(int sockfd, const void *buf, size_t len, int flags);`
- **Paramètres**:
  - `sockfd`: Descripteur de socket.
  - `buf`: Buffer des données à envoyer.
  - `len`: Taille des données à envoyer.
  - `flags`: Options (généralement `0`).
- **Valeur de retour**: Nombre d'octets envoyés, `-1` en cas d'erreur.
- **Exemple**:
  `send(sockfd, "Hello", 5, 0);`

## 7. `recv`

- **Prototype**: `ssize_t recv(int sockfd, void *buf, size_t len, int flags);`
- **Paramètres**:
  - `sockfd`: Descripteur de socket.
  - `buf`: Buffer où stocker les données reçues.
  - `len`: Taille maximale des données à lire.
  - `flags`: Options (généralement `0`).
- **Valeur de retour**: Nombre d'octets reçus, `-1` en cas d'erreur.
- **Exemple**:
  `recv(sockfd, buffer, sizeof(buffer), 0);`

## 8. `write`

- **Prototype**: `ssize_t write(int fd, const void *buf, size_t count);`
- **Paramètres**:
  - `fd`: Descripteur de fichier (socket).
  - `buf`: Données à écrire.
  - `count`: Nombre d'octets à écrire.
- **Valeur de retour**: Nombre d'octets écrits, `-1` en cas d'erreur.
- **Exemple**:
  `write(sockfd, "data", 4);`

## 9. `read`

- **Prototype**: `ssize_t read(int fd, void *buf, size_t count);`
- **Paramètres**:
  - `fd`: Descripteur de fichier (socket).
  - `buf`: Buffer où stocker les données lues.
  - `count`: Nombre d'octets à lire.
- **Valeur de retour**: Nombre d'octets lus, `-1` en cas d'erreur.
- **Exemple**:
  `read(sockfd, buffer, sizeof(buffer));`

## 10. `sendto`

- **Prototype**: `ssize_t sendto(int sockfd, const void *buf, size_t len, int flags, const struct sockaddr *dest_addr, socklen_t addrlen);`
- **Paramètres**:
  - `sockfd`: Descripteur de socket.
  - `buf`: Données à envoyer.
  - `len`: Taille des données.
  - `flags`: Options (généralement `0`).
  - `dest_addr`: Adresse du destinataire.
  - `addrlen`: Taille de l'adresse.
- **Valeur de retour**: Nombre d'octets envoyés, `-1` en cas d'erreur.
- **Exemple**:
  `sendto(sockfd, "Hello", 5, 0, (struct sockaddr *)&dest_addr, sizeof(dest_addr));`

## 11. `recvfrom`

- **Prototype**: `ssize_t recvfrom(int sockfd, void *buf, size_t len, int flags, struct sockaddr *src_addr, socklen_t *addrlen);`
- **Paramètres**:
  - `sockfd`: Descripteur de socket.
  - `buf`: Buffer pour stocker les données reçues.
  - `len`: Taille maximale des données à lire.
  - `flags`: Options (généralement `0`).
  - `src_addr`: Adresse source du paquet reçu.
  - `addrlen`: Taille de l'adresse.
- **Valeur de retour**: Nombre d'octets reçus, `-1` en cas d'erreur.
- **Exemple**:
  `recvfrom(sockfd, buffer, sizeof(buffer), 0, (struct sockaddr *)&src_addr, &addrlen);`

## 12. `close`

- **Prototype**: `int close(int fd);`
- **Paramètres**:
  - `fd`: Descripteur de socket.
- **Valeur de retour**: `0` en cas de succès, `-1` en cas d'erreur.
- **Exemple**:
  `close(sockfd);`

## 13. `gethostbyname`

- **Prototype**: `struct hostent *gethostbyname(const char *name);`
- **Paramètres**:
  - `name`: Nom de l'hôte (ex: `www.example.com`).
- **Valeur de retour**: Pointeur vers une structure `hostent` contenant l'adresse IP, `NULL` en cas d'erreur.
- **Exemple**:
  `struct hostent *host = gethostbyname("example.com");`

## 14. `gethostbyaddr`

- **Prototype**: `struct hostent *gethostbyaddr(const void *addr, socklen_t len, int type);`
- **Paramètres**:
  - `addr`: Adresse IP.
  - `len`: Taille de l'adresse.
  - `type`: Type d'adresse (ex: `AF_INET` pour IPv4).
- **Valeur de retour**: Pointeur vers une structure `hostent`, `NULL` en cas d'erreur.
- **Exemple**:
  `struct hostent *host = gethostbyaddr(&ip_addr, sizeof(ip_addr), AF_INET);`

> [!WARNING]
> Attention code chiant pour gérer les adresses.  
> Pour créer une struct sockaddr_in côté client avec le port et l'adresse du serveur:
>
> ```c
> struct  sockaddr_in serveur; // Création de la struct
> serveur.sin_family = AF_INET; // Utilisons le protocole Internet
> serveur.sin_port = htons(sport); // Définir le port et convertit l'entier court non signé hostshort de l'ordre des octets de l'hôte en ordre des octets du réseau.
> inet_aton(address,&serveur.sin_addr); // Convertit l'adresse à partir de la notation IPv4 (x.x.x.x) sous forme binaire (dans l'ordre des octets du réseau) et la stocke dans la structure vers laquelle pointe le 2nd paramètre.
> ```
>
> Pour créer une struct sockaddr_in côté serveur avec le port souhaité:
>
> ```c
> struct  sockaddr_in serveur; // Création de la struct
> serveur.sin_family = AF_INET; // Utilisons le protocole Internet
> serveur.sin_port = htons(sport); // Définir le port et convertit l'entier court non signé hostshort de l'ordre des octets de l'hôte en ordre des octets du réseau.
> serveur.sin_addr.s_addr = INADDR_ANY; // Attribution de n'importe quel adresse IP (la sienne).
> ```
