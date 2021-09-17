---
layout: post
title: "Vad är serverless"
date: 2021-09-16 17:17:00
tags: Serverless FaaS AzureFunctions
--- 

### Vad är serverless? 

På namnet så låter det kanske som man kör program utan att använda sig av en server, men så är inte fallet.
Med "Serverless" är hur en server hanteras samt implementeras och är något som hanteras av molnbaserade leverantörer.
Servern/servrarna hanteras alltså istället av en leverantör och inte från företaget som utvecklar sin app. 
På detta viset, så slipper företaget som hyr servern att underhålla, utveckla, uppdatera och hantera vanliga infrastrukturuppgifter.

Serverless arkitekturen håller aldrig berkäkningsresurser i instabila minnen, utan beräkningsresurserna tar plats i små partier. 
Låt säga att i fall man inte använder en applikation, så kommer inga resurser att tilldelas till servern.
Med detta så betalar man för det man använder och det blir kostnadseffektivt för företaget. 

Huvudsaken med denna serverless modellen är att underlätta utvecklingsprocessen till produktion. 
När man väl distribuerat tjänsten så svarar applikationen väldigt snabbt till krav och kan skala upp och ner applikationen automatiskt efter kravspecifikationen.
Utvecklarna som använder tjänsten, behöver inte tänka på bandbredd eller hur många servrar applikationen behöver. 
Man kan kräva mer bandbredd och servrar efter behov medans behoven ökar och det går snabbt att fixa utan större bemödan.

### Fördelar med serverless

<strong>Kostnadseffektivt<strong>

Som jag var inne på tidigare, så blir det billigare för ett företag att använda sig av serverless.
Man betalar för det man använder och slipper då onödiga kostnader som att betala för appar som man inte använder längre.
Molntjänstleverantören tar bara betalt utav dig för minnet som används och tiden som koden körs och inte för appar som är inaktiva.

Man sparar pengar på saker som att man slipper installation, licenser, uppdatering m.m.

<strong>Snabbare appdistribution<strong>

Utvecklarna behöver inte köra backend konfigurationen eller ladda upp kod till servern för att distribuera en ny version av appen. 
Man har också flexibiliteten att distrubuera ny kod direkt efter varandra eftersom det inte är någon sluten arkitektur. 
Utöver ovanstående, så kan man även uppdatera, lägga till nya funktioner och fixa fel i appen väldigt snabbt. 


<strong>Produktivet<strong>

Eftersom utvecklarna själva inte behöver fixa serverhanteringen, så sparar man tid och blir mer effektiva. 
De behöver heller inte tänka på att hantera HTTP request eller "multithreading" i koden. 

<strong>Skalbarheten<strong>

"Serverless" system erbjuder en hög grav av skalbarhet, eftersom man kan skala upp eller ned baserat på företagets behov för stunden.
Leverantören sköter den automatiska skalningen vilket gör att utvecklarna kan fokusera på annat.
Utvecklare i mindre team kan köra sin kod självständigt utan att behöva stöd eller infrastruktur. 

Det finns ju även nackdelar med serverless och dessa kommer nedan.

### Nackdelar med serverless
  
<strong>Säkerhet<strong>

Säkerhet är något som blir allt viktigare över nätet, men med nya tekniker så uppstår också nya säkerhetshål. 
När man använder sig av "Serverless computing" så har man inte själv kontrollen från leverantören som man använder.
Det medför att det är riskabelt när hela företagets backend med känslig information är sparade på en sådan server.
  
<strong>Prestanda<strong>
  
Ibland kan kod som körs mindre få en viss fördröjning än kod som körs kontinuerligt på mjukvaru containrar, dedikerade servrar och virtuella maskiner. 
Det tar tid för servern att starta om och skapar då ännu mer fördröjning på applikationen att starta / svara. 
  
<strong>Svårt att testa och felsöka<strong>

Man behöver veta hur sin kod presterar när man har distrubuerat den och för det så behöver man testa koden, vilket är svårt i en "serverless" miljö. 
Eftersom utvecklarna också inte har kontroll över varje backend process, samt att applikationer är uppdelade i mindre funktioner så blir felsökningen även problematisk. 
  
 
### Vad är FaaS?
  
Faas står för "Function as a Service" vilket är en molntjänst där utvecklare kan bygga, köra och hantera applikationspaket som funktioner
utan att behöva underhålla deras egna infrastruktur. 
  
Faas är en händelsestyrd modellteknik som kör "stateless" containers och dessa funktioner hanterar server-side logik och "state" genom
användningen av tjänster från en Faas leverantör. 
  
###  Faas och serverless
  
Faas är ett sätt att implementera "serverless computing" då utvecklare kan skriva business logiken som sedan körs i Linux containers och hanteras 
av en plattform.
Vanligtvis så körs molnbaserade tjänster av en molnbaserad plattform men denna modell utvecklas hela tiden så att man kan köra denna modellen även lokalt och med hybriddistrubution.
  
