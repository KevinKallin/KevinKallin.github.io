---
layout: post
title: "Filer i molnet"
date: 2021-10-01 10:03:00
tags: Filer AzureStorageEmulator 
--- 

### Inledning

I denna uppgift så skulle vi lägga till filer i molnet genom att göra det lokalt med Azure Storage Emulator eller Azurite. 
Jag valde att köra på Azure Storage Emulator. 

### Beskrivning av applikationen

Vi har gjort en MVC-app där man kan lägga till / ta bort filer. När man lägger till en fil, så sparas det i emulatorn. 
Det går även att ändra så att det även sparas i sitt eget storageaccount på Azure, men då måste en inställning i app.settings göras.

Först får man trycka på Add files i menyn :

![image](https://user-images.githubusercontent.com/65369996/135588422-8f881f85-47d9-46bc-8cbf-aaf5dea045c5.png)

Då kommer man till sidan där man kan lägga till eller radera en fil. Som vi ser i bilden nedan, så har jag redan lagt till då filer. 
Det skapas ett nytt id för varje bild och har även en länk. För stunden så kan man inte se bilderna på sidan och inte heller via länken
men är något jag ska fixa senare. 

Ovanstånede sker bara när jag kör via emulatorn, använder jag connectionstringen och hämtar in bilderna
från azure protal, så funkar länken att klicka på och bilden som finns tillagd visas och ser ut så här:

![image](https://user-images.githubusercontent.com/65369996/135756119-529731b9-6270-41c2-8431-0ecf55ac3203.png)


![image](https://user-images.githubusercontent.com/65369996/135588711-10162827-b998-452e-a077-0e126307a347.png)

Trycker man på Add blob så kommer denna rutan upp:

![image](https://user-images.githubusercontent.com/65369996/135589038-69a53190-4385-42c8-a553-08d2a2472c86.png)

Trycker man på välj fil så kommer man in på "Den här datorn > bilder" 

### Diagram för dataflödet

![image](https://user-images.githubusercontent.com/65369996/135596630-8522e8d7-c5d6-4755-82cf-583c82754d89.png)

Detta är ett väldigt simpelt diagram, men visar lite för hur flödet är.
I Storageaccountet, så skapar man en container och inuti containern så sparas alla filer.


### Beskriv koden

  <strong>Program som vi installerat</strong
  * Azure Storage Emulator
  * Azure Storage Explorer
  
  Efter att vi har laddat ner ovanstående program, så har man fått starta upp en server på emulatorn, genom att skriva AzureStorageEmulator.exe init /forceCreate i
  emulatorns egna cmd. 
  Då skapas en lokal SQL server upp i bakgrunden.
  
  När väl den är igång så behöver man lägga till detta i app.setting inuti projektet:

  ![image](https://user-images.githubusercontent.com/65369996/135591107-17ed605b-1812-4310-b7cc-0f3d35b71526.png)
  
  Då kommer man åt ett standardkonto som gäller för alla som vill använda som av emulatorn.
  Man kan skriva det på flera olika sätt, men detta tyckte jag var det smidigaste. 
  
  Inuti Azure storage explorer har jag skapat en container som heter "images", vilket ni kan se nedan:
  
  ![image](https://user-images.githubusercontent.com/65369996/135591395-e61d336f-acb9-41ae-aa14-9ec6bb75f9b9.png)
  
  Inne i den containern, sparas alla bilder som vi lägger till i webappen. Om vi tar en närmare titt på det, så är det 
  samma ID:n inne i containern som det är i webappen:
  
  Container: 
  
  ![image](https://user-images.githubusercontent.com/65369996/135591657-df1b8695-e6c1-4e52-87b5-bb4db83a4c9c.png)

  Webapp:
  
  ![image](https://user-images.githubusercontent.com/65369996/135591781-b8a5a06c-f943-433a-89c0-979c2cfdb176.png)
  
  För att detta ska kunna sparas i emulatorn, så har vi behövt skapa upp några klasser:
  
  BlobService:

  ![image](https://user-images.githubusercontent.com/65369996/135592374-d64a3f29-a4ca-4308-ae81-90621d09cbfb.png)
  
  IBlobService:
  
  ![image](https://user-images.githubusercontent.com/65369996/135592471-fa697dd3-8431-4bba-96ac-44bc0a72f7ff.png)
  
  IBlobService är ett interface och det använder vi oss av för att använda oss av dependency injection i startup.cs filen:
  
  ![image](https://user-images.githubusercontent.com/65369996/135592663-ac63f53b-c4e7-4077-ba4a-90e14327c9b6.png)
  
  Det är för att kunna skapa en koppling mellan appen och servern som blobs läggs till / sparas på. 
  
  Vi har även en controller: 
  
  ![image](https://user-images.githubusercontent.com/65369996/135592941-fe7bd985-8a6a-49f0-b628-f0d68107a10b.png)

  För att detta sedan ska visas i appen har vi även skapat två Views med razor syntax,
  en för att visa filerna och skapa "deleteknappen": 
  
  ![image](https://user-images.githubusercontent.com/65369996/135593162-29dab1f7-4d0f-44c2-936f-3e977ad709e0.png)
  
  Och en för att kunna lägga till filerna:

  ![image](https://user-images.githubusercontent.com/65369996/135593310-50d7b57a-c7b4-4789-b3ee-85d15a763994.png)

  ### Vad skulle det kosta att driva applikationen?
  
  Om vi skulle ha en applikation med 1000 användare och varje användare lägger upp 100mb / dag och som sedan laddas ner 3 gånger varje dag
  så skulle kostnaden bli runt $85. Nedan kommer bild med uträkningen:

  ![image](https://user-images.githubusercontent.com/65369996/135746515-2ccd1beb-a67a-4be6-b813-f6b80e5c3590.png)


  ### Säkerhet för vår blob data
  
  Azure har något som heter "Key Vault". Det är en säker nyckelhantering som är väsentlig för att skydda data i molnet. 
  Man använder denna tjänsten för att kryptera nycklarna och andra hemligheter som lösenord som använder HSM-lagrade nycklar.
  Med denna tjänsten kan inte Microsoft se eller extrahera våra nycklar, med det sagt så är det mycket säkert att använda sig av denna tjänsten. 
  
  ### Referenser
  
  [Key Vault](https://azure.microsoft.com/sv-se/services/key-vault/#product-overview)
  
  [Azure Storage Emulator](https://www.youtube.com/watch?v=gy9V1-mOExo)
  
  [Setting up the Azure Storage Emulator](https://medium.com/oneforall-undergrad-software-engineering/setting-up-the-azure-storage-emulator-environment-on-windows-5f20d07d3a04)
  
  [Azure Storage CRUD](https://www.c-sharpcorner.com/article/azure-storage-crud-operations-in-mvc-using-c-sharp-part-two/)
  

  
  

  


