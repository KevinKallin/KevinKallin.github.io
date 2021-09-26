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
