## Database

### Wat is een database?

Een database is een georganiseerde collectie van gestructureerde informatie (of data) dat is opgeslagen in een (elektronisch) systeem. Elektronisch wordt de data gecontroleerd door een database management systeem (DBMS). Deze twee samen zijn onderdeel van het database-systeem of kortgezegd de database.

- <i> georganiseerde collectie van gestructureerde informatie (of data)</i>: je moet vooraf bepalen hoe het georganiseerd gaat zijn.
- <i>database management systeem (DBMS)</i>: is het softwarepakket. Het database-systeem dat we gebruiken heet `pgAdmin`.

### Eisen aan de data

Als je data in een database wilt opslaan moet het aan een paar dingen voldoen.

- data moet (eenvoudig) opslaanbaar zijn
- data moet uitgelezen en doorzocht kunnen worden
- data moet bewerkt moeten kunnen worden
- data moet verwijderd kunnen worden zonder nadelige gevolgen

### Eisen  data en database

De data moet consistent zijn.
- <i>Sla de data niet dubbel op</i>. Bijv. wanneer je een rekeningnummer 1234 in tabel 1 hebt staan en hetzelfde rekeningnummer ook in tabel 2. Wanneer het rekeningnummer verandert en alleen in tabel 1 wordt aangepast is je data inconsistent
- <i>Relaties moeten blijven kloppen wanneer de gegevens verwijderd worden</i>.

Autorisatie/Authenticatie: bij installeren moest je een postgres user aanmaken en hiervoor heb je een wachtwoord aangemaakt. Deze user heeft toegang tot <u>ALLE</u> DBMS.
- <i>Geef niet iedereen toegang tot lezen, schrijven en verwijderen</i>.

### ACID

Wat moet een databasetransactie garanderen?

- Atomicity <br/>
CRUD-operaties zijn "all or nothing". Operatie wordt uitgevoerd of niet uitgevoerd. Niet gedeeltelijk.

- Consistency <br/>
De database verandert alleen in valide status. Dus een aanpassing maakt de database niet kapot.

- Isolation <br/>
Bij gelijktijdige operaties moet het resultaat hetzelfde zijn als bij serieële operaties. Dus bijvoorbeeld wanneer er 1 of 500 mensen tegen de database aanpraat, moet hij hetzelfde resultaat geven.

- Durability <br/>
Wanneer een transactie is committed (doorgevoerd) dan blijft die ook comitted. Ook bij stroomuitval, crashes of errors.