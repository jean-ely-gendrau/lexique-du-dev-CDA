# Commandes SQL Essentielles

## Table des matières
- [SHOW DATABASES](#showdatabases)
- [CREATE USER](#createuser)
- [CREATE TABLE](#createtable)
- [INSERT INTO](#insertinto)
- [SELECT](#select)
- [WHERE](#where)
- [JOIN](#join)
- [UPDATE](#update)
- [DELETE](#delete)
- [ALTER TABLE](#altertable)
- [GROUP BY](#groupby)
- [HAVING](#having)
- [ORDER BY](#orderby)
- [LIMIT](#limit)
- [UNION](#union)

---

### 0. `SHOW DATABASES` <a name="showdatabases"></a>
- **Description** : Affiche la liste des bases de données disponibles sur le serveur MySQL.
- **Exemple** :
```sql
SHOW DATABASES;
```

### 1. `CREATE USER` <a name="createuser"></a>
- **Description** : Crée un nouvel utilisateur pour accéder à la base de données.
- **Exemple** :
```sql
CREATE USER 'lecteur'@'localhost' IDENTIFIED BY 'lecteur';
```

- **Vérifier** : L'ajout de l'utilisateur à la table `user`.
```sql
USE mysql;

SELECT User, Host FROM user WHERE User = 'lecteur';
```

- **Droits Utilisateur** : Donne les droits d'accès à une base de données spécifique.
```sql
GRANT SELECT
ON bibliotheque.*
TO 'lecteur'@'localhost';
```

- **FLUSH PRIVILEGES** : Rafraîchit les privilèges pour que les changements prennent effet.
```sql
FLUSH PRIVILEGES;
```

### 2. `CREATE TABLE` <a name="createtable"></a>
- **Description** : Crée une nouvelle table dans la base de données.
- **Tip** : Spécifie les colonnes et leurs types de données lors de la création de la table.
- **Exemple** :
```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);
```

### 3. `INSERT INTO` <a name="insertinto"></a>
- **Description** : Insère de nouvelles lignes de données dans une table.
- **Tip** : Les valeurs doivent correspondre aux colonnes définies dans la table.
- **Exemple** :
```sql
INSERT INTO users (id, name, email)
VALUES (1, 'John Doe', 'john.doe@example.com');
```

### 4. `SELECT` <a name="select"></a>
- **Description** : Récupère des données d'une ou plusieurs tables.
- **Info** : Utilisé avec des clauses comme `WHERE`, `JOIN`, et `ORDER BY` pour filtrer ou organiser les résultats.
- **Exemple** :
```sql
SELECT name, email FROM users;
```

### 5. `WHERE` <a name="where"></a>
- **Description** : Filtre les lignes dans une requête SQL selon une condition spécifique.
- **Tip** : Peut utiliser des opérateurs comme `=`, `>`, `<`, `LIKE`, `IN`, etc.
- **Exemple** :
```sql
SELECT * FROM users
WHERE id = 1;
```

### 6. `JOIN` <a name="join"></a>
- **Description** : Combine des lignes de plusieurs tables basées sur une condition commune entre elles.
- **Types** : Les types courants incluent `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN` et `FULL JOIN`.
- **Exemple** :
```sql
SELECT users.name, orders.order_date
FROM users
INNER JOIN orders ON users.id = orders.user_id;
```

### 7. `UPDATE` <a name="update"></a>
- **Description** : Modifie les valeurs des colonnes d'une ou plusieurs lignes dans une table.
- **Warning** : Assure-toi d'utiliser `WHERE` pour éviter de mettre à jour toutes les lignes !
- **Exemple** :
```sql
UPDATE users
SET email = 'new.email@example.com'
WHERE id = 1;
```

### 8. `DELETE` <a name="delete"></a>
- **Description** : Supprime des lignes d'une table.
- **Warning** : Sans `WHERE`, toutes les lignes de la table seront supprimées.
- **Exemple** :
```sql
DELETE FROM users
WHERE id = 1;
```

### 9. `ALTER TABLE` <a name="altertable"></a>
- **Description** : Modifie la structure d'une table existante (ajout de colonnes, modification de types, etc.).
- **Tip** : Peut être utilisé pour ajouter des contraintes ou des index.
- **Exemple** :
```sql
ALTER TABLE users
ADD phone_number VARCHAR(20);
```

### 10. `GROUP BY` <a name="groupby"></a>
- **Description** : Regroupe les lignes ayant des valeurs identiques dans certaines colonnes et permet d'appliquer des fonctions d'agrégation (`COUNT`, `SUM`, `AVG`, etc.).
- **Exemple** :
```sql
SELECT country, COUNT(*)
FROM users
GROUP BY country;
```

### 11. `HAVING` <a name="having"></a>
- **Description** : Filtre les résultats après l'application de `GROUP BY`, souvent utilisé avec des fonctions d'agrégation.
- **Exemple** :
```sql
SELECT country, COUNT(*)
FROM users
GROUP BY country
HAVING COUNT(*) > 10;
```

### 12. `ORDER BY` <a name="orderby"></a>
- **Description** : Trie les résultats d'une requête dans un ordre spécifique (croissant ou décroissant).
- **Tip** : Par défaut, l'ordre est croissant (`ASC`). Utilise `DESC` pour l'ordre décroissant.
- **Exemple** :
```sql
SELECT * FROM users
ORDER BY name ASC;
```

### 13. `LIMIT` <a name="limit"></a>
- **Description** : Restreint le nombre de résultats renvoyés par une requête.
- **Tip** : Utile pour paginer les résultats.
- **Exemple** :
```sql
SELECT * FROM users
LIMIT 10;
```

### 14. `UNION` <a name="union"></a>
- **Description** : Combine les résultats de deux ou plusieurs requêtes `SELECT` en supprimant les doublons.
- **Exemple** :
```sql
SELECT name FROM users
UNION
SELECT name FROM admins;
```
