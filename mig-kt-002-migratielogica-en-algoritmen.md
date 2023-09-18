# MIG-KT-002 - Migratielogica en algoritmen

## Beschrijving <a href="#beschrijving" id="beschrijving"></a>

## Overwegingen <a href="#overwegingen" id="overwegingen"></a>

### Van bus naar store <a href="#van-bus-naar-store" id="van-bus-naar-store"></a>

De grootste paradigmashift in Koppeltaal 2.0 is de afscheid van de bus-architectuur, waar berichten door middel van een postbus worden uitgewisseld, naar een FHIR resource service waar de gegevens binnen het domein door middel van opgeslagen FHIR objecten worden uitgewisseld. Met deze wijziging wordt een significante verantwoordelijkheid die bij de applicatieleveranciers ligt, het in stand houden van de status quo door het correct verwerken van de berichten, weggenomen. De FHIR resource service is binnen het domein een bron van waarheid waar applicaties op elk gekozen moment terecht kunnen voor de laatste versie van de resources binnen het domein. Deze paradigmashift vereist dat er wordt nagedacht over hoe naar Koppeltaal 2.0 te migreren.

### Id’s en identifiers <a href="#ids-en-identifiers" id="ids-en-identifiers"></a>

Koppeltaal 1.x maakt gebruik van FHIR DSTU3 en message bundles. Alle resources binnen de bundle, net als de bundle zelf, moeten uniek geïdentificeerd worden met de resource link. Verder, hebben sommige entiteiten, maar niet alle, een een FHIR identifier. Een FHIR identifier bestaat uit een system en een waarde. Het system maakt het mogelijk te differentiëren in verschillende type identifiers.

`<identifier> <system>https://example.com/identifiers/email</system> <value>bert@example.com</value> </identifier>`

Koppeltaal 2.0 maakt gebruik van R4, in FHIR R4 kent elk object een logical id en een type. Met de combinatie van deze twee is het mogelijk een canonical URL te maken, hetgeen lijkt op de resource link. Daarnaast kan, net als in FHIR DSTU3 een object één of meerdere identifier hebben.

In Koppeltaal 2.0 en FHIR R4 is er echter een belangrijk verschil rond de logical id / resource link. Waar in Koppeltaal 1.x deze door de maken van de resource wordt toegewezen, gebeurt dit in Koppeltaal 2.0 door de FHIR resource service, zie ook [TOP-KT-003 - Logische ID, bedrijfsidentifier, referenties en referentie integriteit](https://vzvz.atlassian.net/wiki/spaces/KTSA/pages/27066395) .

### Migratie: tijdelijke identifiers <a href="#migratie-tijdelijke-identifiers" id="migratie-tijdelijke-identifiers"></a>

Gegeven de bovenstaande observaties is er een oplossingsrichting bedacht waar gebruik wordt gemaakt van een tijdelijk, migratiespecifieke, identifier. Deze identifier heeft een specifiek systeem en in de waarde is de resource link waarmee de resource in Koppeltaal 1.x uniek wordt geïdentificeerd. Deze tijdelijke identifier maakt het mogelijk de Koppeltaal 1.x identifier van resources van de bron van de resource naar de afnemers van de resource te communiceren. Bij het aanmaken van de resource in het Koppeltaal 2.0 domein voegt het bronsysteem de waarde van de Koppeltaal 1.x resource link toe aan de entiteit, zodat het systeem wat deze ontvangt op basis van deze identifier de entiteit in de database correct kan verwerken.

&#x20;

### Migratie: timing en afhankelijkheden <a href="#migratie-timing-en-afhankelijkheden" id="migratie-timing-en-afhankelijkheden"></a>

De oplettende lezer van het voorgaande neemt waar dat er in de bovengestelde oplossingsrichting een sterke afhankelijkheid bestaat tussen de bronhouder en afnemer van de resource; waar verwijzingen bestaan tussen resources is het onmogelijk de resources te publiceren alvorens deze zelf te publiceren. Er ligt dus letterlijk een kleine puzzel aan afhankelijkheden die per domein gelegd moet worden.

## Toepassing, eisen en restricties <a href="#toepassing-eisen-en-restricties" id="toepassing-eisen-en-restricties"></a>

## Gebruikte standaarden <a href="#gebruikte-standaarden" id="gebruikte-standaarden"></a>

## Voorbeelden <a href="#voorbeelden" id="voorbeelden"></a>

