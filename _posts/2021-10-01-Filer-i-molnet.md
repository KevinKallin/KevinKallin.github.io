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


