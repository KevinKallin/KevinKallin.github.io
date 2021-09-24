---
layout: post
title: "Databaser i molnet"
date: 2021-09-22 23:06:00
tags: Databaser
--- 

### Vad gör vår applikation?

Vi har skapat ett väldigt simpelt api, där man spara ett band med artist till en Cosmos databas.
Det går inte lägga till flera artister till ett band, vilket är dumt men har fokuserat på att få det att funka bara.
Vi har stött på en del problem med detta projekt och till en början så kunde vi inte spara till databasen, därav är apiet väldigt simpelt.

För att lägga till ett band med artist så kan det se ut så här:

![image](https://user-images.githubusercontent.com/65369996/134632316-2bd8f72e-d828-4c74-8f36-e52782583b27.png)

I bodyn så fyller man i band och namn på artisten och vi får då statuskoden 200 OK. 

Man kan även se vilka band som har skapats till databasen genom att köra ett GET request som kan se ut såhär:

![image](https://user-images.githubusercontent.com/65369996/134633337-cf4901ad-f0e4-4df5-b848-ba8e038a461b.png)



### Beskriv koden 

Här är vår kod:

POST Metoden:

![image](https://user-images.githubusercontent.com/65369996/134632618-2d4fe632-d0e3-4334-973c-75caaf27e301.png)

GET Metoden: 

![image](https://user-images.githubusercontent.com/65369996/134633631-bbbb8e76-67bf-4a2e-91c8-a988099256d5.png)

BandModel klassen: 

![image](https://user-images.githubusercontent.com/65369996/134633699-15f380ff-f2da-46f4-974f-1afd07b5f873.png)

Vi har en modell som heter "BandModel" som vi använder oss av för spara data till databasen. 
Klassen har Id som autogeneras varje gång ett band skapas, ett Band som ska vara ett bandnamn och där är kanske namnet på propertyn otydlig
och så har vi artist. 

POST metoden har jag förklarat högst upp och visat med ett exempel hur man gör ett.

Vår GET metod "GetAllBands" hämtar datan från databasen genom en Query ( "SELECT * FROM c" ) vilket innebär att den hämtar in alla band från databasen.
Även här finns ett exempel hur det kan se ut i början av inlägget. 

### Databasen

Databasen skapade vi med Azure extension inne i VS code. 

![image](https://user-images.githubusercontent.com/65369996/134635388-e7cecc9e-5c0b-447b-8548-80398a041cb3.png)

Som på bilden ovan, så går man in och skapar en server och sedan när den skapats så skapar man en databasen genom att högerklicka på namnet som man valde till servern:

![image](https://user-images.githubusercontent.com/65369996/134635611-e1f5a253-cafd-432b-b97f-6732372d3e8a.png)

Det är några till steg med information för att få databasen helt färdigställd, men med brist på tid så hinner jag inte förklara dessa stegen nu.

Databasen döpte vi till my-database och vi har skapat en container inne i Azure portal, som heter my-container. Ännu en gång inga optimala namn, men som jag sagt tidigare, så har prio varit att få ett fungerande api.


### Uppdatering / Ändring av databas

Om jag ska vara helt ärlig, så är det inget jag har tänkt på alls då inte tiden har räckt till. 

### Vad kostar det att driva ?

Ett program med få användare:

![image](https://user-images.githubusercontent.com/65369996/134637482-339e71c7-5ec1-4d53-b498-8d8b6c08561e.png)

Så skulle månadskostnaden bli ca 23$ i månaden. 

Med en stor mängd användare: 

![image](https://user-images.githubusercontent.com/65369996/134637676-5e893f40-cda8-410c-81ba-10e0e459cc71.png)


### Referenser 

[Create Azure function](https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-csharp?tabs=in-process&pivots=programming-runtime-functions-v3)

[Connect Azure Function to Cosmos DB](https://docs.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-cosmos-db-vs-code?tabs=in-process&pivots=programming-language-csharp)

[Beräkna pris för databas](https://azure.microsoft.com/en-us/pricing/calculator/)













