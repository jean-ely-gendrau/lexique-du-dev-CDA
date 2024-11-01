# Tests en Java

## Description Générale

Les tests en Java sont essentiels pour garantir la qualité et la robustesse du code. Ils permettent de valider les fonctionnalités, d'assurer la fiabilité, et d'identifier rapidement les bugs. Parmi les outils couramment utilisés pour les tests en Java, on trouve **JUnit** pour les tests unitaires, **Mockito** pour le mocking, et **Spring Data JPA** pour les tests d'intégration avec des bases de données. Ces outils offrent des moyens variés pour isoler, simuler, et tester les composants de l'application.

## Sommaire

1. [Tableau récapitulatif des éléments](#tableau-récapitulatif-des-éléments)
2. [Annotations de Test en Java](#annotations-de-test-en-java)
3. [Tests Unitaires avec JUnit](#tests-unitaires-avec-junit)
4. [Mocking avec Mockito](#mocking-avec-mockito)
5. [Tests de Base de Données avec Spring Data JPA](#tests-de-base-de-données-avec-spring-data-jpa)
6. [Ressources Externes](#ressources-externes)

---

## Tableau récapitulatif des éléments

| Nom                                | Type       | Description                                                                                           |
|------------------------------------|------------|-------------------------------------------------------------------------------------------------------|
| `@Test`                            | Annotation | Marque une méthode comme un test JUnit.                                                               |
| `@BeforeEach`                      | Annotation | Exécute une méthode avant chaque test. Utile pour initialiser des objets communs.                     |
| `@AfterEach`                       | Annotation | Exécute une méthode après chaque test, souvent pour libérer les ressources.                           |
| `@Mock`                            | Annotation | Crée un mock d'une classe pour simuler son comportement.                                              |
| `@InjectMocks`                     | Annotation | Injecte les mocks dans la classe testée pour simuler des dépendances.                                 |
| `@DataJpaTest`                     | Annotation | Active les tests spécifiques à JPA en configurant une base de données en mémoire.                     |
| `@Transactional`                   | Annotation | Exécute chaque test dans une transaction annulée à la fin (rollback).                                 |
| `@Sql`                             | Annotation | Exécute un script SQL pour pré-remplir ou nettoyer la base de données avant ou après un test.         |
| `@AutoConfigureTestDatabase`       | Annotation | Configure la base de données utilisée pour les tests, en utilisant H2 par défaut.                     |
| `@SpringBootTest`                  | Annotation | Charge le contexte complet de l’application pour les tests d’intégration.                             |

---

## Annotations de Test en Java

### `@Test`

#### Description
L'annotation `@Test` marque une méthode comme un test JUnit, permettant ainsi d'exécuter des assertions pour vérifier le comportement du code.

#### Exemple d'implémentation
```java
@Test
public void testAddition() {
    int result = calculator.add(2, 3);
    assertEquals(5, result);
}
```

#### Conseils ou astuces
- Utilisez des noms de méthodes de test explicites pour comprendre facilement ce qui est testé.

#### Avertissements ou notes
- Assurez-vous d'exécuter `@BeforeEach` pour initialiser les objets nécessaires avant chaque test.

---

### `@DataJpaTest`

#### Description
`@DataJpaTest` est une annotation Spring Boot qui configure uniquement les composants de persistance, comme les repositories, et utilise une base de données en mémoire pour les tests.

#### Exemple d'implémentation
```java
@DataJpaTest
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    public void testFindByEmail() {
        User user = new User("test@example.com");
        userRepository.save(user);
        User foundUser = userRepository.findByEmail("test@example.com");
        assertEquals("test@example.com", foundUser.getEmail());
    }
}
```

#### Conseils ou astuces
- Utilisez `@Rollback` si des transactions spécifiques nécessitent un rollback en fin de test.
  
#### Avertissements ou notes
- `@DataJpaTest` configure une base en mémoire, donc évitez de l'utiliser pour tester contre des bases de données réelles.

---

## Tests Unitaires avec JUnit

### Description
JUnit est un framework de test unitaire qui permet d'écrire et d'exécuter des tests pour vérifier le bon fonctionnement des unités de code.

### Exemple d'implémentation
```java
@BeforeEach
public void setUp() {
    calculator = new Calculator();
}

@Test
public void testMultiply() {
    int result = calculator.multiply(3, 4);
    assertEquals(12, result);
}
```

### Conseils ou astuces
- Utilisez `@BeforeEach` et `@AfterEach` pour configurer et nettoyer l'environnement de test.
  
### Avertissements ou notes
- Les tests doivent être isolés et ne pas dépendre de l'ordre d'exécution.

---

## Mocking avec Mockito

### Description
Mockito est un framework permettant de simuler des objets (mocks) pour les tests unitaires. Cela permet de tester des classes isolées en simulant leurs dépendances.

### Exemple d'implémentation
```java
@ExtendWith(MockitoExtension.class)
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    public void testFindUser() {
        User user = new User("test@example.com");
        when(userRepository.findByEmail("test@example.com")).thenReturn(user);
        
        User found = userService.findUser("test@example.com");
        assertEquals("test@example.com", found.getEmail());
    }
}
```

### Conseils ou astuces
- Utilisez `@InjectMocks` pour injecter automatiquement les mocks dans la classe à tester.
  
### Avertissements ou notes
- Évitez d'utiliser des mocks pour tester des interactions avec la base de données dans les tests d'intégration.

---

## Tests de Base de Données avec Spring Data JPA

### Description
Spring Data JPA permet de tester les opérations de persistance avec des bases de données en mémoire (comme H2), en utilisant des annotations comme `@DataJpaTest`.

### Exemple d'implémentation avec H2
```java
@DataJpaTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
public class ProductRepositoryTest {

    @Autowired
    private ProductRepository productRepository;

    @Test
    public void testSaveProduct() {
        Product product = new Product("Laptop", 1000.0);
        productRepository.save(product);

        Product found = productRepository.findById(product.getId()).orElse(null);
        assertNotNull(found);
        assertEquals("Laptop", found.getName());
    }
}
```

### Conseils ou astuces
- Configurez `@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)` pour tester contre une vraie base de données si nécessaire.
  
### Avertissements ou notes
- `@DataJpaTest` est souvent utilisé avec une base de données en mémoire pour éviter de polluer la base de données de production.

---

## Ressources Externes

1. **Spring Documentation** - [Testing the Data Access Layer](https://docs.spring.io/spring-framework/docs/current/reference/html/testing.html)
2. **Baeldung** :
   - [Testing JPA Queries with Spring Boot and @DataJpaTest](https://www.baeldung.com/spring-boot-testing-jpa-repositories)
   - [Guide to @DataJpaTest in Spring Boot](https://www.baeldung.com/spring-boot-datajpatest)
   - [Spring Boot Testing: Writing JUnit Tests Using an H2 Database](https://www.baeldung.com/spring-boot-testing-in-memory-database)
3. **JUnit 5 User Guide** - [Documentation JUnit](https://junit.org/junit5/docs/current/user-guide/)
4. **Mockito Documentation** - [Mockito Official Documentation](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html)
5. **Java Code Geeks** - [Mocking Database Connections in Java](https://www.javacodegeeks.com/2020/01/mocking-database-connections-java.html)
6. **YouTube** - Chaînes recommandées :
   - **Amigoscode** : [Amigoscode sur YouTube](https://www.youtube.com/c/amigoscode)
   - **TechPrimers** : [TechPrimers sur YouTube](https://www.youtube.com/c/TechPrimers)

---
