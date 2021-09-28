



### Inledning

I denna uppgift så ska vi övertyga vår CTO att modernisera vår applikation.
Den nuvarande applikationen använder bara interna servrar och resurser och 
jobbar med klassificierad data som är oerhört viktigt för företaget att ingen obehörig kommer åt. 

CTO vill inte använda som av en molnlösning, för att hen vill ha full kontroll på datan över internet. 
I detta inlägg kommer jag därför förklara vad VPC(Virtual Private Cloud) och vad Azure Private Link är. 



### Vad är Azure Private Link? 

Private link möjliggör åtkomst till kundvärdar och tredjepart tjänster över en private endpoint i vårt virtuella nätverk.
Det möjliggör verkligen att få en privat anslutningserfarenhet mellan tjänster och virtuella nätverk.

Azure privat link ger Azure tjänsterna på insidan av kundernas egna VNet. 
Tjänsternas resuerser kan nås genom att använda en privat IP-adress, precis som alla andra resuser i VNet. 
Detta förenklar nätverkskonfigurationen genom att behålla åtkomst reglerna privata. 

Nätverkstrafiken mellan ditt virtuella nätverk och tjänsterna går genom Microsofts egna huvudledsnätvärk.
Att din känsliga data inte exponeras över ett publikt nätvärk är inte längre nödvändigt. 
Man kan skapa sitt egen privat link tjänst i sitt egna virtuella nätverk och leverera det till kunderna. 


<strong> Azure Private Link Service</strong>

Azure private link service är en referens till vår egna tjänst som drivs av Azure private link. Vår tjänst som kan köras bakom Azure Standard Load Balancer kan
bli aktiverad för Privat Link access så att konsumenter till vår tjänst kan komma åt det privat från deras egna Vnets. 
Våra konsumenter kan alltså skapa en privat endpoint inuti deras VNet och kartlägga det till denna tjänsten(Azure Private Link). 

<strong> Azure Private Endpoint </strong>

Azure private endpoint är ett nätverksgränssnitt som ansluter oss privat och säkert till en tjänst som drivs av Azure private link. 
Azure private endpoint använder sig utav en privat IP-adress från vårt VNen och effektivt ger tillgång till tjänsten till vårt VNet.
Tjänsten kan vara allt ifrån en Azure service, såsom Azure storage, Cosmos DB, SQL eller vårt egna. 


### Fördelar med Azure Private Link

<strong>Global räckvidd</strong>
Anslut till tjänster runt hela världen - Det ansluts privat till tjänsterna som körs i andra regioner än sin egna. 
Konsumentens virutella nätverk kan vara i Region A och kan anslutas med tjänsterna bakom en Private Link i Region B.


<strong>Kom åt tjänsterna privat på Azure platformen</strong>
Anslut vårt virtuella nätverk till tjänser hos Azure utan en publik ip-adress från källan eller destinationen. 
Tjänsteleverantörerna kan framställa deras tjänster i deras egna virtuella nätverk och konsumenterna kan komma åt dessa tjänster
i deras lokala virtuella nätverk. 

<strong>Skydd mot Data läckage</strong>
En privat endpoint är kartlagd till en instans av en Platform as a Service(Paas) resurs istället för en hel tjänsten. 
Konsumenterna kan bara ansluta till den specifika resursen. Åtkomst till alla andra resurser i tjänsten är blockerad. 
Denna mekanismen ger skydd mot data läckage risker. Det är inte längre nödvändigt till att skapa åtkomstrestriktioner som Service endpoints. 

### Vad är Virtual Private Cloud (VPC)?
Ett virtuellt privat moln är säkert, isolerat privat moln som är hostad inom ett publikt moln. 
VPC kunder kan köra kod, spara data, "hosta" webbsiodr och kan göra allt som det normalt kan i ett vanligt
privat moln, men det privata molnet är "hostat" avlägset av en leverantör av ett publikt moln. 
VPC kombinerar skalbarheten och övertygelsen från ett publik moln med dataisloreing av ett privat moln. 

<strong>Skillnaden mellan ett privat och publikt moln</strong>

I ett publikt moln så är det delad moln infrastruktur. Många olika konsumenter av molnleverantören använder sig / kommer åt
samma infrastruktur, men datan är inte delad - precis som alla ordrar från en restaurang som är tillagad i samma kök, 
så är inte alla ordrar likadana. Detta kallas inom detta område för "Multitenancy".
Publika molnleverantörer inkluderar AWS, GCP, och Microsoft Azure. 


Ett privat moln är däremot "single-tenant". Ett privatmoln är en molntjänst som är exklusivt erbjudet till en organisation. 
VPC, är ett privat moln inuti ett privat moln och ingen annan delar VPC med VPC-kunden. 


### Fördelar med VPC

<strong>Bättre prestanda</strong>

Moln-hostade webbsidor och applikationer brukar prestera bättra än de som är hostade på lokala servers. 

<strong>Bättre säkerhet</strong>

De offentliga molnleverantörerna som erbjuder VPC har ofta fler resurser för att uppdatera och underhålla infrastrukturen, särskilt för små och medelstora företag.
För stora företag eller företag som står inför extremt hårda datasäkerhetsbestämmelser är detta en mindre fördel.

<strong>Skalbarheten</strong>

VPC är hostad av en publik leverantör och därför kan kunderna lägga till mer dataresurser efter begäran/behov. 

[What is VPC?](https://www.cloudflare.com/learning/cloud/what-is-a-virtual-private-cloud/)

[Azure Private Link](https://docs.microsoft.com/da-dk/azure/private-link/private-link-overview )

[Azure Private Link Overview](https://medium.com/awesome-azure/introduction-to-azure-private-link-andprivate-endpoint-and-private-link-service-a61be184356e)

[Azure networking - Private link](https://www.youtube.com/watch?v=PWKM5KXjWno)
