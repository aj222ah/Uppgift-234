# Den Glade Piraten - Testfall

## Förkrav
### Uppkopplingar per testfall
| Testfall nr. | Uppkopplad mot testdatabas | Testversion av BankAPI | 
|:------------:|:--------------------------:|:----------------------:|
|2.1           |Ja                          |Uppkopplat              |
|2.2           |Ja                          |Uppkopplat              |
|2.3           |Ja                          |Nedkopplat              |
|2.2           |Ja                          |Uppkopplat              |
|2.2           |Ja                          |Uppkopplat              |
|2.2           |Ja                          |Uppkopplat              |
|2.2           |Ja                          |Uppkopplat              |
|2.2           |Ja                          |Uppkopplat              |
|2.2           |Ja                          |Uppkopplat              |

### Medlemsinformation i testdatabas
| Medlemsnummer | Medlem - namn              | Inledande betalningssaldo | 
|:------------: |----------------------------|:-------------------------:|
|111111         |Kalle Karlsson              |- 549,00 SEK               |
|222222         |Anders Andersson            |+ 152,45 SEK               |
|333333         |Sven Svensson               |0,00 SEK                   |

### Övrig information om testdatabas
* Förseningsavgiften är 50 SEK + 8% av utestående betalning  
* Skrivaren är inkopplad, installerad och påslagen

#### Inloggningsuppgifter till testversion BankAPI
|Login:      |Lösenord:   |
|------------|------------|
|testa123    |admin987    |

## Testfall
### TF 1.1 Huvudscenario: funktion avstämning inbetalningar
1. Kassören väljer att stämma av inbetalningar
2. Systemfunktionen för avstämning initieras

### TF 2.1 Huvudscenario: systemet kontaktar banken
1. Systemet försöker kontakta banken
2. Banken svarar på kontaktförsöket
3. Systemet anger sina inloggningsuppgifter
4. Banken verifierar inloggningen

### TF 2.2 Huvudscenario: systemet kontaktar banken med felaktig inloggning
1. Systemet försöker kontakta banken
2. Banken svarar på kontaktförsöket
3. Systemet anger felaktiga inloggningsuppgifter
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
2. Systemet formaterar informationen till en lista
3. Systemet visar listan

### TF 4.4 TF 4.1 Huvudscenario: systemet presenterar en lista över inkomna betalningar - felaktigt medlemsnummer
1. Systemet kopplar indata från banken till medlem
2. Systemet särbehandlar uppgifterna som inte kan matchas med en medlem
3. Systemet formaterar informationen till en lista med omatchade inbetalningar överst
4. Systemet visar listan

### TF 5.1 Huvudscenario: funktion avstämning belopp
1. Kassören väljer att stämma av inbetalat belopp mot förväntat belopp
2. Systemfunktionen för beloppsavstämning initieras

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
2. Systemet formaterar de sorterade resultatet som en lista 

### TF 7.1 Scenario 7a: lägg på förseningsavgift
1. Systemet letar upp medlemmens betalningssaldo
2. Systemet beräknar förseningsavgift
3. Systemet presenterar betalningssaldot samt beräknad förseningsavgift
4. Systemet mottar godkännande från kassör
5. Systemet uppdaterar betalningssaldo

### TF 7.2 Scenario 7b: presentera medlemsfaktura
1. Kassör väljer vilken medlemsfaktura hen vill se
2. Systemet letar upp fakturan och visar den

### TF 7.3 Scenario 7b: funktion initiera återbetalning
1. Kassör initierar funktionen
2. Systemet letar upp medlemsinformation och betalningssaldo
3. Systemet kontaktar banken (se separat testfall) med uppgifterna