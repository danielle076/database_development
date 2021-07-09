## Insert 1

Voeg de volgende vijf duiven toe aan je database:

* Bert, NL-21-1234568, doffer, 2021
* Sjaak, NL-21-1234597, duivin, 2021
* Henk, NL-21-1234467, duivin, 2021
* Aart, NL-21-1234367, doffer, 2021
* Mootje, NL-21-1222456, duivin, 2021

Het kan zijn dat jouw tabel (geheel logisch) geen namen van duiven kan opslaan. Deze hoef je dan niet toe te voegen.

** BONUSopdracht: ** Kijk of je via `ALTER TABLE` de tabel zo kan aanpassen dat ook namen opgeslagen kunnen worden.

### Antwoord inclusief bonus

Documentatie en antwoorden:

* https://www.postgresqltutorial.com/postgresql-alter-table/
* https://www.postgresqltutorial.com/postgresql-insert/

```sql
ALTER TABLE pigeon 
ADD COLUMN name varchar(64);

INSERT INTO pigeon (name, ringnumber, sex, birthdate)
VALUES('Bert', 'NL211234568', 'doffer', '2021-01-01');
INSERT INTO pigeon (name, ringnumber, sex, birthdate)
VALUES('Sjaak', 'NL211234597', 'duivin', '2021-01-01');
INSERT INTO pigeon (name, ringnumber, sex, birthdate)
VALUES('Henk', 'NL211234467', 'duivin', '2021-01-01');
INSERT INTO pigeon (name, ringnumber, sex, birthdate)
VALUES('Aart', 'NL211234367', 'doffer', '2021-01-01');
INSERT INTO pigeon (name, ringnumber, sex, birthdate)
VALUES('Mootje', 'NL211222456', 'duivin', '2021-01-01');

```

## Insert 2

Voeg de volgende 10 duiven in 1 query aan je database toe. Dus gebruik maak 1 keer `INSERT INTO`

* Pim, NL-19-1234568, doffer, 2019
* Otis, NL-18-1234597, duivin, 2018
* Rooie, NL-20-1234467, duivin, 2020
* Blauwe, NL-16-1234367, doffer, 2016
* Grijsje, NL-15-1222456, duivin, 2015
* Adelaartje, NL-14-1222456, doffer, 2014
* Witte, NL-12-1222456, duivin, 2012
* Spoetnik, NL-20-1222456, duivin, 2020
* Apollo, NL-18-1222456, doffer, 2018
* Kraai, NL-17-1222456, duivin, 2017

Documentatie en antwoorden:

* https://www.postgresqltutorial.com/postgresql-insert-multiple-rows/

```sql
INSERT INTO pigeon (name, ringnumber, sex, birthdate)
VALUES ('Pim', 'NL191234568', 'doffer', '2019-01-01'),
('Otis', 'NL181234597', 'duivin', '2018-01-01'),
('Rooie', 'NL201234467', 'duivin', '2020-01-01'),
('Blauwe', 'NL161234367', 'doffer', '2016-01-01'),
('Grijsje', 'NL151222456', 'duivin', '2015-01-01'),
('Adelaartje', 'NL141222456', 'doffer', '2014-01-01'),
('Witte', 'NL121222456', 'duivin', '2012-01-01'),
('Spoetnik', 'NL201222456', 'duivin', '2020-01-01'),
('Apollo', 'NL181222456', 'doffer', '2018-01-01'),
('Kraai', 'NL171222456', 'duivin', '2017-01-01');
```

## Insert 3

Voeg de volgende duif toe:
Haasje, NL-20-1222456, doffer, 2020

Welke foutmelding krijg je?

```sql
    INSERT INTO pigeon (name, ringnumber, sex, birthdate)
    VALUES('Haasje', 'NL201222456', 'doffer', '2020-01-01')
```

> ERROR:  duplicate key value violates unique constraint "pigeon_pkey"
> DETAIL:  Key (ringnumber)=(NL201222456) already exists.
> SQL state: 23505

## Insert 4

Als het goed is heb je een CHECK aan je duiven-tabel toegevoegd. Kijkt of die werkt. Voeg de volgende duif toe:
Error, NL-12-1234567, Man, 12

```sql
    INSERT INTO pigeon (name, ringnumber, sex, birthdate)
    VALUES('Error', 'NL121234567', 'Man', '2012-01-01')
```

>ERROR:  new row for relation "pigeon" violates check constraint "pigeon_sex_check"
>DETAIL:  Failing row contains (NL121234567, Man, 2012-01-01, Error).
>SQL state: 23514

## Insert 5

Voeg vijf personen toe aan de lid database. Zorg dat bij 1 persoon het geslacht leeg is.

```sql
INSERT INTO person (firstname, lastname, birthdate, sex, bank_account_number, phone_number, email, member_since, last_paid)
VALUES ('Danielle', 'van den Akker', '1983-06-28', 'f', 'NL91ABNA123456789', '0612345678', 'intoyou@gmail.com', DEFAULT, DEFAULT),
('Freckle', 'Kat', '2019-04-26', 'm', 'NL21RABO123456789', '0623456789', 'freckle@gmail.com', DEFAULT, DEFAULT),
('Frummel', 'Kat', '2021-04-09', 'm', 'NL12INGB123456789', '0698765432', 'frummel@gmail.com', DEFAULT, DEFAULT),
('Martin', 'Boot', '1980-05-20', NULL, 'NL91ABNA987654321', '0619283746', 'martin@gmail.com', DEFAULT, DEFAULT),
('Martini', 'Bellini', '1979-07-10', 'f', 'NL21RABO987654321', '0676543218', 'martini@gmail.com', '2015-01-01', '2021-01-01')
```

