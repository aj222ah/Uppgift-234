# Den Glade Piraten - Krav

## Aktörer

### Primära
#### Kassör  
Vill kunna hantera medlemsavgiftsberäkning, fakturering och uppgifter om betalningar på ett smidigt sätt.  

#### Sekreterare (administratör)  
Vill få överblick över klubbens medlemmar samt deras båtinnehav och båtplatser. Vill ha ett enkelt sätt 
att fördela passande båtplatser till klubbens medlemmar.  

#### Medlem  
Vill kunna uppdatera sina egna uppgifter, dels personliga uppgifter men också om båtinnehav etc. 
Vill få fakturor på korrekta belopp och slippa manuellt lämna in kvitton till kassören. Vill ha möjlighet 
att boka utrustning som tillhandahålls av klubben för att säkerställa att den finns tillgänglig när 
medlemmen är på båtklubben.

### Sekundära
#### Nationella båtregistret  
Tillhandahåller information om båtar

#### Banksystem 
Hanterar medlemmarnas betalning av medlemsavgiften och tillhandahåller informationen åt klubben

#### Räddningstjänsten 
Förväntar sig att få korrekta uppgifter om båtarnas kajplatser vid behov

## Identifierade användningsfall
Uppdatera medlemsuppgifter  
Uppdatera båtinnehav  
Generera fakturor  
Stämma av inbetalningar  
Fördela båtplatser  
Boka utrustning  

[Diagram finns här](https://c9.io/aj222ah/uppgift234/workspace/Use case lab 3.pdf)

## Användningsfall - kort format
### Uppdatera medlemsuppgifter
Medlemmen loggar in och väljer vilken/vilka uppgift(er) hen vill uppdatera. Medlemmen anger sin nya information och sparar. Systemet bekräftar att uppgifter sparats.

### Uppdatera båtinnehav
Medlemmen loggar in och väljer att uppdatera båtinnehav. Systemet presenterar alternativen uppdatera befintlig båt eller registrera ny båt. Medlemmen väljer och skriver in uppgifterna. Systemet kontaktar nationella båtregistret för att komplettera uppgifter om ägare samt detaljer om båten. Nationella båtregistret överför uppgifterna till systemet. Systemet presenterar uppgifterna för medlemmen. Medlemmen sparar uppgifterna. Systemet bekräftar att uppgifterna sparats.

### Gererera fakturor
Kassören initierar fakturagenerering. Systemet presenterar en lista över medlemmar och deras totalbelopp för medlemsavgiften. Kassören väljer att skriva ut fakturor. Systemet skriver ut fakturor

### Fördela båtplatser
Sekreteraren är inloggad i systemet som administratör och väljer att se förra säsongens båtplatser. Systemet presenterar listan. Sekreteraren väljer att i möjligaste mån läta medlemmarna behålla sina platser från förra året. Systemet bekräftar de sparade platserna och presenterar en lista över resterande båtar och tillgängliga kajplatser. Sekreteraren kan nu välja att antingen få förslag på hur båtplatserna ska fördelas från systemet eller göra sammankopplingen själv. När samtliga båtar fått en plats sparar sekreteraren uppgifterna. Systemet bekräftar att uppgifterna sparats.

### Boka utrustning
Medlemmen är inloggad i systemet och systemet presenterar en lista över utrustning. Medlemmen väljer tidpunkt som han vill boka utrustning för och systemet visar utrustning som är bokningsbar vid det angivna tillfället. Medlemmen väljer utrustning och sparar sin bokning. Systemet bekräftar bokningen.

## Användningsfall - fully dressed
### Stämma av inbetalningar
#### Förkrav
Förfallodatumet för betalning av medlemsavgiften har passerats. Kassören är inloggad i systemet som kassör.

#### Huvudscenario
1. Banken överför uppgifter om inkomna betalningar till systemet
2. Kassören väljer att se betalningar
3. Systemet presenterar en lista över vilka medlemmar som betalat samt vilket belopp de betalat
4. Kassören initierar avstämning mellan inbetalat belopp och fakturerat belopp per medlem
5. Systemet presenterar lista med eventuella avvikelser markerade
6. Kassören konstaterar att inga avvikelser finns och avslutar funktionen

6a. Det finns avvikelser där någon medlem inte betalat eller betalat för lite  
 1. Kassören markerar berörda fakturor  
 2. Systemet genererar lista över medlemmar samt totalbelopp för medlemsavgiften samt förseningsavgift  
 3. Åter till användningsfallet 'Generera fakturor'  
  
6b. Det finns avvikelser där någon medlem betalat för mycket  
 1. Kassören markerar berörda fakturor  
 2. Systemet visar berörd faktura med medlemsuppgifter  
 3. Kassören initierar utskrift av notifikation till berörd medlem  
 4. Systemet skriver ut notifikation  
 5. Kassören initierar återbetalning  
 6. Systemet kontaktar banken med uppgifterna  
