# Är en variabel relevant
Används i rapporter för att ta reda på om länkar skall skapas till kartan.

Låt säga att man är på denna sidan: https://www.sverigesvattenmiljo.se/sa-mar-vara-vatten/2021/variabelgrupper/85/0/64

Man har alltså valt att titta på rapporten om variabelgruppen "Vattnets egenskaper"
Och sedan valt vattenmiljön "Kust och öppet hav".

Lite längre ner så får man du en lista där man kan se olika variabler på kartan, eller bara läsa mer om olika variabler.

Vilka variabler som visas kommer ifrån att varje variabel har en lista med vilka vattenmiljöer som den är relevant för.
T ex Säl är bara relevant för vattenmiljön "Kust och öppet hav".

Utöver om den är relevant för vald vattenmiljö, så visas bara variabeln om:
        Det finns en "fakta"-sida om variabeln t ex den här sidan om Siktdjup: https://www.sverigesvattenmiljo.se/undersoka-vattenmiljo/siktdjup
    och / eller
        Det finns data för variabeln i vald vattenmiljö

Det här som detta anropet kommer in.

_Jag behöva veta vilka variabler som tillhör variabelgruppen "Vattnets egenskaper" och som har data för någon stationer/vattenförekomster/bedömningsområden i hela vattenmiljön "Kust och öppet hav"._

Så jag tänker mig att jag hämtar detta så här:
````http request
GET https://api/relevanta-variabler?variabelgrupp=23&vattenmiljo=1
````
Och förväntar mig att få tillbaka ett svar i JSON format, som är en lista över variabel id t ex:
````json
[1, 5, 23, 178]
````

Samma förfrågan skall man istället kunna göra där man istället skickar med ett område:

_Vilka variabler som tillhör variabelgruppen "Vattnets egenskaper" och som har data för någon stationer/vattenförekomster/bedömningsområden i hela området "Skagerrak"._

````http request
GET https://api/relevanta-variabler?variabelgrupp=23&omrade=14
````
Och förväntar mig att få tillbaka ett svar i JSON format, som är en lista över variabel id t ex:
````json
[23, 178]
````

Mer data än så behöver jag inte få tillbaka för att kunna veta om länkarna skall skapas eller inte.
Namn på variabeln eller liknade har jag redan tillgång till.
