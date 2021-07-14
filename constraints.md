## Constraints

Je hebt de volgende constraints:

- NOT NULL
- CHECK
- UNIQUE
- PRIMARY KEY
- FOREIGN KEY

Je moet rekening houden met wat er moet gebeuren wanneer data met een relatie verwijderd wordt.

- RESTRICT
- NO ACTION
- SET NULL
- SET DEFAULT
- CASCADE

### Constraints - NO ACTION & RESTRICT (1)

Dit is de default waarde. Je kunt geen data verwijderen zolang er een relatie is.

```sql
CREATE TABLE press_officer (
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

### Constraints - NO ACTION & RESTRICT (2)

Je kunt de default waarde ook uitgeschreven.

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
            ON DELETE NO ACTION
);
```

### Constraints - NO ACTION & RESTRICT (3)

NO ACTION en RESTRICT hebben soortgelijk gedrag.

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
            ON DELETE RESTRICT
);
```

### Constraints - NO ACTION & RESTRICT (4)

![img_24.png](pictures/img_24.png)

### Constraints - SET NULL

De waarde van de foreign key wordt op NULL gezet.

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
            ON DELETE SET NULL
);
```

### Constraints - SET DEFAULT

Zet de waarde van de foreign-key naar een ingestelde default waarde.

```sql
CREATE TABLE press_officer(
    id INT GENERATED ALWAYS AS IDENTITY,
    company_id INT,
    -- overige weggelaten.
    PRIMARY KEY(id),
    CONSTRAINT fk_company
        FOREIGN KEY(company_id)
            REFERENCES company(id)
            ON DELETE SET DEFAULT
);
```

### Constraints - CASCADE

Deze is belangrijk! Wanneer je een rij uit de hoofdtabel verwijderd, worden alle relaties ook verwijderd!

```sql
CREATE TABLE press_officer(
    id INT GENERATED ALWAYS AS IDENTITY,
    company_id INT,
    -- overige weggelaten.
    PRIMARY KEY(id),
    CONSTRAINT fk_company
        FOREIGN KEY(company_id)
            REFERENCES company(id)
            ON DELETE CASCADE
);
```

### Alter table

```sql
ALTER TABLE child_table
    ADD CONSTRAINT constraint_name
    FOREIGN KEY (fk_columns)
    REFERENCES parent_table (parent_key_colWumns);
```