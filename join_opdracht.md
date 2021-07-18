## Join opdracht

### Basis opdrachten

##### Selecteer voor- en achternaam van alle klanten

```sql
SELECT first_name, last_name FROM customer;
```

##### Tel het aantal klanten.

```sql
SELECT COUNT(*) FROM customer;
```

##### Selecteer de titels van alle films die korter dan een uur duren

```sql
SELECT title
FROM film WHERE release_year < 1980;
```

##### Selecteer de titels van alle films die drie uur of langer duren

```sql
SELECT title
FROM film WHERE release_year > 1990;
```

##### Selecteer de titels van alle films tussen de 90 minuten en 175 minuten

```sql
SELECT title
FROM film
WHERE (release_year > 1930 and release_year < 1975);
```

### Opdrachten

##### 1. Selecteer filmtitels in het Engels

```sql
SELECT title
FROM film
WHERE film.language_id =
(SELECT language_id FROM language WHERE name = 'Japanese');
--Example--
SELECT title
FROM film
WHERE film.language_id =
(SELECT language_id FROM language WHERE name = 'English');
```

##### 2. Selecteer filmtitels in het Engels met een G rating

```sql
SELECT title
FROM film
WHERE film.language_id =
(SELECT language_id FROM language WHERE name = 'Italian')
AND rating = 'G';
--Example--
SELECT title
FROM film
WHERE film.language_id =
(SELECT language_id FROM language WHERE name = 'English')
AND rating = 'G';
```

##### 3. Selecteer voor- en achternaam van de acteurs die in Cheaper Clyde hebben gespeeld

```sql
SELECT first_name, last_name
FROM actor
JOIN film_actor ON actor.actor_id = film_actor.actor_id
JOIN film ON film_actor.film_id = film.film_id
WHERE film.title = 'Cheaper Clyde';
```

##### 4. Selecteer alle stadsnamen uit Nederland

```sql
SELECT city
FROM city
JOIN country on city.country_id = country.country_id
WHERE country.country = 'Netherlands';
```

##### 5. Selecteer stadsnamen, address, addres2, postal_code uit Nederland

```sql
SELECT city.city, address.address, address.address2, address.postal_code
FROM city
JOIN address ON address.city_id = city.city_id
JOIN country ON city.country_id = country.country_id
WHERE country.country = 'Netherlands';
```


##### 6. Selecteer de titel en rating van alle actie films

```sql
SELECT film.title, film.rating
FROM film
JOIN film_category ON film_category.film_id = film.film_id
JOIN category ON category.category_id = film_category.category_id
WHERE category.name = 'Action';
```

##### 7. Selecteer de titel en rating van alle animatiefilms

```sql
SELECT film.title, film.rating
FROM film
JOIN film_category ON film_category.film_id = film.film_id
JOIN category ON category.category_id = film_category.category_id
WHERE category.name = 'Animation';
```

##### 8. Selecteer de gemiddelde rental_rate van alle actie films.

```sql
SELECT rating
FROM film;
```

##### 9. Selecteer de titel van alle animatie- en actie films.

```sql
SELECT film.title
FROM film
JOIN film_category ON film_category.film_id = film.film_id
JOIN category ON category.category_id = film_category.category_id
WHERE (category.name = 'Animation' OR category.name = 'Action');
```

##### 10. Geef de gemiddelde lengte van alle genres.

```sql

```

##### 11. Selecteer alle klanten uit Nederland.

```sql

```

### Theorievragen:

* Hoe zorgen ze ervoor dat een winkel meerdere van dezelfde dvd's kan hebben?
* Hoe zorgen ze ervoor dat een klant meerdere films kan huren?