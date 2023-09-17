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

## Techniques de Clean Code

- code syntaximent correct VS **code lisible et compréhensible, facile à maintenir et à faire évoluer**
- **théorie de la vitre brisée**
    - dégradation qui n'est pas réparée va entrainer d'autres dégradations
    - fonctionne pour des bases de code déjà saines
- **règle du boy-scout**
    - laisser le code modifié dans un meilleur état que celui où on l'a trouvé
    - amélioration progressive du code

Rester simple et aller à l'essentiel
- **KISS** : Keep It Simple and Stupid, invite à faire le code le plus simple possible
- **YAGNI** : You Ain't Gonna Need It (vous n'en aurez pas besoin)
La pratique du TDD nous permet également naturellement de faire cela

Les 4 règles du Simple Design (Kent Beck) :
- **passer les tests** : vérifier le bon fonctionnement, outil de documentation
- **révéler l'intention** : noms de variables et méthodes clairs, fonctions petites et simples, limitation des commentaires
- **éviter la duplication** : DRY (Don't Repeat Yourself), limiter à une seule représentation toute connaissance
- **rester petit** : pas de code mort, pas de complexité inutile

Exprimer l'intention
- expliquer ce qu'on fait et pourquoi, plutôt que comment
- l'art du nommage
    - s'appuyer sur le métier, se focaliser sur le service rendu
    - utiliser des noms pour les classes, des verbes pour les méthodes

Structure le code
- découper et organiser le code, pour avoir une vision d'ensemble et pouvoir naviguer dans les détails

Découper les fonctions
- se limiter à quelques lignes, sinon découper : une fontion ne doit faire qu'une seule chose
- le découpage en sous-fonction aide à hiérarchiser les niveaux d'abstraction
- séparation des considérations techniques et métiers


Commenter avec modération
- les commentaires peuvent être obsolètes
- code bien écrit possède une valeur documentaire : *Don't comment bad code, rewrite it*

```java
// récupération des adultes
List<Person> adultes = new ArrayList<>;
for(Person p : persons){
    if(person.getAge() >=18){
        adults.add(p);
    }
}
// suppression du commentaire en mettant le code dans une méthode : List<Person> findAdults(List<Person> persons);
```

Les commentaires utiles :
- signaler une subtilité
- marquer des problèmes à résoudre (TODO)

Ne pas se répéter (DRY)
- est-ce que les morceaux de code vont évoluer de concert ? si oui, **couplage**, sinon **duplication**
- chaque connaissance métier ne doit apparaître qu'une seule fois

Avoir du code de test propre :
- vérifier le comportement de l'applicaition mais aussi fournir une documentation exécutable

## Le développement dirigé par le comportement (BDD)

Le BDD (**Behaviour-Driven Development**), ou programmation pilotée par le comportement
- favorise le dialogue avec le métier, via des exemples, pour éviter les quiproquos

L'ATDD (**Acceptance Test–Driven Development**),développement piloté par les tests d'acceptation
- mise en place des exemples définis dans le BDD, sous forme de tests, dans un langage métier et non technique
- utilisation d'un langage commun (Gherkin) pour écrire ces exemples sous forme de scénarios
- utilisation de Cucumber (ou autre) pour lire ses exemples

3 rôles dans le BDD (**Tres Amigos**), se retrouvent dans des ateliers de spécifications :
- **le PO**, représentant le besoin
    - explique sa vision
- **le développeur**, représentant la mise en oeuvre
    - reformule, propose des aménagements ou alternatives pour aider à la réalisation
- **le testeur**, pour challenger les 2 autres
    - pose des questions sur les limtes du cas d'usage, pour vérifier que la proposition est bonne

Il est possible d'avoir des amigos supplémentaires selon les enjeux (UX, expert sécurité, juriste, service production)

Les bénéfices du BDD :
- la compréhension partagée entre tous
- tests servent de **critère d'acceptation**, puis de **tests de non régression**
- **living documentation** : documentation complète et à jour, disponible sous forme de rapport ou site web

Dans un contexte legacy, introduire des scénarios permet de documenter le comportement existant. On parle de **tests de caractérisation**, qui pourront être réutilisés dans une optique de ré-écriture.

## Le pair et le mob programming

Pair-programmer : travailler à 2 sur une même machine
- le pilote, au clavier, et le copilote, en accompagnement
- rôles tournant tous les 5-10 minutes
- savoir ralentir pour ne pas perdre l'équipier
- rôles complémentaires

Pourquoi binômer :
- apprendre et progresser
- partager et transmettre
- se protéger contre le *bus factor*

Prévoir des temps seul pour traiter ses mails, répondre aux imprévus, se ressourcer

Le mob programming consiste à faire travailler une équipe entière sur une seule tâche sur un seul clavier
- chaque question trouve une réponse immédiate (au lieu de devoir demander à la bonne personne plus tard)
- partage de l'information dans l'équipe
- pratique intéressante pour les tâches sensibles ou difficiles, ou lors de formations et ateliers, également pour aligner les pratiques de code...
- à réaliser idéalement de manière récurente, afin de partager les réalisations récentes, d'avoir une meilleure maitrise de la base de code

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