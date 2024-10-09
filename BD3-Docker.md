# Commandes utiles pour Docker, Symfony, et MariaDB

## Docker Compose

- **Démarrer les services Docker Compose :**
  `docker compose up`

- **Arrêter les services Docker Compose :**
  `docker compose down`

- **Exécuter une commande dans un conteneur spécifique :**
  `docker compose exec <service> <command>`
  - Par exemple entrer dans un conteneur: `docker compose sfapp bash`

- **Lister les services en cours d'exécution avec Docker Compose :**
  `docker compose ps`


## Commandes Symfony (dans le conteneur sfapp)

- **Mettre à jour les dépendances :**
  `composer update`

- **Créer une nouvelle entité :**
  `php bin/console make:entity`

- **Créer un nouveau contrôleur :**
  `php bin/console make:controller`

- **Créer une nouvelle migration :**
  `php bin/console make:migration`

- **Exécuter les migrations Doctrine :**
  `php bin/console doctrine:migration:migrate`


## Commandes MariaDB (dans le conteneur database)

- **Voir les logs de MariaDB :** `cat /var/log/mysql.log`

- **Se connecter à MariaDB avec un utilisateur spécifique :**
  `mariadb -u udbsfapp -p`

- **Entrer le mot de passe (exemple pour `pdbsfapp`) :**
  `pdbsfapp`

- **Afficher la liste des bases de données :**
  `mariadb> show databases;`

- **Utiliser une base de données spécifique :**
  `mariadb> use <database>;`

---