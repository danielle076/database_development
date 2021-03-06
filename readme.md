## Werken met een Database

Een database is een medium om data in op te slaan. We focussen ons op het gebruik van <u>relationele databases</u>: een database waar relaties tussen data in het model worden gedefinieerd.

Meer informatie over databases vind je [hier](database.md). 

### DBMS

Een databasemanagementsysteem (DBMS) is software voor het opslaan en verkrijgen van data, waar het in acht nemen van verschillende beveiligingskwesties mogelijk zijn.

We hebben een aantal spelers op de markt:
- MySQL
- Oracle Database
- SQLServer
- PostgreSQL

Wij werken met PostgreSQL. Klik [hier](postgresql.md) voor meer informatie.

### SQL

SQL (Structured Query Language) is een Data Manipulation Language. Het is een specifieke programmeertaal die is ontworpen voor specifieke databases. Je doet er twee dingen mee.
1. je creëert tabellen in je database 
2. je voert data in, update data, leest data en verwijdert de data (CRUD).

[Hier](sql.md) kun je meer informatie vinden over SQL.

### Tabel oefening

Ga [hier](create_opdracht.md) oefenen met tabellen aanmaken.

### CRUD

Create, Read, Update en Delete (CRUD) zijn de vier basisfuncties die databases moeten kunnen uitvoeren.

- Create (of insert): Toevoegen van nieuwe gegevens.
- Read (of select): Opvragen van gegevens.
- Update: Wijzigen van gegevens.
- Delete: Verwijderen van gegevens.

Hoe je deze kunt toepassen in postgreSQL lees je [hier](crud.md).

### CRUD oefening

[Deze](crud_opdracht.md) opgaven zijn een vervolg op de tabel oefening.

### Relaties

Lees [hier](relaties.md) meer over relaties.

### UML & Tabel

Het toepassen van relaties in databases lees je [hier](uml_tabel.md).

### Add foreign key opdracht

Naar aanleiding van de informatie uit UML en tabel zijn er [hier](fk_opdracht.md) oefeningen.

### Foreign key in SQL

Hoe je foreign key in SQL kunt toepassen lees je [hier](foreign_key.md).

### Constraints

Constraints zijn beperkingen die je aan je data kunt toevoegen. Dit
doe je op kolom-niveau of tabel-niveau in SQL. [Hier](constraints.md) kun je daar meer over lezen.

### Select met JOIN

Data uit verschillende tabellen combineren doe je met [join](join.md).

### JOIN oefening

We gaan een .tar bestand importeren in pgAdmin.

1. maak een database
2. rechts klikken op de database > Restore
3. bij filename ga je het .tar bestand zoeken en selecteren
4. role name wordt postgres
5. klik op button Restore

Het bestand dat we hebben geïmporteerd heet `dvdrental.tar` en de opdrachten die we maken met deze database staan [hier](join_opdracht.md).
