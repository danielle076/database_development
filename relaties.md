## Relaties

### Relaties in Java

In Java heb je twee soorten relaties:

- Has-a, bijvoorbeeld een klant heeft een adres, een liefhebber heeft een duif
- Is-a, bijvoorbeeld een hond is een dier, een auto is een vehicle (vaak overerving van abstracte klasses of interface)

_Voorbeeld 1 tot 1 - Java_

Stel je hebt een klasse `Person` en die heeft een adres en dat adres moet hij hebben als je hem aanmaakt. Als variabele zet je `private Address address` en bij de constructor geef je specifiek het adres mee tussen `()`. Je dwingt dus af dat Person alleen aangemaakt worden met dat adres.

```java
public class Person {
    private Address address;
    
    public Person(Address address) {
        this.address = address;
    }
    // Getters & Setters weggelaten
}
```

_Voorbeeld 1 tot n_

Dit is een relatie 1 of meer. Een `Company` kan 1 of meerdere werknemers hebben. Dit houd je bij in een `List<Person>`. Op het moment dat een Company aangemaakt wordt, wordt een lijst met employees aangemaakt: `public Company(List<Person> employees)` en opgeslagen in `private List<Person> employees;`. Met de `addEmployee` kun je employees 1 voor 1 toevoegen.

```java
public class Company {
    private List<Person> employees;
    
    public Company(List<Person> employees) {
        this.employees = employees;
    }
    public void addEmployee(Person employee) {
        employees.add(employee);
    }
}
```

_Voorbeeld n tot n_

De meer tot meer relatie. In Java is dit heel raar, dus gaan we niet te diep op in. In dit voorbeeld kan een `Person` voor een `Company` werken, maar dit kunnen 1 of meerdere bedrijven zijn. En een bedrijf heeft 1 of meerdere employees in dienst. Dus je kan bij de `Person` klasse een lijst bijhouden met bedrijven waarvoor hij werkt en in de `Company` klasse een lijst met employees die voor het bedrijf werkt.

```java
public class Company {
    private List<Person> employees;
}
public class Person {
    private List<Company> companies;
}
```