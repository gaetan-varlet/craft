# Software craftsmanship

Dépôt regroupant les principes craft ainsi que des liens vers des exemples

Le software craftsmanship, c'est :
- une communauté de professionnels
- l'excellence technique
- un logiciel bien conçu
- l'ajout de valeur
- une démarche de partenariat avec le client
- l'amélioration continue
- des outils

Les grandes thématiques à aborder :
- bonnes pratiques du craft (SOLID, TDD, Design Pattern…)
- architecture hexagonale
- clean architecture
- micro-services
- event-sourcing / CQRS / CQS
- Domain Driven Design

# Les bonnes pratiques du craft

## Le développement dirigé par les tests (TDD)

- proposé par Kent Beck à la fin des années 1990
- technique de développement qui ne se limite pas aux tests
- un des piliers de l'Extreme Programming (XP) et du craft
- écrire le code de test avant le code de production
    - **Test-First** : test validant notre programme, par exemple, un unique test pour tester le comportement final
    - **Test-Driven Development** : guide le développeur avec un feedback permet, en avançant pas à pas (baby-steps)

![Red Green Refactor](./images/tdd_red_green_refactor.png)

Les lois du TDD :
- on doit écrire un test qui échoue avant d'érire n'importe quel code de production
- on ne doit écrire que le code suffisant pour que le test en échec réussisse

### Pourquoi faire du TDD ?

Avantages :
- plus de code mort
- fautes d'inattention décelées immédiatement
- presque plus besoin du mode debug
- moins de maintenance corrective => amélioration de la productivité
- sérénité pour le refactor
- plaisir de coder avec le confort généré
- documentation gratuite
- délégation aux collègues plus facile

Inconvénients :
- courbe d'apprentissage importante
- nécessite une discipline sans faille
- pratique mal interprétée qui peut mener à des tests fragiles et un surcoût

### Conseils

- commiter après chaque nouveau test qui passe / code refactoré
- nommer le test avec la règle de gestion qui est testée avec les mots clés **Shoud/When** (devrait/quand) : `divide_should_raise_an_error_when_denominator_is_zero`
- le corps du test doit être découpé en 3 parties avec les mots clés **Given/When/Then** :
    - initialisation des données
    - appel de la fonction à tester
    - vérification du résultat
- pour éviter les valeurs de retour en dur dans le code, possibilité d'écrire 2 tests pour la même règle de gestion

### Kata

[Fizz Buzz](https://github.com/gaetan-varlet/fizz-buzz)

## Le BDD / L'ATDD

Le Behaviour-Driven Development, ou programmation pilotée par le comportement
- favorise le dialogue avec le métier, via des exemples, pour éviter les quiproquos

L'Acceptance Test–Driven Development (développement piloté par les tests d'acceptation)
- mise en place des exemples définis dans le BDD, sous forme de tests
- utilisation d'un langage commun (Gherkin) pour écrire ces exemples sous forme de scénarios
- utilisation de Cucumber (ou autre) pour lire ses exemples

dépôt Michael Azerhad : https://github.com/mica16/BDD-TDD-Demo/tree/part3



# Clean Architecture

## Les avantages de la clean architecture

réduction des dépendances de la logique métier avec les services que l'on consomme afin de maintenir une application stable dans le temps
- être indépendant des frameworks : possibilité de switcher de technologie plus facilement
- être indépendant de l'interface utilisateur
- être indépendant de la base de données
- être indépendant de tout service ou système externe
- être testable sans éléments externes

## Les inconvénients

- ajout de complexité


## Mise en place de la Clean architecture sur un projet de cave à vin

- https://github.com/gaetan-varlet/clean-architecture

# Living Documentation

Pourquoi faire de la documentation ?
- il faut que ça serve à plusieurs personnes
- il faut que ce soit pérenne

D'autres possibilités :
- conversations over documentation
- pair-programming
- code is documentation
	- read the code, learn the business domain
	- DDD (Domain Driven Design) : investir dans le savoir métier
- Domain Immersion : aller voir comment travaille le métier pour gagner de l'information
- savoir métier : faire une documentation avec ce qui est stable uniquement, dans un wiki
- pour les comportements métier (qui changent souvent)
	- BDD (Behavior DD) : programmation pilotée par le comprtement
	- description de scénarios de type given/when/then
		- cela crée de la redondance avec le code
		- **Cucumber**, **Specflow** : permet de tester la documentation, vérifier qu'elle correspond au code
		- on parle de **Living Documentation**, assure le rôle de specs et de docs
		- versionné avec le code source
	- **Pikles**
		- Living Documentation generator: it takes your Specification (written in Gherkin, with Markdown descriptions) and turns them into an always up-to-date documentation of the current state of your software - in a variety of formats
- pour faire des diagrammes, utilisation d'outils **Plain-Text Diagram**, ce qui permet de versionner le diagramme sous forme de texte
- **Living glossary** : génération d'un glossaire à partir d'annotations dans notre code, comme **Doclet** par exemple
- **Living Diagram** : génération d'un diagramme à partir du code source


Ce qu'il ne faut pas faire :
1. Write code
2. Write tests
3. Write doc

Ce qu'il faut faire :
- write tests = write doc
- write code = write doc