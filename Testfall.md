# Den Glade Piraten - Krav

## Användningsfall - fully dressed
### Stämma av inbetalningar
#### Förkrav
Förfallodatumet för betalning av medlemsavgiften har passerats. Kassören är inloggad i systemet som kassör.

#### Huvudscenario
1. Kassören väljer att stämma av inbetalningar
2. Systemet kontaktar banken och efterfrågar uppgifter om inbetalningar
3. Banken överför uppgifter om inkomna betalningar till systemet
4. Systemet presenterar en lista över vilka medlemmar som betalat samt vilket belopp de betalat
5. Kassören initierar avstämning mellan inbetalat belopp och fakturerat belopp per medlem
6. Systemet presenterar lista med eventuella avvikelser markerade
7. Kassören konstaterar att inga avvikelser finns och avslutar funktionen

#### Alternativ
**2a. Systemet får ingen kontakt med banken**  
 1. Systemet meddelar kassören att det inte får kontakt med banken

**7a. Det finns avvikelser där någon medlem inte betalat eller betalat för lite**  
 1. Kassören markerar berörda fakturor  
 2. Systemet genererar lista över medlemmar samt totalbelopp för medlemsavgiften samt förseningsavgift  
 3. Åter till användningsfallet 'Generera fakturor'  
  
**7b. Det finns avvikelser där någon medlem betalat för mycket**  
 1. Kassören markerar berörda fakturor  
 2. Systemet visar berörd faktura med medlemsuppgifter  
 3. Kassören initierar utskrift av notifikation till berörd medlem  
 4. Systemet skriver ut notifikation  
 5. Kassören initierar återbetalning  
 6. Systemet kontaktar banken med uppgifterna  

## Testfall
### TF 1.1 Huvudscenario: funktion avstämning inbetalningar
1. Kassören väljer att stämma av inbetalningar
2. Systemfunktionen för avstämning initieras

### TF 2.1 Huvudscenario: systemet kontaktar banken
1. Systemet försöker kontakta banken
2. Banken svarar på kontaktförsöket
3. Systemet anger sina "inloggningsuppgifter"
4. Banken verifierar inloggningen

### TF 2.2 Huvudscenario: systemet kontaktar banken med felaktig inloggning
1. Systemet försöker kontakta banken
2. Banken svarar på kontaktförsöket
3. Systemet anger felaktiga "inloggningsuppgifter"
4. Banken avvisar inloggningen
5. Systemet meddelar användaren om problemet

### TF 2.3 Scenario 2a: systemet får ingen kontakt med banken
1. Systemet försöker kontakta banken
2. Banken svarar inte på kontaktförsöket
3. Systemet meddelar användaren om det misslyckade kontaktförsöket

### TF 4.1 Huvudscenario: matcha betalning med medlem
1. Systemet tar inbetalningens meddelandeinformation (som består av medlemsnumret)
2. Systemet söker efter numret i databasen
3. Numret hittas
4. Inbetalningen knyts till medlemmen

### TF 4.2 Huvudscenario: matcha betalning med medlem - felaktigt medlemsnummer
1. Systemet tar inbetalningens meddelandeinformation (som består av medlemsnumret)
2. Systemet söker efter numret i databasen
3. Numret hittas inte
4. Inbetalningen markeras som oknuten

### TF 4.3 Huvudscenario: systemet presenterar en lista över inkomna betalningar
1. Systemet kopplar indata från banken till medlem
2. Systemet formatterar informationen till en lista
3. Systemet visar listan

### TF 4.4 TF 4.1 Huvudscenario: systemet presenterar en lista över inkomna betalningar - felaktigt medlemsnummer
1. Systemet kopplar indata från banken till medlem
2. Systemet särbehandlar uppgifterna som inte kan matchas med en medlem
3. Systemet formatterar informationen till en lista  med omatchade inbetalningar överst
4. Systemet visar listan

### TF 5.1 Huvudscenario: funktion avstämning belopp
1. Kassören väljer att stämma av inbetalat belopp mot förväntat belopp
2. Systemfunktionen för beloppavstämning initieras

### TF 5.2 Huvudscenario: beloppsavstämning - korrekta belopp
1. Systemet söker upp medlemmens betalningssaldo via medlemsnumret
2. Systemet beräknar om inkommen betalning matchar det fakturerade beloppet
3. Det kvarstående beloppet är 0 kronor
4. Systemet uppdaterar medlemmens betalningssaldo

### TF 5.2 Huvudscenario: beloppsavstämning - för liten inbetalning
1. Systemet söker upp medlemmens betalningssaldo via medlemsnumret
2. Systemet beräknar om inkommen betalning matchar det fakturerade beloppet
3. Det kvarstående beloppet överstiger 0 kronor
4. Systemet uppdaterar medlemmens betalningssaldo

### TF 5.2 Huvudscenario: beloppsavstämning - för stor inbetalning
1. Systemet söker upp medlemmens betalningssaldo via medlemsnumret
2. Systemet beräknar om inkommen betalning matchar det fakturerade beloppet
3. Det kvarstående beloppet understiger 0 kronor
4. Systemet uppdaterar medlemmens betalningssaldo

### TF 6.1 Huvudscenario: funktion presentera beloppsavstämning
1. Systemet sorterar resultaten från beloppsavstämningen
2. Systemet formatterar de sorterade resultatet som en lista 

