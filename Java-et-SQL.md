# Lexique Java et SQL

## Table des matières
- [JDBC](#jdbc)
- [Connection](#connection)
- [Statement](#statement)
- [PreparedStatement](#preparedstatement)
- [ResultSet](#resultset)
- [DriverManager](#drivermanager)
- [SQLException](#sqlexception)
- [commit()](#commit)
- [rollback()](#rollback)
- [AutoCommit](#autocommit)
- [DataSource](#datasource)
- [Hibernate](#hibernate)

---

### 1. `JDBC` <a name="jdbc"></a>
- **Description** : Java Database Connectivity, une API standard pour se connecter et interagir avec une base de données dans Java.
- **Tip** : Utilisé pour exécuter des requêtes SQL, récupérer des résultats et gérer des transactions.
- **Exemple** :
```JAVA
import java.sql.*;

public class JDBCExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydb";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM Users");

            while (rs.next()) {
                System.out.println(rs.getString("name"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 2. `Connection` <a name="connection"></a>
- **Description** : Interface représentant une connexion ouverte à une base de données.
- **Tip** : Utilisée pour créer des `Statement`, `PreparedStatement`, et gérer les transactions.
- **Exemple** :
```JAVA
Connection conn = DriverManager.getConnection(dbUrl, user, password);
```

### 3. `Statement` <a name="statement"></a>
- **Description** : Interface utilisée pour exécuter des requêtes SQL statiques (sans paramètres).
- **Warning** : Vulnérable aux injections SQL, utiliser `PreparedStatement` pour plus de sécurité.
- **Exemple** :
```JAVA
Statement stmt = conn.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM Users");
```

### 4. `PreparedStatement` <a name="preparedstatement"></a>
- **Description** : Interface utilisée pour exécuter des requêtes SQL paramétrées, plus sécurisée que `Statement`.
- **Tip** : Protège contre les injections SQL en précompilant la requête.
- **Exemple** :
```JAVA
PreparedStatement pstmt = conn.prepareStatement("SELECT * FROM Users WHERE id = ?");
pstmt.setInt(1, 10);
ResultSet rs = pstmt.executeQuery();
```

### 5. `ResultSet` <a name="resultset"></a>
- **Description** : Interface représentant les données résultant d'une requête SQL. Utilisé pour lire les résultats ligne par ligne.
- **Tip** : Utilise des méthodes comme `getString()`, `getInt()`, etc. pour accéder aux colonnes de la table.
- **Exemple** :
```JAVA
while (rs.next()) {
    System.out.println(rs.getString("name"));
}
```

### 6. `DriverManager` <a name="drivermanager"></a>
- **Description** : Gestionnaire de pilotes pour établir des connexions à des bases de données.
- **Tip** : Utilisé pour obtenir une connexion via `getConnection()`.
- **Exemple** :
```JAVA
Connection conn = DriverManager.getConnection(url, user, password);
```

### 7. `SQLException` <a name="sqlexception"></a>
- **Description** : Exception levée lorsque des erreurs SQL surviennent lors de l'exécution de requêtes ou de transactions.
- **Tip** : Toujours gérer cette exception lors des opérations JDBC.
- **Exemple** :
```JAVA
try {
    // Code de base de données ici
} catch (SQLException e) {
    e.printStackTrace();
}
```

### 8. `commit()` <a name="commit"></a>
- **Description** : Valide une transaction manuellement dans une connexion SQL.
- **Info** : Utilisé pour appliquer les modifications apportées par une série d'opérations SQL.
- **Exemple** :
```JAVA
conn.commit();
```

### 9. `rollback()` <a name="rollback"></a>
- **Description** : Annule une transaction en cours en cas d'erreur.
- **Tip** : À utiliser dans un bloc `catch` en cas d'échec pour éviter de valider une transaction partielle.
- **Exemple** :
```JAVA
conn.rollback();
```

### 10. `AutoCommit` <a name="autocommit"></a>
- **Description** : Détermine si chaque instruction SQL est validée automatiquement ou non.
- **Tip** : Lorsqu'il est désactivé (`setAutoCommit(false)`), les transactions doivent être validées manuellement avec `commit()`.
- **Exemple** :
```JAVA
conn.setAutoCommit(false); // Désactiver l'auto-commit
conn.commit(); // Valider manuellement
```

### 11. `DataSource` <a name="datasource"></a>
- **Description** : Interface utilisée pour représenter une source de connexions de base de données, souvent utilisée dans les applications d'entreprise pour la gestion des pools de connexions.
- **Exemple** :
```JAVA
DataSource dataSource = new MysqlDataSource();
Connection conn = dataSource.getConnection();
```

### 12. `Hibernate` <a name="hibernate"></a>
- **Description** : Un framework ORM (Object-Relational Mapping) pour Java, qui permet de mapper les classes Java à des tables de base de données et de simplifier les opérations CRUD.
- **Tip** : Réduit le besoin d'écrire du SQL manuel en gérant la persistance des objets Java.
- **Exemple (avec Hibernate)** :
```JAVA
@Entity
@Table(name = "Users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    private String email;
    
    // Getters et Setters
}
```

---
