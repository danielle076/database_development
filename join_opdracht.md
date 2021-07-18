## Join opdracht

### Basis opdrachten

##### Selecteer voor- en achternaam van alle klanten

```sql
SELECT first_name, last_name 
FROM customer;
```

##### Tel het aantal klanten

```sql
SELECT COUNT(*) 
FROM customer;
```

##### Selecteer de titels van alle films die korter dan een uur duren

```sql
SELECT title
FROM film 
WHERE length < 60;
```

##### Selecteer de titels van alle films die drie uur of langer duren

```sql
SELECT title, length
FROM film
WHERE length >= 180;
```

##### Selecteer de titels van alle films tussen de 90 minuten en 175 minuten

```sql
SELECT title, length
FROM film
WHERE (length >= 90 AND length <= 175);
```

### Opdrachten

Je kan de kolommen onder tables > category > columns bekijken, maar overzichtelijker is wanneer je het volgende doet.

```sql
SELECT * FROM actor;
SELECT * FROM address;
SELECT * FROM category;
SELECT * FROM city;
SELECT * FROM country;
SELECT * FROM customer;
SELECT * FROM film;
SELECT * FROM film_actor;
SELECT * FROM film_category;
SELECT * FROM inventory;
SELECT * FROM language;
SELECT * FROM payment;
SELECT * FROM rental;
SELECT * FROM staff;
SELECT * FROM store;
```

##### 1. Selecteer filmtitels in het Engels

```sql
SELECT title, language_id
FROM film
WHERE film.language_id =
(SELECT language_id FROM language WHERE name = 'English');
```

##### 2. Selecteer filmtitels in het Engels met een G rating

```sql
SELECT title, rating
FROM film
WHERE film.language_id =
(SELECT language_id FROM language WHERE name = 'English')
AND rating = 'G';
```

##### 3. Selecteer voor- en achternaam van de acteurs die in Cheaper Clyde hebben gespeeld

```sql
SELECT first_name, last_name, film.title
FROM actor
JOIN film_actor ON actor.actor_id = film_actor.actor_id
JOIN film ON film_actor.film_id = film.film_id
WHERE film.title = 'Cheaper Clyde';
```

Denkwijze: je wilt actor en film joinen waar actor_id is gelijk aan actor_id in film. Maar in film tabel hebben we geen actor_id, we hebben een koppel tabel waar we de combinatie in opnemen van film_id en actor_id. We doen dus 3 joins: op actor, film en op filmactor.

##### 4. Selecteer alle stadsnamen uit Nederland

```sql
SELECT city, country
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
SELECT film.title, film.rating, category.name
FROM film
JOIN film_category ON film_category.film_id = film.film_id
JOIN category ON category.category_id = film_category.category_id
WHERE category.name = 'Action';
```

##### 7. Selecteer de titel en rating van alle animatiefilms

```sql
SELECT film.title, film.rating, category.name
FROM film
JOIN film_category ON film_category.film_id = film.film_id
JOIN category ON category.category_id = film_category.category_id
WHERE category.name = 'Animation';
```

##### 8. Selecteer de gemiddelde rental_rate van alle actie films

```sql
SELECT AVG(rental_rate)
FROM film
JOIN film_category ON film_category.film_id = film.film_id
JOIN category ON category.category_id = film_category.category_id
WHERE category.name = 'Action';
```

##### 9. Selecteer de titel van alle animatie- en actie films

```sql
SELECT film.title, category.name
FROM film
JOIN film_category ON film_category.film_id = film.film_id
JOIN category ON category.category_id = film_category.category_id
WHERE (category.name = 'Animation' OR category.name = 'Action');
```

##### 10. Geef de gemiddelde lengte van alle genres

```sql
SELECT category.name, AVG(film.length) 
FROM film
JOIN film_category ON film.film_id = film_category.film_id
JOIN category ON category.category_id = film_category.category_id
GROUP BY category.name;
```

##### 11. Selecteer alle klanten uit Nederland

```sql
SELECT customer.last_name, country.country 
FROM customer
JOIN address ON customer.address_id = address.address_id
JOIN city ON address.city_id = city.city_id
JOIN country ON country.country_id = city.country_id 
WHERE country.country = 'Netherlands';
```