_In English_

# Flight Booking

## Description
This project aims to define the data structures to be used within the framework of an application intended to manage reservations on airline flights. The chosen structures correspond to terrestrial issues, but could be adapted to intergalactic travel with some modifications, particularly concerning geographical notions.

## Deliverables
### Concerning database
* [MCD, in PNG format](https://drive.google.com/file/d/1dEjmkWkkjPoFVSwOchUbgsYGxg65SRLw/view?usp=sharing)
* [MLD, in PDF format](https://drive.google.com/file/d/180-tnOmjxW38nAaC7QLOAdXV-9svjUpw/view?usp=sharing)
* [MPD, in PNG format](https://drive.google.com/file/d/1--IJgYNdBA8Fu7us8tI2SJJibO8kYWBL/view?usp=sharing)

### Concerning the application
* [data dictionary, in PDF format](https://drive.google.com/file/d/1Pjq2oXuCH86dFvuWeNm_tKm0URHm1oFg/view?usp=sharing)
* [UML class diagram, in PNG format](https://drive.google.com/file/d/1BpyB5YXJ7pXFxBT7-zEBay2pWu_nOumo/view?usp=sharing)
* [UML sequence diagram, in PNG format](https://drive.google.com/file/d/1ogwjD8TY8woMfl3KGJywGNskC6NuiRvB/view?usp=sharing), describing a totally successful booking procedure
* [SQL script for database structure creation](https://drive.google.com/file/d/1MEStdiOBk8DDnlwJei7s9uGAfYrvNfEz/view?usp=sharing), for a MySQL/MariaDB database

## Details on deliverables
### CDM
I chose an approach considering that the people paying for the reservation and the passengers had many attributes in common, and were both qualified as "clients" by the airline. The Buyer and Passenger entities therefore inherit from Customer, keeping only those attributes that are specific to them.

#### Attributes
* The "passenger_specifics" attribute is used to store any important specific information concerning a passenger (food intolerances for example).
* The "rank" attribute of the "Stopover at" relationship indicates the order of potential stopovers.
* The "city_gmt_offset" attribute allows you to store the time difference between a given city and the Greenwich meridian, in particular to avoid any time confusion.
  
#### Cardinalities
* The "Booking" relationship indicates cardinality (0,n) on Flight, because a flight can exist without having any reservations yet, typically when the flight was not yet opened to booking.
* The relationship "Is a" indicates cardinality (0,1) because a client may or may not be a passenger, and may or may not be a buyer. And this, even if he/she must necessarily be at least one of the two to have a relationship with the system.
* The relationship "Is a national from" indicates a cardinality (0,n) on Country, because a country can exist and have no passengers who are nationals of it. Example: country containing an airport, but no nationals from this country where ever passengers.
* The relationship "Is located in" indicates a cardinality (1,n) on Country, because a country can exist via the relationship "Is a national from", without ever having created associated cities. Same principle for "Is located in" and "Lives in": the existence of several relationships to the City entity does not necessarily imply that each of them includes at least one value.

### LDM
Primary keys have been underlined, and foreign keys prefixed with a dash symbol.

### PDM
I did my best to avoid crossings on the diagram, without having completely succeeded, however.

### Data dictionary
* The data sizes shown for integers are more reminders of standard integer sizes under MySql.
* The "real_..._datetime" fields are potentially null because they correspond to observed times, which therefore require the existence of the corresponding event.
* The "..._created_at" and "..._updated_at" fields have been added to all tables to ensure better data tracking.

### Class diagram
I'm quite perplexed about this schema, in which I have difficulty assigning actions to the different entities involved. Example: the creation of a flight is initiated by the associated company, but must logically be managed internally by the object concerned.

### Diagramme de séquence
I tried to indicate the data flow between actors in a fully successful booking process.

### Databse creation SQL script
The script corresponds to a MySql/MariaDB database, with all foreign keys defined. ON DELETE triggers are “RESTRICT” by default. We could consider putting them on "CASCADE", but any deletion of parent data (in particular geographic data) could then have serious consequences on the linked data (e.g.: deleting a city would cascade delete all clients and airports connected to it). Data logging is required for any deletion function.
I chose utf8mb4 storage in order to minimize possible problems linked to international data (diacritic and sorting in particular).

---

_In French_

# Flight Booking

## Description
Ce projet a pour but de définir les structures de données à utiliser dans le cadre d'une application destiné à gérer des réservations sur des vols d'avion. Les structures choisies correspondent à des problématiques terrestres, mais pourraient être adaptées aux voyages intergalactiques moyennant quelques modifications, notamment concernant les notions géographiques.

## Livrables
### Pour la base de données
* [MCD, au format PNG](https://drive.google.com/file/d/1dEjmkWkkjPoFVSwOchUbgsYGxg65SRLw/view?usp=sharing)
* [MLD, au format PDF](https://drive.google.com/file/d/180-tnOmjxW38nAaC7QLOAdXV-9svjUpw/view?usp=sharing)
* [MPD, au format PNG](https://drive.google.com/file/d/1--IJgYNdBA8Fu7us8tI2SJJibO8kYWBL/view?usp=sharing)

### Pour l'application
* [dictionnaire de données, au format PDF](https://drive.google.com/file/d/1Pjq2oXuCH86dFvuWeNm_tKm0URHm1oFg/view?usp=sharing)
* [diagramme de classe UML, au format PNG](https://drive.google.com/file/d/1BpyB5YXJ7pXFxBT7-zEBay2pWu_nOumo/view?usp=sharing)
* [diagramme de séquence UML, au format PNG](https://drive.google.com/file/d/1ogwjD8TY8woMfl3KGJywGNskC6NuiRvB/view?usp=sharing), describing a totally successful booking procedure
* [SQL script for database structure creation](https://drive.google.com/file/d/1MEStdiOBk8DDnlwJei7s9uGAfYrvNfEz/view?usp=sharing), for a MySQL/MariaDB database

## Précisions sur les livrables
### MCD
J'ai choisi une approche considérant que les personnes réglant financièrement la réservation et les passagers avaient de nombreux points communs, et étaient tous deux qualifiés de "clients" par la compagnie aérienne. Les entités Buyer et Passenger héritent donc de Client, ne gardant comme attributs que ceux qui leur sont spécifiques.

#### Attributs
* L'attribut "passenger_specifics" sert à stocker toute information spécifique importante concernant un passager (intolérances alimentaires par exemple).
* L'attribut "rank" de la relation "Stopover at" indique l'ordre des escales éventuelles.
* L'attribut "city_gmt_offset" permet de stocker le décalage horaire entre une ville donnée et le méridien de Greenwich, notamment pour éviter toute confusion horaire.
  
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
Je reste perplexe concernant ce schema, pour lequel j'ai du mal à assigner les actions aux différentes entités impliquées. Exemple : la création d'un vol est déclenchée par la compagnie associée, mais doit logiquement être gérée en interne par l'objet concerné.

### Diagramme de séquence
J'ai cherché à modéliser le flux de données entre les différents acteurs dans un process de réservation sans erreurs.

### Script SQL de création de base de données
Le script correspond à une base de données MySql/MariaDB, avec toutes les clés étrangères définies. Les triggers ON DELETE sont sur "RESTRICT" par défaut. On pourrait envisager de les mettre sur "CASCADE", mais toute suppression de données parent (en particulier les données géographiques) pourrait alors avoir de lourdes conséquences sur les données liées (ex. : la suppression d'une ville supprimerait en cascade tous les clients et aéroports qui y sont connectés). Une historisation des données est à prévoir pour toute fonction de suppression.\
J'ai choisi le stockage utf8mb4 afin de minimiser les problématiques éventuelles liées aux données internationales (diacritiques et tri notamment).
