# Vilka variabler är valbara i kartfiltret
Snarlikt till föregående exempel. Beroende på vad man väljer för filter i kartan så vill jag bara att man skall kunna välja variabler som har data.

_(Dessa två kan man säkert slå ihop till en gemensam)_

Saker man kan filtrera på:
* Miljöövervakning (All / Nationell)
* Vattenmiljö
* Område

Idag hämtar jag en lista en gång över hela strukturen över när olika variabler är relevanta:

````http request
GET /api/relevanta-variabler
````

Förväntat svar är:
````jsonc
{ // En per variabel
  "23": {
    "vattenmiljöer": [ 1, 2 ],
    "områden": [ 1, 2, 3, 4, 5, 6, 7 ],
    "miljöövervakning": [ 1, 2 ]
  },
  "178": {
    "vattenmiljöer": [ 1 ],
    "områden": [ 2, 6, 7 ],
    "miljöövervakning": [ 2 ]
  },
  ...
}
````
Men anropet skulle lika gärna kunna vara med lite parametrar, och att det då görs ett anrop varje gång man gör ett val filtret och då blir istället anropet som i den första filen:
````http request
GET /api/relevanta-variabler?vattenmiljo=1&omrade=12&miljoovervakning=2
````

Förväntat resultat:
````json
[23, 178]
````
Fördelen med att hämta all data direkt är att datan då redan finns innan man börjar filtrera och man behöver då inte vänta på ett svar mellan varje val.
