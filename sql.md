## SQL

### Tabellen

De data moet ergens in worden opgeslagen en dat moet gestructureerd: in een tabel.

- Een tabel bestaat uit rijen en kolommen.
- Een database heeft vaak meerdere tabellen.
- Elke kolom heeft een datatype.
- Elke rij is een opgeslagen entiteit. Bijv. elke persoon die je opslaat in een persoon tabel noem je een entiteit. Een entiteit is wanneer je het vertaald naar Java hetzelfde als een object.

### Een tabel maken

```sql
CREATE TABLE IF NOT EXISTS table_name (
    column1 datatype(length) column_constraint,
    column2 datatype(length) column_constraint,
    column3 datatype(length) column_constraint,
    table_constraints
);
```

- Je begint altijd eerst met `CREATE TABLE`.
  
- `IF NOT EXISTS` is optioneel. Hiermee check je of de tabel al bestaat. Wanneer de tabel al bestaat, dan doet hij voor de rest niks (geeft een melding dat hij al bestaat). Waarom doe je dit: wanneer je een tabel wilt maken en deze bestaat al dan werkt SQL zo dat hij soort van crasht, hij stopt met het uitvoeren van je SQL script en zet alles weer terug naar het begin. Je doet of de hele transactie, of je doet helemaal niks.

- Je geeft de tabel een naam bij `table_name`.

- Vervolgens doe je per column de column naam: `column1`, `column2` etc.
- Dan het `datatype(length)`
- Je kan er constraints (beperkingen) opzetten. Constraints kun je op twee niveaus doen, column `column_constraint` en table `table_constraints`.

### Datatypen

- Numeric (getallen)
    - Integers
        - SMALLINT
        - INT
        - SERIAL (oplopend getal)
    - Floating-point
        - float(n)
        - real/float8
        - numeric(p,s)

- Character (staat tussen aanhaaltekens)
    - CHAR(n) ("n" betekend hoeveel tekens)
    - VARCHAR(n) (bijv. iemands achternaam opslaan)
    - TEXT

- Datum (staat tussen aanhaaltekens)
    - DATE (jaar-maand-dag 2021-07-07)
    - TIME
    - TIMESTAMP
    - INTERVAL

Ze voor meer informatie over datatypen: https://www.postgresqltutorial.com/postgresql-data-types/

### Constraints

Constraints zijn beperkingen die je aan je data kunt toevoegen. Beperkingen zijn dingen waar je data aan moet voldoen en anders wordt het niet opgeslagen in de database. Je doet dit op kolom-niveau of tabel-niveau in SQL.

- NOT NULL
- CHECK
- UNIQUE
- PRIMARY KEY

#### Voorbeeld NOT NULL

Als we iets willen toevoegen aan de tabel, dan mag de column nooit een lege waarde hebben.

```sql
CREATE TABLE orders (
    ord_no integer NOT NULL,
    ord_date date NOT NULL,
    item_name character(35),
    item_grade character(1),
    ord_qty numeric NOT NULL,
    ord_amount numeric
);
```

In dit voorbeeld mogen `ord_no`, `ord_date` en `ord_qty` nooit null zijn, er moet een waarde aan gegeven worden. 

Dus als je iets wilt opslaan in een database dat een waarde moet hebben zet je hem op `NOT NULL`.

#### Voorbeeld CHECK

Je kan een check doen dat de order amount altijd groter moet zijn dan 0 met `ord_amount>0`. 

Deze constraint is postgreSQL specifiek.

```sql
CREATE TABLE orders (
    ord_no integer,
    ord_date date,
    item_name character(35),
    item_grade character(1),
    ord_qty numeric,
    ord_amount numeric CHECK (ord_amount>0)
);
```

#### Voorbeeld UNIQUE

Een waarde in een column mag maar één keer voorkomen, over alle entiteiten in de tabel.

Bijvoorbeeld als iemand zich registreert op een website met zijn e-mail adres da mag dat e-mail adres maar één keer voorkomen. Dan zeg je dat e-mailadres unique moet zijn.

```sql
CREATE TABLE orders (
    ord_no integer UNIQUE,
    ord_date date,
    item_name character(35),
    item_grade character(1),
    ord_qty numeric,
    ord_amount numeric
);
```

In dit voorbeeld is `ord_no` unique.

#### Voorbeeld PRIMARY KEY

Een primary key is altijd uniek.

Een primary key gebruiken we om een entiteit te identificeren. Bijvoorbeeld een BSN.

```sql
CREATE TABLE orders (
    ord_no integer,
    ord_date date,
    item_name character(35),
    item_grade character(1),
    ord_qty numeric,
    ord_amount numeric,
    PRIMARY KEY (ord_no,item_name)
);
```

##### PRIMARY KEY vs UNIQUE

Primary Key
- Wordt gebruikt om een rij of entiteit te identificeren
- Maximaal 1 PK
- Kan niet NULL zijn
- Wordt vaak geïndexeerd op volgorde. Data wordt sneller opgezocht in de database

Unique
- Wordt gebruikt om de waarde van een kolom naast de PK uniek te laten zijn
- Meerdere mogelijk
- Kan NULL zijn
- Niet op volgorde. Langzamer om te vinden