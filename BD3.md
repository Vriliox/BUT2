# Fiche de Révision : SQL dans un langage de programmation

## 1. Transactions et Accès Concurrents

### Définition de la Transaction
- Une transaction est une unité logique de traitement constituée d'une suite d'opérations sur une base de données qui doivent être validées (COMMIT) ou annulées (ROLLBACK) en bloc pour maintenir la cohérence.
- **Propriétés ACID** :
  - **Atomicité** : La transaction s'exécute complètement ou pas du tout.
  - **Cohérence** : La base de données reste cohérente avant et après la transaction.
  - **Isolation** : Les transactions concurrentes ne doivent pas interférer entre elles.
  - **Durabilité** : Les changements validés persistent même après une défaillance système.

### État Cohérent
- Une base est cohérente si toutes les contraintes d'intégrité sont respectées.
- Une transaction doit assurer la transition d'un état cohérent à un autre, même si des états intermédiaires peuvent être incohérents temporairement.

### Gestion des Transactions
- **Début de la transaction** : Implicite dans la plupart des systèmes, généralement au moment de la première instruction SQL.
- **Fin de la transaction** : Par un **COMMIT** ou un **ROLLBACK**.

### Accès Concurrent et Problèmes Associés
- **Transactions Concurrentes** : Plusieurs transactions accèdent simultanément aux mêmes données.
- **Anomalies courantes** :
  - **Perte de mise à jour** : Une transaction écrase les modifications d'une autre.
  - **Lecture impropre** : Une transaction lit des données modifiées non validées par une autre.
  - **Lecture non reproductible** : Une transaction lit des valeurs différentes à chaque accès à cause des modifications par d'autres transactions.

### Niveaux d'Isolation
- **READ UNCOMMITTED** : Permet la lecture des données non validées (lecture sale).
- **READ COMMITTED** : Ne permet que la lecture des données validées.
- **REPEATABLE READ** : Empêche la lecture non reproductible, mais les « tuples fantômes » peuvent apparaître.
- **SERIALIZABLE** : Assure une exécution comme si les transactions étaient séquentielles, évitant toutes les anomalies.

### Mécanismes de Verrouillage dans Oracle
- **Verrouillage implicite** pour les opérations de mise à jour : DELETE, UPDATE, INSERT.
- **Verrouillage explicite** pour une gestion plus fine des accès :
  - **LOCK TABLE ... IN EXCLUSIVE MODE** : Verrouille la table pour empêcher toute modification par d'autres.
  - **SELECT ... FOR UPDATE** : Verrouille les lignes sélectionnées pour modification future.

### Exemples de Commandes
```sql
-- Début implicite d'une transaction
UPDATE compte SET solde = solde - 500 WHERE num_compte = 1;

-- Verrouillage pour modification
SELECT solde FROM compte WHERE num_compte = 1 FOR UPDATE;

-- Validation
COMMIT;

-- Annulation
ROLLBACK;
```

### Synthèse des Verrous
Modes de verrouillage : ROW SHARE, ROW EXCLUSIVE, SHARE, SHARE ROW EXCLUSIVE, EXCLUSIVE.  
Chaque mode détermine les opérations autorisées et les verrous compatibles.

## 2. Déclencheurs (Triggers)

### Définition
- Un **déclencheur (trigger)** est un ensemble d'actions exécutées automatiquement par le SGBD lorsqu'un événement spécifique se produit. Il s'agit d'une procédure stockée qui peut être associée à une table, une vue, ou même à des événements au niveau de la base de données.
- Les triggers permettent de gérer la **cohérence** et de faciliter la **maintenance** en implémentant des règles complexes directement au niveau de la base de données.

### Types de Triggers
- **Statement Trigger** : S'exécute une seule fois, peu importe le nombre de lignes affectées par l'événement déclenchant.
- **Row Trigger** : S'exécute pour chaque ligne affectée par l'événement déclenchant.

### Synchronisation des Triggers
- **BEFORE** : S'exécute avant l'opération DML (Data Manipulation Language).
- **AFTER** : S'exécute après l'opération DML.
- **INSTEAD OF** : Utilisé pour les vues, s'exécute à la place de l'opération DML.

### Événements Déclencheurs
- **Ordres DML** : `INSERT`, `UPDATE`, `DELETE`.
- **Ordres DDL** : `CREATE`, `ALTER`, `DROP`.
- **Événements systèmes** : Démarrage ou arrêt de la base, erreurs système.
- **Événements utilisateur** : Connexion/déconnexion.

### Exemple de Création de Trigger
```sql
CREATE OR REPLACE TRIGGER audit_emp_changes
AFTER INSERT OR UPDATE OR DELETE ON emp
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_name, change_date, operation, old_salary, new_salary)
    VALUES (USER, SYSDATE, 'CHANGE', :OLD.sal, :NEW.sal);
END;
/
```

### Utilisation des Qualificatifs OLD et NEW

- **OLD** : Valeur de la colonne avant la modification (non applicable pour INSERT).
- **NEW**: Valeur de la colonne après la modification (non applicable pour DELETE).

### Gestion et Maintenance
- **Activation/Désactivation** : `ALTER TRIGGER nom_trigger ENABLE | DISABLE`.
- **Suppression** : `DROP TRIGGER nom_trigger`.
- Les triggers peuvent être testés pour s'assurer qu'ils fonctionnent comme prévu et qu'ils n'interfèrent pas avec d'autres triggers.

## 3. ORM et Framework Doctrine

### 1. Introduction à l'ORM
- **ORM (Object-Relational Mapping)** : Technique de programmation permettant de convertir des données entre des systèmes incompatibles (objets dans la programmation orientée objet et bases de données relationnelles).
- Avantages :
  - Simplifie les interactions avec la base de données.
  - Permet de manipuler des objets au lieu de requêtes SQL brutes.
  - Centralise la logique métier et l'accès aux données.
