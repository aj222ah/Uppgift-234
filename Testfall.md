# Den Glade Piraten - Testfall
## Användningsfall
### Stämma av inbetalningar
#### Huvudscenario
1. Kassören väljer att stämma av inbetalningar
2. Systemet kontaktar banken och efterfrågar uppgifter om inbetalningar
3. Banken överför uppgifter om inkomna betalningar till systemet
4. Systemet beräknar nytt saldo för respektive medlem
5. Kassören väljer att se listning av betalningar
6. Systemet presenterar en tabell över vilka medlemmar som betalat, fakturabelopp, betalat belopp samt betalningssaldo efter inbetalning
7. Kassören konstaterar att inga avvikelser finns och avslutar funktionen

#### Alternativ
**2a. Systemet får ingen kontakt med banken**  
 1. Systemet meddelar kassören att det inte får kontakt med banken
 
**4a. Medlemsnummer finns inte i databasen**
 1. Systemet markerar betalningen som avvikande
 2. Åter till steg 5 i huvudscenariot

**7a. Det finns avvikelser där någon medlem inte betalat eller betalat för lite**  
 1. Kassören markerar berörda fakturor  
 2. Systemet genererar lista över medlemmar, deras nya betalningssaldo, samt respektive förseningsavgift  
 3. Åter till användningsfallet 'Generera fakturor'  
  
**7b. Det finns avvikelser där någon medlem betalat för mycket**  
 1. Kassören markerar berörda fakturor  
 2. Systemet visar berörd faktura med medlemsuppgifter  
 3. Till användningsfallet 'Hantera utbetalning' 

## Förkrav
Samtliga användningsfall kräver att användaren är uppkopplad mot testdatabasen  

### Medlemsinformation i testdatabas
|Medlemsnummer|Medlem - namn    |Inledande betalningssaldo| 
|:-----------:|-----------------|------------------------:|
|111111       |Kalle Karlsson   |- 345,00 SEK             |
|222222       |Anders Andersson |- 549,00 SEK             |
|333333       |Sven Svensson    |- 152,45 SEK             |

|Fakturanummer|Medlemsnummer|Fakturadatum|Förfallodag|Fakturabelopp| 
|-------------|-------------|------------|-----------|------------:|
|1352610      |111111       |2013-11-10  |2013-11-30 |- 345,00 SEK |
|1352740      |222222       |2013-11-10  |2013-11-30 |- 549,00 SEK |
|1352605      |333333       |2013-11-10  |2013-11-30 |- 152,45 SEK |

### Övrig information om testdatabas
* Förseningsavgiften är 50 SEK + 8% av utestående betalning  
* Skrivaren är inkopplad, installerad och påslagen

#### Inloggningsuppgifter till testversion BankAPI
|Login:      |Lösenord:   |
|------------|------------|
|testa123    |admin987    |

## Testfall
### Grundläggande testfall (allmän användning - ej specifikt detta användningsfall)
|Testfall|Input               |Förväntad output|Förkrav: Genomfört testfall|Förkrav: Testversion av BankAPI|
|--------|--------------------|----------------|:-------------------------:|:-----------------------------:|
|a       |111111              |Kalle Karlsson  |-                          |Uppkoppling behövs ej          |
|b       |123456              |Medlem finns ej |-                          |Uppkoppling behövs ej          |
|c       |1352740             |Faktura hittad  |-                          |Uppkoppling behövs ej          |
|d       |Initiering funktion |Visning faktura |-                          |Uppkoppling behövs ej          |

#### TF a. Söka medlem - medlem finns
1. Indata: medlemsnummer 111111
2. Systemet söker efter numret i databasen
3. Medlem Kalle Karlsson hittas

#### TF b. Söka medlem - medlem finns inte
1. Indata: medlemsnummer 123456
2. Systemet söker efter numret i databasen
3. Ingen medlem hittas

