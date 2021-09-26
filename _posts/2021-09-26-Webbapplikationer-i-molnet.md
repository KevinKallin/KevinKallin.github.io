---
layout: post
title: "Webbapplikationer i molent"
date: 2021-09-26 12:53:00
tags: CosmosDb Webbapplikation RazorPages
--- 

### Vad gör applikationen? 

Det är en väldigt simpel applikation. Det enda man kan göra är att lägga till en spelare med förnamn, efternman och position och spara det i en databas.
Position kan tyckas vara otydlig, men en spelare i detta fallet syftar på en fotbollsspelare. Vi har endast fokuserat på att få det att funka,
så vi har ingen input validering eller gjort något större med CSS. För att skapa en spelare så går man Add Player i menyn. 

Så här ser Add player sidan ut:

![image](https://user-images.githubusercontent.com/65369996/134804969-6f73d644-5387-4beb-9753-31922804b698.png)

Efter man lagt till en spelare så blir man skickad tillbaka till startsidan.

Man kan även se vilka som har lagts till i databasen genom att klicka på fliken "View Players" i menyn.
Så här presenterar sidan alla spelare:

![image](https://user-images.githubusercontent.com/65369996/134805007-04c8f97b-6da1-469c-a9cc-89d27e76e8ff.png)

### Koden 

Såhär ser strukturen ut för vårt program:

![image](https://user-images.githubusercontent.com/65369996/134805099-c7c1dfe5-589e-4d64-9b2c-abbfde947367.png)

I Models har vi skapat en enda klass "Player" och den ser ut såhär:

![image](https://user-images.githubusercontent.com/65369996/134805118-2dde117c-3cc7-47c4-91ad-eda8e452bdc4.png)

I mappen "Services har vi en klass och ett interface. 
Klassen heter CosmosDbService och ser ut såhär: 

![image](https://user-images.githubusercontent.com/65369996/134805184-f7052c65-336a-4923-a719-6447863fd2ed.png)

Denna klassen skapar anslutningen till databasen och sparar även data samt läser in data från databasen .

Interfacet "ICosmosDbService: 

![image](https://user-images.githubusercontent.com/65369996/134805230-23bdb85f-3073-48ec-aeb3-65064a29d421.png)

För att kopplingen ska funka till databasen, har vi även fått lägga in connectionsträngen i appsettings.json.

![image](https://user-images.githubusercontent.com/65369996/134805371-185bd1ef-f99a-46de-880d-ac9fecb573b2.png

Här får man fylla i vilken url som databasen är uppkopplad till och även en key som jag valt att dölja i detta sammanhang, även om det kanske inte spelar så stor roll.
Man får även fylla i vad databasen heter som man har skapat i Azure portal och även namnet på containern. 

I Startup.cs filen så har vi även fått lägga till dessa rader, för att också skapa kopplingen till databasen med dependency injection:

![image](https://user-images.githubusercontent.com/65369996/134805495-2fb3680a-b69b-4393-aaa4-e5ca0d14cbe3.png) 

Sen har vi även fått lägga till denna metoden, för att ovanstående ska funka:

![image](https://user-images.githubusercontent.com/65369996/134805524-924acdda-8f79-45d8-8f27-5472f7f6862f.png)

Från rad 69-75 på ovanstående bild, så behövde vi lägga in de raderna för att kunna spara en spelare, när man klickar på knappen "Add Player". 
Vi hittade denna lösningen, då inget annat funkade. Tyvärr vet jag inte exakt varför det funkar, men det löste i alla fall problemet. 

För att skapa innehållet på sidan, så har vi skapat två olika "Razor pages", Create och Viewplayer. 

Create.cshtml.cs ser ut såhär:

![image](https://user-images.githubusercontent.com/65369996/134805626-656ab16f-2b1b-4637-ad83-8b733bd51b3d.png)

Och Create.cshtml filen kommer nedan: 

![image](https://user-images.githubusercontent.com/65369996/134805654-f8d0bff4-2a07-4da1-b761-6c160359c9b2.png)

Create.cshtml.cs tar hand om det man fyller i formuläret på hemsidan och sparar det i vår Cosmos databas och
Create.cshtml renderar UI:t för användaren. 

Vi har motsvarande för att kunna visa spelarna också och det funkar på samma sätt, fast att metoden i ViewPlayer.cshtml.cs istället
skriver ut datan från databasen. 

![image](https://user-images.githubusercontent.com/65369996/134805732-e83c4ef3-17c9-4389-9200-f540a980ef4c.png)

ViewPlayer.cshtml:

![image](https://user-images.githubusercontent.com/65369996/134805753-12ff8779-5c31-4b8d-866d-1ef33e5211e9.png)

I denna filen, så loopar vi igenom alla spelare i databasen och för varje spelare, så skapas en ny cell/rad i tabellen. 


### Hur har vi fått programmet att köra i Azure app service?

I mitt förra inlägg med databaser, så skapade jag en databas i molnet och det var grundstenen för detta programmet. 
Istället för att använda apiet från förra programmet, så har jag istället skapat en annan model, "Player" som jag vart inne på tidigare.
I och med det, så har jag skapat en ny container med namnet "Players". Det var första steget för att koppla samman databasen med detta programmet. 

Sedan har vi helt enklet bara "deployat" appen till azure genom att klicka på deploy to web app som bilden nedan visar:

![image](https://user-images.githubusercontent.com/65369996/134805957-a8fc043e-c8c8-4c83-8218-0ea4dbedd980.png)

Man har följt några få steg där man väljer namnet på sidan. Mycket mer än så var det inte. 

## Kostnaden 

Ett program med få användare:

![image](https://user-images.githubusercontent.com/65369996/134637482-339e71c7-5ec1-4d53-b498-8d8b6c08561e.png)

Så skulle månadskostnaden bli ca $23 i månaden. 

Med en stor mängd användare: 

![image](https://user-images.githubusercontent.com/65369996/134637676-5e893f40-cda8-410c-81ba-10e0e459cc71.png)

Här blir kostnaden ca $2350 i månaden. 


### Referenser


[MVC-Wepapp med CosmosDB](https://docs.microsoft.com/sv-se/azure/cosmos-db/sql/sql-api-dotnet-application)

[Razor pages Tim Corey](https://www.youtube.com/watch?v=68towqYcQlY)

[Deploy ASP.NET web app](https://docs.microsoft.com/en-us/azure/app-service/quickstart-dotnetcore?tabs=netcore31&pivots=development-environment-vs)










