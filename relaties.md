## Relaties

- Java: Onderlinge verhoudingen tussen objecten
- Database: Verhoudingen tussen entiteiten


- Java: Has-a relaties en is-a relaties
- Database: Alleen has-relaties


- Java: Relaties worden gemaakt met instantie variabelen
- Database: Maken gebruik van Foreign Keys en koppeltabellen

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

### Kardinaliteit in Java

- 0 tot 1 relatie, iemand heeft bijvoorbeeld 0 of 1 adres, dus nooit 2, 3 of 5
- 1 tot 1 relatie, iemand heeft altijd een adres
- 0 tot N relatie, 0 tot meer kan bijvoorbeeld zijn iemand heeft 0 of meer kinderen
- 1 tot N relatie, 1 of meer kan bijvoorbeeld zijn een bedrijf heeft 1 of meer werknemers
- N tot N relatie, meer of meer is bijvoorbeeld een hond kan meerdere baasjes hebben en een baasje kan meerdere honden hebben

Standaard 0, 1 of oneindig! Je kan ook zeggen dat iets 1 tot 5 relatie kan zijn, bijvoorbeeld iemand kan max 5 adressen hebben.

### Kardinaliteit in Database

- 0 tot 1 relatie
- 1 tot 1 relatie
- 0 tot N relatie
- 1 tot N relatie
- N tot N relatie

Altijd 0, 1 of oneindig. In een database model zeggen we nooit dat iets een 1 tot 5 relatie kan hebben.

### Compositie & aggregatie

De diamantjes die ingekleurd of niet ingekleurd zijn.

- Aggregatie: geen eigenaarschap. 
- Aggregatie: objecten kunnen los van elkaar bestaan
- Compositie: wanneer het object met eigenaarschap wordt verwijderd, verdwijnen de relatie-objecten ook

Stel je hebt een klasse Person en een klasse Adres en je verwijderd de klasse Person, heeft het dan nut om de klasse Adres te laten bestaan. Heeft het wel nut om klasse Adres the laten bestaan dat hij niet verwijderd hoeft te worden dan heb je een aggregatie. Moet Adres verwijdert worden als Person klasse verwijderd wordt dan heb je een compositie.