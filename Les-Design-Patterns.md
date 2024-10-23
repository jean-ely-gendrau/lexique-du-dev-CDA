# Les Design Patterns

## Introduction

Les **Design Patterns** (ou modèles de conception) sont des solutions éprouvées pour résoudre des problèmes récurrents dans le développement logiciel. Ils permettent d'améliorer la maintenance, la réutilisabilité et la flexibilité du code en proposant des solutions standardisées. 

On classe généralement ces patterns en trois grandes catégories :
- **Créationnels**
- **Structuraux**
- **Comportementaux**

## Sommaire

- [Tableau récapitulatif des Design Patterns](#tableau-récapitulatif-des-design-patterns)
- [Design Patterns Créationnels](#design-patterns-créationnels)
- [Design Patterns Structuraux](#design-patterns-structuraux)
- [Design Patterns Comportementaux](#design-patterns-comportementaux)

## Tableau récapitulatif des Design Patterns

| Nom du Pattern           | Type            | Description                                           |
|-------------------------|------------------|------------------------------------------------------|
| Singleton                | Créationnel      | Garantit qu'une classe n'a qu'une seule instance et fournit un point d'accès global à celle-ci. |
| Factory Method           | Créationnel      | Définit une interface pour créer un objet, mais laisse les sous-classes décider de la classe à instancier. |
| Abstract Factory         | Créationnel      | Fournit une interface pour créer des familles d'objets sans spécifier leurs classes concrètes. |
| Builder                  | Créationnel      | Permet de construire un objet complexe étape par étape. |
| Prototype                | Créationnel      | Permet de créer des objets en copiant un prototype.  |
| Adapter                  | Structurel       | Permet à des classes incompatibles de travailler ensemble en les adaptant. |
| Composite                | Structurel       | Compose des objets en structures arborescentes pour représenter des hiérarchies partie-tout. |
| Decorator                | Structurel       | Ajoute dynamiquement des fonctionnalités à un objet. |
| Facade                   | Structurel       | Fournit une interface simplifiée à un ensemble d'interfaces d'un sous-système. |
| Proxy                    | Structurel       | Contrôle l'accès à un autre objet en le représentant. |
| Chain of Responsibility   | Comportemental   | Permet à plusieurs objets de traiter une requête sans connaître le demandeur. |
| Command                  | Comportemental   | Encapsule une demande en tant qu'objet, permettant de paramétrer les clients avec des requêtes. |
| Interpreter              | Comportemental   | Donne une représentation grammaticale d'un langage et un interprète pour évaluer les phrases. |
| Iterator                 | Comportemental   | Fournit un moyen d'accéder aux éléments d'un agrégat sans exposer sa représentation sous-jacente. |
| Mediator                 | Comportemental   | Définit un objet qui encapsule la manière dont un ensemble d'objets interagit. |
| Observer                 | Comportemental   | Permet à un objet d'informer d'autres objets des changements d'état. |
| Strategy                 | Comportemental   | Définit une famille d'algorithmes, encapsule chacun d'eux et les rend interchangeables. |
| Template Method          | Comportemental   | Définit le squelette d'un algorithme dans une méthode, laissant certaines étapes à des sous-classes. |

## Design Patterns Créationnels

### Singleton

- **Description** : Garantit qu'une classe n'a qu'une seule instance et fournit un point d'accès global à celle-ci.
  
- **Exemple d'implémentation** :
  $$$java
  public class Singleton {
      private static Singleton instance;

      private Singleton() {}

      public static Singleton getInstance() {
          if (instance == null) {
              instance = new Singleton();
          }
          return instance;
      }
  }
  $$$

- **Conseils** : Utilisez le pattern Singleton pour des ressources partagées comme des connexions à une base de données.

- **Avertissements** : Évitez d'utiliser des Singletons dans des environnements multithreadés sans synchronisation.

### Factory Method

- **Description** : Définit une interface pour créer un objet, mais laisse les sous-classes décider de la classe à instancier.

- **Exemple d'implémentation** :
  $$$java
  interface Product {
      void use();
  }

  class ConcreteProductA implements Product {
      public void use() {
          System.out.println("Utilisation de Produit A");
      }
  }

  class ConcreteProductB implements Product {
      public void use() {
          System.out.println("Utilisation de Produit B");
      }
  }

  abstract class Creator {
      public abstract Product factoryMethod();
  }

  class ConcreteCreatorA extends Creator {
      public Product factoryMethod() {
          return new ConcreteProductA();
      }
  }

  class ConcreteCreatorB extends Creator {
      public Product factoryMethod() {
          return new ConcreteProductB();
      }
  }
  $$$

- **Conseils** : Utilisez Factory Method pour promouvoir la flexibilité et la réutilisation du code.

- **Avertissements** : Veillez à ne pas surcharger la création d'objets, ce qui pourrait compliquer le code.

### Abstract Factory

- **Description** : Fournit une interface pour créer des familles d'objets sans spécifier leurs classes concrètes.

- **Exemple d'implémentation** :
  $$$java
  interface AbstractFactory {
      ProductA createProductA();
      ProductB createProductB();
  }

  class ConcreteFactory1 implements AbstractFactory {
      public ProductA createProductA() {
          return new ProductA1();
      }
      public ProductB createProductB() {
          return new ProductB1();
      }
  }

  class ConcreteFactory2 implements AbstractFactory {
      public ProductA createProductA() {
          return new ProductA2();
      }
      public ProductB createProductB() {
          return new ProductB2();
      }
  }
  $$$

- **Conseils** : Utilisez Abstract Factory lorsque vous devez garantir que des objets compatibles sont créés.

- **Avertissements** : La complexité peut augmenter rapidement en ajoutant de nouvelles familles de produits.

### Builder

- **Description** : Permet de construire un objet complexe étape par étape.

- **Exemple d'implémentation** :
  $$$java
  class Product {
      private String partA;
      private String partB;

      public void setPartA(String partA) { this.partA = partA; }
      public void setPartB(String partB) { this.partB = partB; }
  }

  class Builder {
      private Product product = new Product();

      public Builder buildPartA(String partA) {
          product.setPartA(partA);
          return this;
      }

      public Builder buildPartB(String partB) {
          product.setPartB(partB);
          return this;
      }

      public Product getResult() {
          return product;
      }
  }
  $$$

- **Conseils** : Utilisez Builder pour créer des objets complexes, en séparant la construction de leur représentation.

- **Avertissements** : Le pattern peut être surdimensionné pour des objets simples.

### Prototype

- **Description** : Permet de créer des objets en copiant un prototype.

- **Exemple d'implémentation** :
  $$$java
  class Prototype implements Cloneable {
      public Prototype clone() {
          try {
              return (Prototype) super.clone();
          } catch (CloneNotSupportedException e) {
              return null;
          }
      }
  }
  $$$

- **Conseils** : Utilisez Prototype pour éviter le coût de création d'objets complexes.

- **Avertissements** : Faites attention aux objets immuables, car les modifications peuvent affecter le prototype.

## Design Patterns Structuraux

### Adapter

- **Description** : Permet à des classes incompatibles de travailler ensemble en les adaptant.

- **Exemple d'implémentation** :
  $$$java
  class Target {
      public void request() {
          System.out.println("Target: request");
      }
  }

  class Adaptee {
      public void specificRequest() {
          System.out.println("Adaptee: specificRequest");
      }
  }

  class Adapter extends Target {
      private Adaptee adaptee;

      public Adapter(Adaptee adaptee) {
          this.adaptee = adaptee;
      }

      public void request() {
          adaptee.specificRequest();
      }
  }
  $$$

- **Conseils** : Utilisez le pattern Adapter pour intégrer des systèmes existants.

- **Avertissements** : L'adaptation peut cacher des incompatibilités structurelles.

### Composite

- **Description** : Compose des objets en structures arborescentes pour représenter des hiérarchies partie-tout.

- **Exemple d'implémentation** :
  $$$java
  interface Component {
      void operation();
  }

  class Leaf implements Component {
      public void operation() {
          System.out.println("Leaf operation");
      }
  }

  class Composite implements Component {
      private List<Component> children = new ArrayList<>();

      public void add(Component component) {
          children.add(component);
      }

      public void operation() {
          for (Component child : children) {
              child.operation();
          }
      }
  }
  $$$

- **Conseils** : Utilisez Composite pour traiter des objets individuels et des compositions d'objets de manière uniforme.

- **Avertissements** : L'utilisation excessive de Composite peut rendre la structure complexe.

### Decorator

- **Description** : Ajoute dynamiquement des fonctionnalités à un objet.

- **Exemple d'implémentation** :
  $$$java
  interface Component {
      void operation();
  }

  class ConcreteComponent implements Component {
      public void operation() {
          System.out.println("ConcreteComponent operation");
      }
  }

  class Decorator implements Component {
      protected Component component;

      public Decorator(Component component) {
          this.component = component;
      }

      public void operation() {
          component.operation();
      }
  }

  class ConcreteDecorator extends Decorator {
      public ConcreteDecorator(Component component) {
          super(component);
      }

      public void operation() {
          super.operation();
          System.out.println("ConcreteDecorator operation");
      }
  }
  $$$

- **Conseils** : Utilisez le pattern Decorator pour ajouter des responsabilités à des objets au lieu de créer des sous-classes.

- **Avertissements** : Trop de décorateurs peuvent rendre le système difficile à comprendre.

### Facade

- **Description** : Fournit une interface simplifiée à un ensemble d'interfaces d'un sous-système.

- **Exemple d'implémentation** :
  $$$java
  class SubsystemA {
      public void operationA() {
          System.out.println("SubsystemA: operationA");
      }
  }

  class SubsystemB {
      public void operationB() {
          System.out.println("SubsystemB: operationB");
      }
  }

  class Facade {
      private SubsystemA subsystemA = new SubsystemA();
      private SubsystemB subsystemB = new SubsystemB();

      public void operation() {
          subsystemA.operationA();
          subsystemB.operationB();
      }
  }
  $$$

- **Conseils** : Utilisez Facade pour réduire la complexité d'un système.

- **Avertissements** : Une façade trop générale peut masquer des fonctionnalités essentielles.

### Proxy

- **Description** : Contrôle l'accès à un autre objet en le représentant.

- **Exemple d'implémentation** :
  $$$java
  interface Subject {
      void request();
  }

  class RealSubject implements Subject {
      public void request() {
          System.out.println("RealSubject: request");
      }
  }

  class Proxy implements Subject {
      private RealSubject realSubject;

      public void request() {
          if (realSubject == null) {
              realSubject = new RealSubject();
          }
          realSubject.request();
      }
  }
  $$$

- **Conseils** : Utilisez Proxy pour ajouter des fonctionnalités comme la mise en cache ou la sécurité.

- **Avertissements** : Le proxy peut introduire une surcharge de performance.

## Design Patterns Comportementaux

### Chain of Responsibility

- **Description** : Permet à plusieurs objets de traiter une requête sans connaître le demandeur.

- **Exemple d'implémentation** :
  $$$java
  abstract class Handler {
      protected Handler successor;

      public void setSuccessor(Handler successor) {
          this.successor = successor;
      }

      public abstract void handleRequest(int request);
  }

  class ConcreteHandlerA extends Handler {
      public void handleRequest(int request) {
          if (request < 10) {
              System.out.println("Handler A handled request " + request);
          } else if (successor != null) {
              successor.handleRequest(request);
          }
      }
  }

  class ConcreteHandlerB extends Handler {
      public void handleRequest(int request) {
          if (request >= 10) {
              System.out.println("Handler B handled request " + request);
          } else if (successor != null) {
              successor.handleRequest(request);
          }
      }
  }
  $$$

- **Conseils** : Utilisez ce pattern pour éviter des conditions if-else complexes.

- **Avertissements** : Évitez d'avoir une chaîne trop longue, ce qui peut nuire aux performances.

### Command

- **Description** : Encapsule une demande en tant qu'objet, permettant de paramétrer les clients avec des requêtes.

- **Exemple d'implémentation** :
  $$$java
  interface Command {
      void execute();
  }

  class ConcreteCommand implements Command {
      private Receiver receiver;

      public ConcreteCommand(Receiver receiver) {
          this.receiver = receiver;
      }

      public void execute() {
          receiver.action();
      }
  }

  class Receiver {
      public void action() {
          System.out.println("Receiver action executed");
      }
  }
  $$$

- **Conseils** : Utilisez Command pour soutenir des opérations annulables ou des journaux d'opérations.

- **Avertissements** : Évitez de créer des commandes trop complexes.

### Interpreter

- **Description** : Donne une représentation grammaticale d'un langage et un interprète pour évaluer les phrases.

- **Exemple d'implémentation** :
  $$$java
  interface Expression {
      int interpret();
  }

  class Number implements Expression {
      private int number;

      public Number(int number) {
          this.number = number;
      }

      public int interpret() {
          return number;
      }
  }

  class Plus implements Expression {
      private Expression left;
      private Expression right;

      public Plus(Expression left, Expression right) {
          this.left = left;
          this.right = right;
      }

      public int interpret() {
          return left.interpret() + right.interpret();
      }
  }
  $$$

- **Conseils** : Utilisez Interpreter pour des langages simples ou des grammaires spécifiques.

- **Avertissements** : Évitez d'utiliser ce pattern pour des langages complexes.

### Iterator

- **Description** : Fournit un moyen d'accéder aux éléments d'un agrégat sans exposer sa représentation sous-jacente.

- **Exemple d'implémentation** :
  $$$java
  interface Iterator {
      boolean hasNext();
      Object next();
  }

  interface Aggregate {
      Iterator createIterator();
  }

  class ConcreteAggregate implements Aggregate {
      private List<Object> items = new ArrayList<>();

      public void add(Object item) {
          items.add(item);
      }

      public Iterator createIterator() {
          return new ConcreteIterator(this);
      }

      public List<Object> getItems() {
          return items;
      }
  }

  class ConcreteIterator implements Iterator {
      private ConcreteAggregate aggregate;
      private int current = 0;

      public ConcreteIterator(ConcreteAggregate aggregate) {
          this.aggregate = aggregate;
      }

      public boolean hasNext() {
          return current < aggregate.getItems().size();
      }

      public Object next() {
          return aggregate.getItems().get(current++);
      }
  }
  $$$

- **Conseils** : Utilisez Iterator pour parcourir des collections sans exposer leur structure.

- **Avertissements** : Assurez-vous que l'itérateur reste synchronisé avec la collection.

### Mediator

- **Description** : Définit un objet qui encapsule la manière dont un ensemble d'objets interagit.

- **Exemple d'implémentation** :
  $$$java
  interface Mediator {
      void notify(Component sender, String event);
  }

  class ConcreteMediator implements Mediator {
      private ComponentA componentA;
      private ComponentB componentB;

      public void setComponentA(ComponentA componentA) {
          this.componentA = componentA;
      }

      public void setComponentB(ComponentB componentB) {
          this.componentB = componentB;
      }

      public void notify(Component sender, String event) {
          if (sender == componentA) {
              componentB.doSomething();
          } else if (sender == componentB) {
              componentA.doSomething();
          }
      }
  }

  class ComponentA {
      private Mediator mediator;

      public ComponentA(Mediator mediator) {
          this.mediator = mediator;
      }

      public void doSomething() {
          System.out.println("Component A does something");
          mediator.notify(this, "A");
      }
  }

  class ComponentB {
      private Mediator mediator;

      public ComponentB(Mediator mediator) {
          this.mediator = mediator;
      }

      public void doSomething() {
          System.out.println("Component B does something");
          mediator.notify(this, "B");
      }
  }
  $$$

- **Conseils** : Utilisez Mediator pour réduire les dépendances entre les composants.

- **Avertissements** : Un médiateur trop complexe peut devenir difficile à gérer.

### Observer

- **Description** : Permet à un objet d'informer d'autres objets des changements d'état.

- **Exemple d'implémentation** :
  $$$java
  interface Observer {
      void update(String message);
  }

  class ConcreteObserver implements Observer {
      public void update(String message) {
          System.out.println("Observer received: " + message);
      }
  }

  class Subject {
      private List<Observer> observers = new ArrayList<>();

      public void attach(Observer observer) {
          observers.add(observer);
      }

      public void notifyObservers(String message) {
          for (Observer observer : observers) {
              observer.update(message);
          }
      }
  }
  $$$

- **Conseils** : Utilisez Observer pour des notifications en temps réel entre objets.

- **Avertissements** : Évitez des dépendances circulaires entre le sujet et les observateurs.

### Strategy

- **Description** : Définit une famille d'algorithmes, encapsule chacun d'eux et les rend interchangeables.

- **Exemple d'implémentation** :
  $$$java
  interface Strategy {
      void execute();
  }

  class ConcreteStrategyA implements Strategy {
      public void execute() {
          System.out.println("Strategy A executed");
      }
  }

  class ConcreteStrategyB implements Strategy {
      public void execute() {
          System.out.println("Strategy B executed");
      }
  }

  class Context {
      private Strategy strategy;

      public void setStrategy(Strategy strategy) {
          this.strategy = strategy;
      }

      public void executeStrategy() {
          strategy.execute();
      }
  }
  $$$

- **Conseils** : Utilisez Strategy pour rendre le code plus flexible et évolutif.

- **Avertissements** : Trop de stratégies peuvent rendre le code difficile à gérer.

### Template Method

- **Description** : Définit le squelette d'un algorithme dans une méthode, laissant certaines étapes à des sous-classes.

- **Exemple d'implémentation** :
  $$$java
  abstract class AbstractClass {
      public final void templateMethod() {
          stepOne();
          stepTwo();
      }

      protected abstract void stepOne();
      protected abstract void stepTwo();
  }

  class ConcreteClass extends AbstractClass {
      protected void stepOne() {
          System.out.println("ConcreteClass step one");
      }

      protected void stepTwo() {
          System.out.println("ConcreteClass step two");
      }
  }
  $$$

- **Conseils** : Utilisez Template Method pour éviter la duplication de code.

- **Avertissements** : Évitez de rendre la méthode template trop complexe.

---