## Update 1

* Verander de naam van NL-19-1234568 naar `Pimmetje`
* Verander de naam van Adelaartje naar Adel
* Verander het geboortejaar en het ringnummer van Kraai naar: 2018 en NL-18-1333457
* NL-21-1234367 blijkt een duivin te zijn. Pas dit aan.

```sql
UPDATE pigeon
SET name = 'Pimmetje'
WHERE ringnumber = 'NL191234568';

UPDATE pigeon
SET name = 'Adel'
WHERE name = 'Adelaartje';

UPDATE pigeon
SET birthdate = '2018-01-01' , ringnumber = 'NL181333457'
WHERE ringnumber = 'NL171222456';

UPDATE pigeon
SET sex = 'duivin'
WHERE ringnumber = 'NL211234367';
```

## Delete 1

* Verwijder alle personen die geen geslacht hebben uit de database.
* NL-12-1222456 doet niet meer mee aan wedstrijden. Verwijder deze.

```sql
DELETE FROM person
WHERE sex IS NULL OR sex = '';

DELETE FROM pigeon
WHERE ringnumber = 'NL121222456';
```

## Select 1

Selecteer alle informatie van alle duiven.

```sql
    SELECT *
    FROM pigeon
```

## Select 2

Selecteer alle informatie van alle jonge duiven.

```sql
-- optie 1
SELECT *
FROM pigeon
WHERE birthdate = '2021-01-01';

-- optie 2
SELECT *
FROM pigeon
WHERE EXTRACT(year FROM birthdate) = EXTRACT(year FROM now());

-- optie 3
SELECT *
FROM pigeon
WHERE birthdate >= '2021-01-01' AND birthdate <= '2021-12-31'

-- optie 4
SELECT *
FROM pigeon
WHERE birthdate BETWEEN '2021-01-01' AND '2021-12-31' 
```

## Select 3

Selecteer het geslacht en de ringnummer van alle duiven.

```sql
SELECT sex, ringnumber
FROM pigeon
```

## Select 4

Selecteer de ringsnummer van alle jonge duiven.

```sql
SELECT ringnumber
FROM pigeon
WHERE EXTRACT(year FROM birthdate) = EXTRACT(year FROM now());
```

## Select 5

Selecteer alle ringnummers van alle **niet** jonge duiven.

```sql
SELECT ringnumber
FROM pigeon
WHERE EXTRACT(year FROM birthdate) != EXTRACT(year FROM now());
```

## Delete 2

Verwijder alle data uit de losplaats tabel

```sql
DELETE 
FROM drop_location;
```

## Select 6

Vind een manier om de database het aantal mensen te laten tellen.

```sql
SELECT COUNT(*)
FROM person
```

## Select 7

Selecteer alle leden geboren voor 1970.

```sql
SELECT *
FROM person
WHERE birthdate < '1970-01-01';
```

## Select 8

Selecteer alle leden geboren tussen 1950 en 1960.

```sql
SELECT *
FROM person
WHERE birthdate >= '1950-01-01' AND birthdate < '1961-01-01';

-- optie 2
SELECT *
FROM person
WHERE birthdate BETWEEN '1950-01-01' AND '1960-12-31';
```

## Select 9

Selecteer alle voor- en achternamen en het e-mailadres van de leden waarvan we geen geboortedatum hebben.

```sql
SELECT firstname, lastname, email
FROM person
WHERE birthdate IS NULL;
```

## Select 10

Selecteer de voor- en achternaam en inschrijvingsdatum gesorteerd op inschrijvingsdatum (aflopend).

Documentatie en antwoorden:

* https://www.postgresqltutorial.com/postgresql-order-by/

```sql
SELECT firstname, lastname, member_since
FROM person
ORDER BY member_since DESC;
```

## Select 11

Selecteer de voor- en achternaam en inschrijvingsdatum gesorteerd op inschrijvingsdatum (oplopend).

```sql
SELECT firstname, lastname, member_since
FROM person
ORDER BY member_since;

-- of (ASC is default value, dus dit hoeft niet)

SELECT firstname, lastname, member_since
FROM person
ORDER BY member_since ASC;
```

## Select 12

Selecteer de voornaam en het e-mailadres van het langst ingeschreven vrouwelijke lid.

Documentatie en antwoorden:

* https://www.postgresqltutorial.com/postgresql-limit/

```sql
SELECT firstname, lastname, email
FROM person
WHERE sex = 'f'
ORDER BY member_since
LIMIT 1;
```

## Select 13

Selecteer alle duivennamen die met Ap beginnen. (Mocht je geen duivennamen bijhouden, doe het dan op de leden tabel).

Documentatie en antwoorden:

* https://www.postgresqltutorial.com/postgresql-like/

```SQL
SELECT name
FROM pigeon
WHERE name LIKE 'Ap%'
```

## Select 14

Tel het aantal doffers in de database.

Documentatie en antwoorden:

* https://www.w3schools.com/sql/sql_count_avg_sum.asp

```sql
SELECT COUNT(*)
FROM pigeon
WHERE sex = 'doffer';
```

## Select 15

Selecteer het ringnummer van de vijf oudste duivinnen.

```sql
SELECT ringnumber
FROM pigeon
WHERE sex = 'duivin'
ORDER BY birthdate, ringnumber --ringnumber is een toevoeging, wanneer de date gelijk is, kijken we daarna naar het ringnumber.
LIMIT 5;
```

## Extra

Zoek uit hoe je een gehele tabel kunt verwijderen.

```sql
DROP TABLE IF EXISTS drop_location 
CASCADE;
```
