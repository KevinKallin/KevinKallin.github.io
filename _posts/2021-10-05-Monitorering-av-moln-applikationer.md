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

Det första man måste göra för att få detta att funka är att lägga till denna kodraden inne i startup-filen:

![image](https://user-images.githubusercontent.com/65369996/136066582-1e3eb6c5-95d2-4c41-9e57-a7ad98129388.png)
 
Det är för att App insights ska kunna mäta alla request och liknande som görs i applikationen. 
För att App insights också ska fungera, så ska man aktivera det inne i Azure portalen. 

![image](https://user-images.githubusercontent.com/65369996/136067022-51a55816-8043-4add-b4cd-374417ee9efc.png)


När man sedan trycker på "View Application Insights data, så kommer man även vidare till en sida där man kan hitta
sin instrumental key, som är viktigt att lägga in i appsettings filen i programmet, för att koppla programmet till rätt resurs på Azure.

![image](https://user-images.githubusercontent.com/65369996/136067370-0a448a51-d2fb-4dcc-8cce-ee379539da9b.png)

* Har valt att dölja nyckeln på bilden för att ingen obehörig ska komma åt den. 










