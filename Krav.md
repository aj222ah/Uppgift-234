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
Uppdatera medlemsuppgifter / båtinnehav  
Hantera medlemsavgiftsbetalning      
Fördela båtplatser  
Boka utrustning

## Användningsfall - kort format
### Uppdatera medlemsuppgifter
Medlemmen loggar in och väljer vilken/vilka uppgift(er) hen vill uppdatera. Medlemmen anger sin nya information och sparar. Systemet bekräftar att uppgifter sparats.

### Fördela båtplatser
Sekreteraren är inloggad i systemet som administratör och väljer att se förra säsongens båtplatser. Systemet presenterar listan. Sekreteraren väljer att i möjligaste mån läta medlemmarna behålla sina platser från förra året. Systemet bekräftar de sparade platserna och presenterar en lista över resterande båtar och tillgängliga kajplatser. Sekreteraren kan nu välja att antingen få förslag på hur båtplatserna ska fördelas från systemet eller göra sammankopplingen själv. När samtliga båtar fått en plats sparar sekreteraren uppgifterna. Systemet bekräftar att uppgifterna sparats.

### Boka utrustning
Medlemmen är inloggad i systemet och systemet presenterar en lista över utrustning. Medlemmen väljer tidpunkt som han vill boka utrustning för och systemet visar utrustning som är bokningsbar vid det angivna tillfället. Medlemmen väljer utrustning och sparar sin bokning. Systemet bekräftar bokningen.

## Användningsfall - fully dressed
### Hantera medlemsavgiftsbetalning
#### Förkrav
Det är dags att fakturera medlemsavgifterna. Kassören är inloggad i systemet som kassör. Klubben erbjuder endast pappersfaktura.

#### Huvudscenario
1. Kassören initierar fakturagenerering
2. Systemet presenterar en lista över medlemmar och deras totalbelopp för medlemsavgiften
3. Kassören väljer att skriva ut fakturor
4. Systemet skriver ut fakturor
5. Respektive medlem betalar sin faktura hos sin bank
6. Banken överför uppgifter om inkomna betalningar till systemet
7. Kassören väljer att se betalningar
8. Systemet presenterar en lista över vilka medlemmar som betalat samt vilket belopp de betalat
9. Kassören initierar avstämning mellan inbetalat belopp och fakturerat belopp per medlem
10. Systemet presenterar lista med eventuella avvikelser markerade
11. Kassören konstaterar att inga avvikelser finns och avslutar funktionen

#### Alternativ
2a. Systemet indikerar ett problem med beräkning av något fakturabelopp
1. Kassören väljer att granska den berörda fakturan
2. Systemet visar fakturan med problemet markerat
3. Kassören anger uppgifterna manuellt
4. Åter till punkt 4 i huvudscenariot

10a. Det finns avvikelser där någon medlem inte betalat eller betalat för lite
1. Kassören markerar berörda fakturor
2. Systemet genererar lista över medlemmar samt totalbelopp för medlemsavgiften samt förseningsavgift
3. Åter till punkt 3 i huvudscenariot

10b. det finns avvikelser där någon medlem betalat för mycket
1. Kassören markerar berörda fakturor
2. Systemet visar berörd faktura med medlemsuppgifter
3. Kassören initierar utskrift av notifikation till berörd medlem
4. Systemet skriver ut notifikation
5. Kassören initierar återbetalning
6. Systemet kontaktar banken med uppgifterna
7. Medlemmen får sin återbetalning från banken
8. Banken bekräftar till systemet att återbetalning skett
9. Systemet korrigerar sina uppgifter
10. Åter till punkt 7 i huvudscenariot