#### TF c. Söka faktura - faktura finns
1. Indata: fakturanummer 1352740
2. Systemet letar upp fakturan

#### TF d. Visa faktura
1. Användare initierar visning
2. Systemet visar fakturan

### Testfall knutna till användningfallsscenariot
|Testfall|Input              |Förväntad output      |Förkrav: Genomfört testfall|Förkrav: Testversion BankAPI|
|--------|-------------------|----------------------|:-------------------------:|:--------------------------:|
|1.1     |Initiering funktion|Funktion startar      |-                          |Uppkoppling behövs ej       |
|2.1     |testa123, admin987 |Inloggning ok         |-                          |Uppkopplad                  |
|2.2     |321atset, 789nimda |Inloggning misslyckas |-                          |Uppkopplad                  |
|2.3     |                   |Bank ej tillgänglig   |-                          |Nedkopplad                  |
|4.1     |345,00             |0,00                  |a. (medlem 111111)         |Uppkopplad                  |
|4.2     |345,00             |-204,00               |a. (medlem 222222)         |Uppkopplad                  |
|4.3     |345,00             |192,55                |a. (medlem 333333)         |Uppkopplad                  |
|4.4     |belopp i SEK       |Avvikande inbetalning |b. (medlem finns ej)       |Uppkopplad                  |
|6.1     |Initiering funktion|Lista över betalningar|4.1 / 4.2 / 4.3 / 4.4      |Uppkoppling behövs ej       |
|7.1     |-204,00            |270,32                |4.2                        |Uppkoppling behövs ej       |

#### TF 1.1 Huvudscenario: funktion avstämning inbetalningar
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

#### TF 4.1 Huvudscenario: jämför betalningssaldo - korrekt inbetalning
1. Testfall söka medlem genomfört (medlem 111111)
2. Indata från bank: betalat belopp 345,00 SEK
3. Systemet hämtar betalningssaldo för medlem 111111: -345,00 SEK
4. Systemet beräknar nytt betalningssaldo (-345,00 + 345,00 = 0,00) 
5. Systemet sparar nytt betalningssaldo

#### TF 4.2 Huvudscenario: jämför betalningssaldo - för liten inbetalning
1. Testfall söka medlem genomfört (medlem 222222)
2. Indata från bank: betalat belopp 345,00 SEK
3. Systemet hämtar betalningssaldo för medlem 222222: -549,00 SEK
4. Systemet beräknar nytt betalningssaldo (-549,00 + 345,00 = -204,00) 
5. Systemet sparar nytt betalningssaldo

#### TF 4.3 Huvudscenario: jämför betalningssaldo - för stor inbetalning
1. Testfall söka medlem genomfört (medlem 333333)
2. Indata från bank: betalat belopp 345,00 SEK
3. Systemet hämtar betalningssaldo för medlem 333333: -152,45 SEK
4. Systemet beräknar nytt betalningssaldo (-152,45 + 345,00 = 192,55) 
5. Systemet sparar nytt betalningssaldo

### TF 4.4 Scenario 4a: jämför betalningssaldo - felaktigt medlemsnummer
1. Testfall b är utfört
2. Inbetalningen markeras som avvikande

### TF 6.1 Huvudscenario: systemet presenterar en tabell över inkomna betalningar
1. Testfall 4.1, 4.2, 4.3 och/eller 4.4 är utfört
2. Systemet sorterar information grupperad efter utfall
3. Systemet formaterar informationen till en tabell
4. Systemet visar tabellen

### TF 7.1 Scenario 7a: lägga på förseningsavgift
1. Testfall 4.2 är genomfört
2. Systemet letar upp medlemmens betalningssaldo (: -204,00 SEK)
3. Systemet beräknar förseningsavgift (204,00 * 0,08 = 16,32 + 50 = 66,32 SEK)
4. Systemet uppdaterar betalningssaldo (204,00 + 66,32 = 270,32) 
