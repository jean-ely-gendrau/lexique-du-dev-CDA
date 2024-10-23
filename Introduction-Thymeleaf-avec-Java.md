# Introduction à Thymeleaf avec Java

## Description générale

Thymeleaf est un moteur de template Java conçu pour créer des vues dynamiques dans les applications web. Il permet de générer des pages HTML à partir de modèles (templates) et de les peupler avec des données dynamiques issues de contrôleurs Java. Thymeleaf est souvent utilisé en combinaison avec des frameworks tels que Spring MVC pour construire des interfaces utilisateur.

Ce document vous guide à travers les différentes fonctionnalités de Thymeleaf, en mettant l'accent sur l'intégration avec Java, ainsi que des conseils pratiques, des astuces et des avertissements importants.

---

## Sommaire

1. [Syntaxe de base](#syntaxe-de-base)
2. [Gestion des variables](#gestion-des-variables)
3. [Boucles et conditions](#boucles-et-conditions)
4. [Fragments et inclusion](#fragments-et-inclusion)
5. [Formulaires et gestion des données](#formulaires-et-gestion-des-données)

---

## Tableau récapitulatif des principaux éléments de Thymeleaf

| Élément                   | Type           | Description                                                                           |
|---------------------------|----------------|---------------------------------------------------------------------------------------|
| `${variable}`              | Expression     | Injection de variables dans le template HTML                                          |
| `th:text`                  | Attribut HTML  | Définit le texte du contenu d'un élément HTML                                         |
| `th:if / th:unless`        | Attribut HTML  | Conditions pour afficher ou non des blocs de code HTML                                |
| `th:each`                  | Attribut HTML  | Boucle pour itérer sur une collection                                                 |
| `th:fragment`              | Attribut HTML  | Définit un fragment réutilisable dans plusieurs templates                             |
| `th:include`               | Attribut HTML  | Inclusion d'un fragment ou d'un autre template dans la page                           |
| `th:object`                | Attribut HTML  | Bind un objet à un formulaire pour faciliter la gestion des données                   |
| `th:field`                 | Attribut HTML  | Spécifie un champ de formulaire lié à une propriété d'un objet                        |

---

## 1. Syntaxe de base <a id="syntaxe-de-base"></a>

### Description

Thymeleaf utilise des expressions et des attributs spécifiques pour insérer dynamiquement du contenu dans des modèles HTML. L'expression la plus courante est `${variable}`, qui permet d'accéder à des données côté serveur et de les afficher dans la page HTML.

### Exemple d'implémentation

```html
<p th:text="${nom}">Nom par défaut</p>
```

Ce code remplace le texte "Nom par défaut" par la valeur de la variable `nom` si elle est présente.

### Astuces

- Utilisez `${}` pour afficher des variables, mais aussi pour manipuler des objets Java directement dans le template (par exemple `${user.name}`).
- Pensez à bien vérifier la présence des variables dans vos contrôleurs avant de les injecter dans les templates.

### Avertissements

- Si une variable n'existe pas dans le modèle, aucun message d'erreur ne sera levé par défaut. Pensez à valider les données avant le rendu.

---

## 2. Gestion des variables <a id="gestion-des-variables"></a>

### Description

Thymeleaf permet de manipuler des variables depuis le modèle de données. Ces variables peuvent être des objets Java, des collections ou des simples types de données.

### Exemple d'implémentation

```html
<h1 th:text="'Bonjour, ' + ${nom}">Bonjour, invité</h1>
```

Si la variable `nom` contient "Marie", le rendu sera "Bonjour, Marie".

### Astuces

- Utilisez les expressions pour concaténer des chaînes, faire des opérations mathématiques ou encore accéder à des propriétés d'objets complexes.

### Avertissements

- Évitez d'imbriquer trop d'expressions pour maintenir une bonne lisibilité.

---

## 3. Boucles et conditions <a id="boucles-et-conditions"></a>

### Description

Thymeleaf offre des mécanismes pour itérer sur des collections (`th:each`) et ajouter des conditions (`th:if`, `th:unless`) pour contrôler l'affichage des éléments HTML.

### Exemple d'implémentation

```html
<ul>
    <li th:each="item : ${items}" th:text="${item}">Item par défaut</li>
</ul>
```

Ce code génère une liste d'éléments HTML basée sur la collection `items`.

### Astuces

- Vous pouvez accéder à l'index de l'itération en utilisant `${#iter.index}` dans vos boucles.
- Combinez `th:if` avec `th:each` pour ne pas afficher de section si la collection est vide.

### Avertissements

- Faites attention aux collections nulles : prévoyez toujours des mécanismes de vérification pour éviter les erreurs de rendu.

---

## 4. Fragments et inclusion <a id="fragments-et-inclusion"></a>

### Description

Les fragments sont des blocs de templates réutilisables. Cela permet de mieux organiser le code en séparant les parties communes (en-tête, pied de page) dans des fichiers séparés.

### Exemple d'implémentation

Définir un fragment :

```html
<div th:fragment="entete">Ceci est l'en-tête</div>
```

Inclure un fragment dans une autre page :

```html
<div th:include="fragments :: entete"></div>
```

### Astuces

- Utilisez les fragments pour des éléments récurrents (navigation, pied de page, etc.), ce qui facilite la maintenance et la modularité de vos templates.
- Vous pouvez passer des paramètres aux fragments via des expressions.

### Avertissements

- N'abusez pas des inclusions de fragments pour éviter une surcharge inutile des pages HTML.

---

## 5. Formulaires et gestion des données <a id="formulaires-et-gestion-des-données"></a>

### Description

Thymeleaf propose des fonctionnalités dédiées pour la gestion des formulaires. En liant directement les champs du formulaire à des propriétés d'un objet, vous facilitez la validation et la récupération des données en Java.

### Exemples d'implémentations

```html
<form th:object="${user}" action="#" method="post">
    <input type="text" th:field="*{nom}" />
    <input type="submit" value="Envoyer" />
</form>
```

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Formulaire Utilisateur</title>
</head>
<body>
    <h1>Formulaire d'inscription</h1>

    <form action="#" th:action="@{/formulaire}" th:object="${utilisateur}" method="post">
        <div>
            <label for="nom">Nom:</label>
            <input type="text" id="nom" th:field="*{nom}" />
        </div>
        <div>
            <label for="email">Email:</label>
            <input type="email" id="email" th:field="*{email}" />
        </div>
        <div>
            <button type="submit">Soumettre</button>
        </div>
    </form>
</body>
</html>
```

Ce code génère un formulaire lié à l'objet `user` et à sa propriété `nom`.

### Astuces

- Utilisez `th:object` pour binder un objet à un formulaire et `th:field` pour lier directement les champs aux propriétés de cet objet.
- Pensez à la validation des formulaires côté serveur et à l'affichage des erreurs dans le template.

### Avertissements

- Assurez-vous de bien sécuriser vos formulaires contre les attaques de type CSRF en ajoutant des jetons de sécurité.

---
