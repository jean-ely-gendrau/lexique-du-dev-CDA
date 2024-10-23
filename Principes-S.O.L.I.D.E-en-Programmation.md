# Principes S.O.L.I.D.E en Programmation

Le principe S.O.L.I.D.E est un ensemble de cinq principes de conception qui visent à améliorer la lisibilité et la maintenabilité du code dans le développement logiciel. Ces principes sont particulièrement pertinents dans le cadre de la programmation orientée objet. En suivant ces principes, les développeurs peuvent créer des systèmes plus flexibles, extensibles et faciles à comprendre.

## Sommaire

- [S - Single Responsibility Principle](#s---single-responsibility-principle)
- [O - Open/Closed Principle](#o---openclosed-principle)
- [L - Liskov Substitution Principle](#l---liskov-substitution-principle)
- [I - Interface Segregation Principle](#i---interface-segregation-principle)
- [D - Dependency Inversion Principle](#d---dependency-inversion-principle)

## Tableau Récapitulatif des Éléments

| Nom                            | Type de Donnée | Taille   | Description                                          |
|--------------------------------|----------------|----------|-----------------------------------------------------|
| S - Single Responsibility       | Principe       | -        | Une classe ne doit avoir qu'une seule responsabilité. |
| O - Open/Closed                | Principe       | -        | Les entités doivent être ouvertes à l'extension, mais fermées à la modification. |
| L - Liskov Substitution        | Principe       | -        | Les objets d'une classe dérivée doivent pouvoir remplacer ceux de la classe de base. |
| I - Interface Segregation      | Principe       | -        | Les clients ne doivent pas être forcés d'utiliser des interfaces qu'ils n'utilisent pas. |
| D - Dependency Inversion        | Principe       | -        | Les modules de haut niveau ne doivent pas dépendre des modules de bas niveau, mais tous deux doivent dépendre d'abstractions. |

## S - Single Responsibility Principle

### Description
Le principe de responsabilité unique stipule qu'une classe ne doit avoir qu'une seule raison de changer, c'est-à-dire qu'elle doit être responsable d'une seule fonctionnalité.

### Exemple d'implémentation

```java
class Report {
    void generateReport() {
        // Génération du rapport
    }
}

class ReportPrinter {
    void printReport(Report report) {
        // Imprimer le rapport
    }
}
```

### Conseils
- Évitez de créer des classes « Dieu » qui font trop de choses. 
- Pensez à la séparation des préoccupations.

### Avertissements
- Ne pas suivre ce principe peut rendre le code difficile à tester et à maintenir.

## O - Open/Closed Principle

### Description
Le principe ouvert/fermé stipule que les entités (classes, modules, fonctions, etc.) doivent être ouvertes à l'extension mais fermées à la modification.

### Exemple d'implémentation

```java
abstract class Shape {
    abstract double area();
}

class Circle extends Shape {
    double radius;
    Circle(double radius) {
        this.radius = radius;
    }
    double area() {
        return Math.PI * radius * radius;
    }
}
```

### Conseils
- Utilisez des interfaces et des classes abstraites pour permettre l'extension.
- Appliquez le patron de conception « Stratégie » ou « Observateur ».

### Avertissements
- Modifier des classes existantes peut introduire des bogues inattendus.

## L - Liskov Substitution Principle

### Description
Le principe de substitution de Liskov indique que les objets d'une classe dérivée doivent pouvoir remplacer ceux de la classe de base sans altérer la validité du programme.

### Exemple d'implémentation

```java
class Bird {
    void fly() {
        // Voler
    }
}

class Sparrow extends Bird {
    void fly() {
        // Voler comme un moineau
    }
}

class Ostrich extends Bird {
    void fly() {
        // Ne peut pas voler, donc ça violerait LSP
    }
}
```

### Conseils
- Évitez de créer des classes dérivées qui ne respectent pas les comportements de la classe de base.

### Avertissements
- Ne pas suivre ce principe peut entraîner des comportements inattendus dans le code.

## I - Interface Segregation Principle

### Description
Le principe de séparation des interfaces stipule que les clients ne doivent pas être forcés d'utiliser des interfaces qu'ils n'utilisent pas.

### Exemple d'implémentation

```java
interface Printer {
    void print();
}

interface Scanner {
    void scan();
}

class MultiFunctionPrinter implements Printer, Scanner {
    public void print() {
        // Imprimer
    }
    public void scan() {
        // Scanner
    }
}
```

### Conseils
- Divisez les interfaces larges en interfaces plus petites et spécifiques.

### Avertissements
- Des interfaces encombrées peuvent rendre le code difficile à gérer.

## D - Dependency Inversion Principle

### Description
Le principe d'inversion des dépendances stipule que les modules de haut niveau ne doivent pas dépendre des modules de bas niveau, mais tous deux doivent dépendre d'abstractions.

### Exemple d'implémentation

```java
interface Database {
    void save();
}

class MySQLDatabase implements Database {
    public void save() {
        // Sauvegarder dans MySQL
    }
}

class UserService {
    private Database database;

    UserService(Database database) {
        this.database = database;
    }

    void saveUser() {
        database.save();
    }
}
```

### Conseils
- Utilisez l'injection de dépendances pour gérer les dépendances.

### Avertissements
- Une mauvaise gestion des dépendances peut compliquer le test unitaire du code.
