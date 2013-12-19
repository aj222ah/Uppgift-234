### Söka medlem - medlem finns
1. Indata från bank: medlemsnummer 111111
2. Systemet söker efter numret i databasen
3. Medlem Kalle Karlsson hittas

### Söka medlem - medlem finns inte
1. Indata från bank: medlemsnummer 123456
2. Systemet söker efter numret i databasen
3. Ingen medlem hittas

### Jämför betalningssaldo - korrekt inbetalning
1. Testfall söka medlem genomfört (medlem 111111)
2. Indata från bank: betalat belopp 549,00 SEK
3. Systemet hämtar betalningssaldo för medlem 111111: -549,00 SEK
4. Systemet beräknar nytt betalningssaldo (-549,00 + 549,00 = 0,00) 
5. Systemet sparar nytt betalningssaldo

### Jämför betalningssaldo - för liten inbetalning
1. Testfall söka medlem genomfört (medlem 111111)
2. Indata från bank: betalat belopp 349,00 SEK
3. Systemet hämtar betalningssaldo för medlem 111111: -549,00 SEK
4. Systemet beräknar nytt betalningssaldo (-549,00 + 349,00 = -200,00) 
5. Systemet sparar nytt betalningssaldo

### Jämför betalningssaldo - för stor inbetalning
1. Testfall söka medlem genomfört (medlem 111111)
2. Indata från bank: betalat belopp 799,00 SEK
3. Systemet hämtar betalningssaldo för medlem 111111: -549,00 SEK
4. Systemet beräknar nytt betalningssaldo (-549,00 + 799,00 = 250,00) 
5. Systemet sparar nytt betalningssaldo