En funktion är en del av en mjukvara som kör business logiken på ett operativsystem. Applikationer kan bli kombinerade av många olika funktioner.
Att använda Faas-modellen är ett sätt att bygga en app med arkitekturen från "Serverless".
  
FaaS ger utvecklare en abstraktion av att köra webbapplikationer som ger svar från händelse, utan att man behöver hantera servern.
Som ett exempel så kan man ladda upp en fil som utlöser kod som sedan konverterar filen till många olika format. 
  
Detta är bara en bråkdel av vad faktiskt FaaS är men ger en mindre inblick om vad det är. 
  

### Vår kalkylator
  
Här är koden för vår kalkylator:
  
![image](https://user-images.githubusercontent.com/65369996/133748291-774bc30f-752a-45b8-99dd-9a02473ffb6c.png)
  

 De första raderna: 
  
 ![image](https://user-images.githubusercontent.com/65369996/133748598-a1a3052a-b15e-4e88-b256-66e0c0f8d908.png)
  
Gör att vi kan skriva in ett namn för requestet och sedan kalkylera ett uttryck. Man kan ta bort name parametern, men vi valde ha kvar den bara för att skicka ett litet meddelande.
  
  * num = första numret som man fyller i
  * op = Vilken operator man kör, exempelvis * / + eller -
  * num2 = Det är andra numret som ska beräknas. 
  
Val av namn på variablerna är inte optimala, men vi valde att inte lägga större fokus på det. 
  
Om ni kollar på bilderna nedan, så kan ni se ett resultat av att fylla i de fyra parametrarna som jag precis beskrivit. 
  
  ![image](https://user-images.githubusercontent.com/65369996/133749219-e2b3dc4e-3bca-4fa7-a027-b79533c5add0.png)
  
 ![image](https://user-images.githubusercontent.com/65369996/133750564-522480e2-9450-408b-886a-6535e33bcba0.png)



Vi har gjort en switch-sats för att man skall kunna välja vilken operator som ska beräkna de två talen.
Först och främst, så skapade vi ju variablen op som en sträng. Initu switch-satsen så konverterar vi de strängarna som ska räkna ut summan och gör om num och num2 till datatypen int. 
  
Sedan skickar vi resultatet till strängen responsemessage och där har vi enkelt valt att bara skriva ut "Hello <name> , <num> <operator> <num> = <sum>. Detta ser ni även på bilderna ovan. 
  
Här är switch-satsen: 

  ![image](https://user-images.githubusercontent.com/65369996/133750314-6f2bec9b-eff3-4d00-aefb-2534fc5479f0.png)

Här är strängen med responsemessage:
  
 ![image](https://user-images.githubusercontent.com/65369996/133750400-a3157e13-fe4e-46ff-bf26-13f4f06f95d5.png)
  
  
 För att skapa denna HTTP trigger, så har vi först gått in och skapat en ny resurs inne i Azure portalen.
  
 ![image](https://user-images.githubusercontent.com/65369996/133752717-8dcedf62-6ce3-47d5-8acc-4e92e438168b.png)
  
 Sedan har vi valt Compute > Funktionsapp 
  
 ![image](https://user-images.githubusercontent.com/65369996/133752810-60f83a06-0035-4104-808c-da476431b15a.png)
  
 Då får man upp ett formulär som skall fyllas i: 
  
 ![image](https://user-images.githubusercontent.com/65369996/133752896-83aa3987-0b4f-4c35-9fbb-08dfc946547b.png)
  
 Efter ha skapat resursen och funktions appen, så går man in på funktionsappen och får upp följande meny: 
  
 ![image](https://user-images.githubusercontent.com/65369996/133753362-13e17a96-d47f-49b0-ad4c-54f16bd2db6e.png)
 
  Här klickar man på funktioner och sedan skapa. Då kommer det upp en lista med mallar på vilken trigger man vill skapa.
  I detta fallet skulle vi skapa en HTTP trigger, som då utlöses vid ett GET/POST request. 
  
  ![image](https://user-images.githubusercontent.com/65369996/133763695-8ca055c6-1f22-466f-b223-cdeaf994fefa.png)

 Efter man har skapat triggern, så trycker man på kod + test och sedan kan man skriva sin kod. 
 Alla dessa steg ovan gjorde vi innan vi kunde börja skriva koden. 
  
 
 ### Hur har vi testat applikationen / Säkerhet?
  
  Vi har bara skrivit några olika request, ett av testerna finns högre upp, där man kan se resultet från beräkningen 21 * 45 = 945.
  Mer än så har vi egentligen inte testat. 
  Säkerhetshoten mot denna app är väl egentligen inte något problem, då ingen känslig information finns. Vi har ingen databas för att använda oss och spara informationen från 
  kalkylatorn och inga användare mer än oss själva som loggar in på vårt Azure konto, så därav har vi inte gjort något för att säkra den. 
  
  Eftersom det är en sån simpel applikation, har vi heller inte gjort någon felhantering, så skulle man inte tex skriva något annat än de fyra operatorerna 
  vi har valt till kalkylatorn, så har vi inget som säger att det blir fel. 
  
  
  
  
  
  
 

















