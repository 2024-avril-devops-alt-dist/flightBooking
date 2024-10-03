# Flight Booking

## Description
Ce projet a pour but de définir les structures de données à utiliser dans le cadre d'une application destiné à gérer des réservations sur des vols d'avion.

## Livrables
### Pour la base de données
* [MCD au format PNG](https://drive.google.com/file/d/1dEjmkWkkjPoFVSwOchUbgsYGxg65SRLw/view?usp=sharing) ou [au format PDF](https://drive.google.com/file/d/1FqpRxlomF0e2ASoh0Qn4uu3NWIkSYetJ/view?usp=sharing)
* [MLD au format PDF](https://drive.google.com/file/d/180-tnOmjxW38nAaC7QLOAdXV-9svjUpw/view?usp=sharing)
* [MPD au format PNG](https://drive.google.com/file/d/1--IJgYNdBA8Fu7us8tI2SJJibO8kYWBL/view?usp=sharing) ou [au format PDF](https://drive.google.com/file/d/11Wmd82lZnkxY0432BtZUCC3Qa3gTV37S/view?usp=sharing)

### Pour l'application
* [dictionnaire de données au format PDF](https://drive.google.com/file/d/1Pjq2oXuCH86dFvuWeNm_tKm0URHm1oFg/view?usp=sharing)
* diagramme de classe
* diagramme de séquence
* [script SQL de création de base de données](https://drive.google.com/file/d/1MEStdiOBk8DDnlwJei7s9uGAfYrvNfEz/view?usp=sharing)

## Précisions sur les livrables
### MCD
J'ai choisi une approche considérant que les personnes réglant financièrement la réservation et les passagers avaient de nombreux points communs, et étaient tous deux qualifiés de "clients" par la compagnie aérienne. Les entités Buyer et Passenger héritent donc de Client, ne gardant comme attributs que ceux qui leur sont spécifiques.

#### Attributs
* L'attribut passenger_specifics sert à stocker toute information spécifique importante concernant un passager (intolérances alimentaires par exemple).
* L'attribut "rank" de la relation "Stopover at" indique l'ordre des escales éventuelles.
  
#### Cardinalités
* La relation "Booking" indique une cardinalité (0,n) sur Flight, car un vol peut exister sans avoir encore de réservations.\
* La relation "Is a" indique une cardinalité (0,1) car un client peut être ou pas un passager, et peut être ou pas un acheteur. Et ce, même s'il doit nécessairement être au moins un des deux pour avoir une relation avec le système.
* La relation "Is a national from" indique une cardinalité (0,n) sur Country, car un pays peut exister et n'avoir aucun passager qui en soit un ressortissant.
* La relation "Is located in" indique une cardinalité (1,n) sur Country, car un pays peut exister via la relation "Is a national from", sans pour autant qu'on n'ait jamais créé de villes associées. Même principe pour "Is located in" et "Lives in" : l'existence de plusieurs relations vers l'entité City n'implique pas nécessairement que chacune d'entre elles comprenne au moins une valeur.

### MLD
Les clés primaires ont été soulignées, et les clés étrangères préfixées par un symbole dièse.

### MPD
J'ai fait mon possible pour éviter les croisements sur le schema, sans avoir totalement réussi néanmoins.

### Dictionnaire de données
* Les tailles de données indiquées pour les entiers sont plus des rappels aux tailles standards d'entiers sous MySql.
* Les champs "real_..._datetime" sont potenitellement  nuls car ils correspondent à des horaires constatés, qui nécessitent donc l'existence de l'événement correspondant.
* Les champs "..._created_at" et "..._updated_at" ont été ajoutés à toutes les tables afin d'assurer un meilleur suivi de la donnée.

### Diagramme de classe

### Diagramme de séquence

### Script SQL de création de base de données
Le script correspond à une base de données MySql/MariaDB, avec toutes les clés étrangères définies. Les triggers ON DELETE sont sur "RESTRICT" par défaut. On pourrait envisager de les mettre sur "CASCADE", mais toute suppression de données parent (en particulier les données géographiques) pourrait alors avoir de lourdes conséquences sur les données liées (ex. : la suppression d'une ville supprimerait en cascade tous les clients et aéroports qui y sont connectés). Une historisation des données est à prévoir pour toute fonction de suppression.
