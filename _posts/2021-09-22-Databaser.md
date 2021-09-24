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








