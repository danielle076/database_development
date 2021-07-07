## Database

Maak een nieuwe database aan in `pgAdmin` en noem deze `postduif`.

## Maak de tabel duif

De tabel `duif` moet de volgende gegevens bevatten:

* ringnummer
* geslacht
* geboortedatum

Houd rekening met de volgende punten:

1. Verzin zelf de datatypes.
1. Geen enkel veld mag leeg zijn.
1. Geboortedatum mag ook jaar zijn.
1. Kun je een check maken voor geslacht? Hier mag alleen `doffer` of `duivin` ingevoerd worden.
1. Het ringnummer bestaat altijd uit een x aantal tekens. Dwing dit af.
1. Alle tabel- en kolomnamen moeten in het **engels**.
1. Is geboortedatum echt nodig?

### Oplossing

```sql
-- We zorgen er eerst voor dat de tabel wordt verwijderd, mocht die bestaan.
DROP TABLE if exists pigeon CASCADE;

CREATE TABLE pigeon (
   ringnumber VARCHAR(11) PRIMARY KEY,
   sex varchar(6) CHECK (sex = 'doffer' OR sex = 'duivin') NOT NULL,
   birthdate date NOT NULL
);

-- De geboortedatum is niet per se nodig, want het geboortejaar is onderdeel van het ringnummer.
```

## Maak de tabel lid

De tabel `lid` moet de volgende gegevens kunnen bijhouden:

1. De geboortedatum van de persoon.
1. De voornaam van de persoon.
1. De achternaam van de persoon.
1. Het geslacht van de persoon.
1. Het rekeningnummer van de persoon.
1. Het telefoonnummer van de persoon.
1. Het e-mailadres van de persoon.
1. Sinds wanneer lid.
1. Datum laatste betaling contributie.

Paar dingen om op te letten:

* Is er al data in de tabel aanwezig die als Primary Key kan dienen en die je ook zou willen gebruiken om iemand te
  identificeren?
* Welke kolommen kunnen uniek gemaakt worden? Houd hierbij rekening met:
    * Leden kunnen op hetzelfde adres wonen.
    * Ieder lid moet een eigen e-mailadres opgeven.
* De volgende data is niet verplicht: geslacht, rekeningnummer en geboortedatum.
* Bij inschrijving betaalt het lid altijd direct zijn contributie.
* Kun je een DEFAULT waarde aan `datum laatste betaling contributie` en `lid sinds` geven. De default-waarde is dan de dag van invoer.
* Alle tabel- en kolomnamen moeten in het **engels**.

### Oplossing

```sql
DROP TABLE if exists person CASCADE;

CREATE TABLE person (
    id INT GENERATED ALWAYS AS IDENTITY,
    firstname varchar(64) NOT NULL,
    lastname varchar(64) NOT NULL,
    birthdate date,
    sex char(1) check(sex = 'f' OR sex = 'm'),
    bank_account_number varchar(64),
    phone_number varchar(10) NOT NULL, 
    email varchar(64) UNIQUE NOT NULL, 
    member_since date DEFAULT CURRENT_DATE, -- CURRENT_DATE is een manier om de huidige datum te krijgen.
    last_paid date DEFAULT now() -- now() is een manier om de huidige datum te krijgen.
);
```
## Maak de tabel losplaats

De tabel `losplaats` bevat minimaal de volgende gegevens:

* Een x coördinaat.
* Een y coördinaat.
* Een plaatsnaam.

Verzin zelf welke *constraints* voor deze tabel moeten gelden.

### Oplossing

```sql
DROP TABLE if exists drop_location CASCADE;

CREATE TABLE drop_location (
   latitude NUMERIC(9,6) NOT NULL,
   longitude NUMERIC(9,6) NOT NULL, 
   city VARCHAR(32) NOT NULL,
   PRIMARY KEY (latitude, longitude)
);
```

In bovenstaand voorbeeld worden het X en Y coördinaten SAMEN als PRIMARY KEY geconfigureerd.