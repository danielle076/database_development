## Foreign key

Zelf een foreign key maken wordt uitgelegd met onderstaand voorbeeld.

We maken een standaard tabel. Deze tabel company gaat een 1 of meer relatie hebben met press_officer.

```sql
CREATE TABLE company (
    id INT GENERATED ALWAYS AS IDENTITY,
    name VARCHAR(255) NOT NULL,
    PRIMARY KEY(id)
);
```

Table company heeft een eigen id `id INT GENERATED ALWAYS AS IDENTITY`. De primary key verwijst naar de id.

```sql
CREATE TABLE press_officer(
    id INT GENERATED ALWAYS AS IDENTITY,
    company_id INT,
    full_name VARCHAR(255) NOT NULL,
    phone VARCHAR(15),
    email VARCHAR(100),
    PRIMARY KEY(id),
    CONSTRAINT fk_company
        FOREIGN KEY(company_id)
            REFERENCES company(id)
);
```

Table press_officer heeft ook een eigen id `id INT GENERATED ALWAYS AS IDENTITY` en primary key.

Daarnaast heeft hij ook een company_id `company_id INT` kolom. De dataype van deze id is een INT. Foreign key qua datatype moet altijd precies overeenkomen als de datatype uit de tabel waar hij naar verwijst.

Vervolgens gaan we een constraint maken. Een constraint is een beperkings regel die je kan opleggen. Deze constraint gaan we een naam geven: `fk_company.`. Dan zeggen we op welke kolom de foreign key van toepassing is `FOREIGN KEY(company_id)`. En dan naar welke tabel we moeten gaan en welke kolom we uit de tabel moeten hebben `REFERENCES company(id)`. Company is dan de tabel en id is de kolom uit de tabel company.

