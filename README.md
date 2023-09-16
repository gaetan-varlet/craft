# Software craftsmanship
Dépôt regroupant les principes craft ainsi que des liens vers des exemples

Le software craftsmanship, c'est :
- une communauté de professionnels, l'excellence technique, un logiciel bien conçu, l'ajout de valeur
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

- **Test-First** : test validant notre programme, par exemple, un unique test pour tester le comportement final
- **Test-Driven Development** : guide le développeur avec un feedback permet, en avançant pas à pas (baby-steps)

Les lois du TDD :
- interdiction d'écrire du nouveau code sauf pour faire passer un test qui échoue
- interdiction d'écrire plus de code qu'il n'en faut pour réussir le test ayant échoué

Exemple : exercice [Fizz Buzz](https://github.com/gaetan-varlet/fizz-buzz)

### Pourquoi faire du TDD ?

Avantages :
- plus de code mort
- fautes d'inattention décelées immédiatement
- presque plus besoin du mode debug
- moins de maintenance corrective => amélioration de la productivité
- sérénite pour le refactor
- plaisir de coder avec le confort généré
- documentation gratuite
- délégation aux collègues plus facile

Inconvénients :
- courbe d'apprentissage importante
- nécessite une discipline sansa faille
- pratique mal interprétée qui peut mener à des tests fragiles et un surcoût



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