- Inconvénients :
  - Peut ajouter une surcharge et des limitations par rapport à l'utilisation de SQL natif.
  - Courbe d'apprentissage pour la configuration et l'utilisation avancée.

### 2. ORM : Cas de Doctrine
- **Doctrine** : Un des ORM les plus populaires dans l'écosystème PHP, souvent utilisé avec Symfony.
- Fonctionnalités principales :
  - Permet de mapper des classes PHP aux tables de la base de données.
  - Gère la persistance des objets en les transformant automatiquement en enregistrements de base de données.
  - Propose des outils de migration pour gérer les changements de schéma de la base.

### 3. Doctrine : Les Entités
- **Entité** : Une classe PHP représentant une table dans la base de données.
- Exemple d'entité :
```php
/**
 * @Entity
 * @Table(name="users")
 */
class User {
    /** @Id @GeneratedValue @Column(type="integer") */
    private $id;

    /** @Column(type="string", length=100) */
    private $name;

    // Getters et setters...
}
```

### 4. Doctrine : Mapping Fondamental
- **Mapping** : Association entre les propriétés de classe et les colonnes de la base de données.
- Types de mappings :
  - Annotations (directement dans la classe).
  - Fichiers YAML ou XML.
- Exemple de mapping via annotations :
```php
/** @Column(type="date") */
private $birthDate;
```

### 5. Doctrine : Gestion des Associations entre Classes
- Types d'associations :
  - **OneToOne** : Relation un-à-un.
  - **OneToMany** : Relation un-à-plusieurs.
  - **ManyToOne** : Relation plusieurs-à-un.
  - **ManyToMany** : Relation plusieurs-à-plusieurs.
- Exemple :
```php
/** @OneToMany(targetEntity="Post", mappedBy="user") */
private $posts;
```

### 6. Langage de Requête de Doctrine : DQL
- **DQL (Doctrine Query Language)** : Langage de requête orienté objet, similaire à SQL, utilisé pour interroger les entités.
- Exemple de requête DQL :
```php
$query = $entityManager->createQuery('SELECT u FROM User u WHERE u.name = :name');
$query->setParameter('name', 'Alice');
```

### 7. Générateur de Requête
- Doctrine offre des méthodes pour créer des requêtes dynamiques avec le **QueryBuilder**.
- Exemple d'utilisation du QueryBuilder :
```php
$qb = $entityManager->createQueryBuilder();
$qb->select('u')
   ->from('User', 'u')
   ->where('u.age > :age')
   ->setParameter('age', 18);
```

### 8. SQL Natif
- Doctrine permet également l'exécution de requêtes SQL brutes pour des besoins spécifiques.
- Exemple :
```php
$connection = $entityManager->getConnection();
$sql = 'SELECT * FROM users WHERE status = :status';
$stmt = $connection->prepare($sql);
$stmt->execute(['status' => 'active']);
```

## 4. Index et Optimisation

### 1. Introduction aux Index
- **Index** : Structure définie sur une ou plusieurs colonnes d'une table pour permettre un accès rapide aux lignes lors des requêtes basées sur la clé d'index.
- **Types d'index** : Uniques, non uniques, composés, partitionnés, B-tree, bitmap, et à clé inversée.
- **Caractéristiques** :
  - Logiquement et physiquement indépendants des tables.
  - Actualisés automatiquement à chaque opération DML (INSERT, UPDATE, DELETE).

### 2. Types d'Index
- **Index B-Tree** : Le plus courant, structure hiérarchique avec racine, blocs de branche et noeuds de feuille.
- **Index Bitmap** : Utilisé pour les colonnes avec faible cardinalité, particulièrement utile pour les requêtes avec des conditions OR.
- **Index à Clé Inversée** : Utilisé pour éviter les goulets d'étranglement d'E/S lors des insertions ordonnées par valeurs croissantes de la clé.

### 3. Directives pour la Création des Index
- **Bonnes pratiques** :
  - Indexer les colonnes fréquemment utilisées dans les clauses WHERE.
  - Ne pas indexer des petites tables ou des colonnes avec peu de valeurs distinctes.
  - Créer des index composés si plusieurs colonnes sont souvent utilisées ensemble.
- **Sélectivité** : L'efficacité d'un index dépend de sa sélectivité, soit le ratio entre le nombre moyen de lignes retournées et le total de lignes.

### 4. Gestion des Index
- **Création** :
  `sql
  CREATE INDEX nom_index ON table(colonne) TABLESPACE nom_tablespace;
  `
- **Reconstruction** :
  `sql
  ALTER INDEX nom_index REBUILD TABLESPACE nouveau_tablespace;
  `
- **Suppression** :
  `sql
  DROP INDEX nom_index;
  `

### 5. Plan d'Exécution et Optimisation
- **Plan d'exécution** : Séquence d'étapes choisies par l'optimiseur pour exécuter une requête SQL de manière efficace.
- **EXPLAIN PLAN** : Commande SQL permettant d'afficher le plan d'exécution d'une requête.
  `sql
  EXPLAIN PLAN FOR SELECT * FROM emp WHERE deptno = 10;
  SELECT * FROM table(DBMS_XPLAN.DISPLAY);
  `
- **SET AUTOTRACE** : Utilisée dans SQL*Plus pour afficher le plan d'exécution et les statistiques.
  `sql
  SET AUTOTRACE ON;
  `

### 6. Situations de Non-Utilisation des Index
- **Requêtes avec valeurs NULL** : Les index ne prennent pas en compte les valeurs NULL.
- **Expressions complexes** : Les fonctions appliquées aux colonnes ou les clauses de type `LIKE '%texte'` empêchent l'utilisation de l'index.