---
layout: post
title: "Monitorering av moln applikationer"
date: 2021-10-05 17:38:00
tags:  
--- 

### Beskriv kort applikationen

Jag valde att fortsätta med min web app från "Webbapplikationer i molnet" där jag gjort en cosmos databas som lägger till en spelare
med förnamn, efternman och position. Tanken är att det ska vara en fotbollsspelare och det är inte tydligt i själva applikationen, 
men har inte fokuserat helt på den biten när jag gjorde programmet för två veckor sedan. 

När man ska lägga till en spelare, så måste man fylla i förnamn, efternamn och position. Gjorde man inte det i förra programmet
så skickades man bara till startsidan utan att någonting sparades, nu kommer istället ett felmeddelande upp och det ser ut såhär:

![image](https://user-images.githubusercontent.com/65369996/136073453-662dc1c0-a690-4aa5-837a-644b089f55ed.png)


I samband med detta felmeddelandet, så skapas även ett exception som registreras i Appinsights. Kommer visa ett exempel längre ner i detta inlägg. 

### Ett enklare diagram över programmet

![image](https://user-images.githubusercontent.com/65369996/136065886-655cb8cc-08d8-41c4-bff8-3c3455caeae8.png)

### Beskriv koden för loggimplementationen 

Det första man måste göra för att få detta att funka är att lägga till denna kodraden inne i startup-filen:

![image](https://user-images.githubusercontent.com/65369996/136066582-1e3eb6c5-95d2-4c41-9e57-a7ad98129388.png)
 
Det är för att App insights ska kunna mäta alla request och liknande som görs i applikationen. 
För att App insights också ska fungera, så ska man aktivera det inne i Azure portalen. 

![image](https://user-images.githubusercontent.com/65369996/136067022-51a55816-8043-4add-b4cd-374417ee9efc.png)


När man sedan trycker på "View Application Insights data, så kommer man även vidare till en sida där man kan hitta
sin instrumental key, som är viktigt att lägga in i appsettings filen i programmet, för att koppla programmet till rätt resurs på Azure.

![image](https://user-images.githubusercontent.com/65369996/136067370-0a448a51-d2fb-4dcc-8cce-ee379539da9b.png)

* Har valt att dölja nyckeln på bilden för att ingen obehörig ska komma åt den. 

För att sedan lägga till loggingen i själva applikationen så har jag fått lägga till namespacet "Microsoft.Extensions.Logging.
Med Dependency injection, har jag sedan fått in det i den delen av programmet där spelaren skapas. 

![image](https://user-images.githubusercontent.com/65369996/136067885-2868d4e8-e156-418c-bba0-b2867756b027.png)

Här nedan gör jag en kontroll på att ifall något av fälten när man ska spara en spelare inte är ifyllda, så kommer ett exception
skickas och ett meddelande kommer visas för användaren. Det meddelandet finns i början på detta inlägget. 

![image](https://user-images.githubusercontent.com/65369996/136068389-69217706-0c09-4596-82c3-894634461f1c.png)

Det som sker i samband med detta också, är att exceptionet kommer visas i App Insights inne på min resurs på Azure portal
och det kan se ut såhär:

![image](https://user-images.githubusercontent.com/65369996/136069533-9c4f531f-b694-4b6a-9df7-e91348a6de35.png)


Nu är det ganska mycket information på denna bilden, men kollar man närmare på högerspalten, så ser man att det är ett ArgumentException som har blivit sparat.
Kollar man även längre ner, så ser man en text där det står "OrginalFormat" och texten "You need to fill in all the fields", vilket är meddelandet som jag 
lagt in i programmet för att användaren ska se att något har blivit fel. 


### Hur kan logging hjälpa till med säkerheten?

Loggingen kan göra oerhört mycket för säkerheten. Man kan framförallt bli notifierad direkt ifall något akut händer, men man kan även se allt som användarna
gör. Ett bra verkligt exempel med logging är på tex myndigheter, så loggas allt som personalen gör på datorerna. Det gör man för att det finns känslig
data som personalen har hand om och inte får använda sig utav bara nyfikenhet, men som de alltid har tillgång till. Med hjälp av logging, så kan man då
spåra vem som har varit inne på vad och i fall något inte skulle gå rätt till, så är det enkelt att se vem som har gjort det.

För mitt program för stunden, så är ovanstående exempel meningslöst men det är bara en grym grej som logging kan göra för säkerheten.

### Mina Queries

Här är min första:

![image](https://user-images.githubusercontent.com/65369996/136073910-244bcaa9-688d-4632-8f45-e13c854545f6.png)

Den visar hur många misslyckade request det har varit och på vilket ställe det har gått fel. 
Detta är bra för att upptäcka fel i sin kod eller se ett beteende från användarna. 
Man kanske har något som är otydligt på hemsidan och där många av användarna glömmer / trycker fel
och med denna queryn så kommer allt sådant att upptäckas när man ska lägga till en spelare.


Här är min andra:

![image](https://user-images.githubusercontent.com/65369996/136074789-56f3709f-2d7c-4f21-873e-7df981b0d81f.png)

På denna så visar den från vilka länder användarna kommer ifrån som är inne på sidan. 
Detta kan vara bra att veta för att man ska kunna anpassa sin applikation så bra som möjligt beroende på vart 
man till exempel har kunder ifrån. 










