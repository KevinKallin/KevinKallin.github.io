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
Det går även att ändra så att det även sparas i sitt eget storageaccount på Azure, men då måste en inställning i app.settings göras 
och det kommer jag visa lite senare. 

Först får man trycka på Add files i menyn :

![image](https://user-images.githubusercontent.com/65369996/135588422-8f881f85-47d9-46bc-8cbf-aaf5dea045c5.png)

Då kommer man till sidan där man kan lägga till eller radera en fil. Som vi ser i bilden nedan, så har jag redan lagt till då filer. 
Det skapas ett nytt id för varje bild och har även en länk. För stunden så kan man inte se bilderna på sidan och inte heller via länken
men är något jag ska fixa senare.

![image](https://user-images.githubusercontent.com/65369996/135588711-10162827-b998-452e-a077-0e126307a347.png)

Trycker man på Add blob så kommer denna rutan upp:

![image](https://user-images.githubusercontent.com/65369996/135589038-69a53190-4385-42c8-a553-08d2a2472c86.png)

Trycker man på välj fil så kommer man in på "Den här datorn > bilder" 

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

  
  





  
  

  


