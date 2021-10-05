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

![image](https://user-images.githubusercontent.com/65369996/136061301-96968751-597a-4950-b070-daff3c4ff7be.png)

I samband med detta felmeddelandet, så skapas även ett exception som registreras i Appinsights. Kommer visa ett exempel längre ner i detta inlägg. 

### Ett enklare diagram över programmet

![image](https://user-images.githubusercontent.com/65369996/136065886-655cb8cc-08d8-41c4-bff8-3c3455caeae8.png)

### Beskriv koden för loggimplementationen 

