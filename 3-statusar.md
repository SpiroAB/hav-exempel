#Vilka statusar har alla vatten
Hämtar alla kartprickar för stationer/vattenförekomster/bedömningsområden, med kopplingar till vilka vattenmiljöer / områden dom finns i.

Används för att som sagt rita ut prickarna på kartan, men även för att kunna dölja / visa dom beroende på valda filter.
````http request
GET https://api/statusar
````

Förväntat resultat är GEO-JSON:

````json
[
  {
    "type": "Feature",
    "geometry": {
      "type": "Point",
      "coordinates": [
        18.20619,
        60.49112
      ]
    },
    "properties": {
      "name": "Öregrundsgrepen",
      "entity_type": 1,
      "entity_id": 12345,
      "variables": { // En per variabel
        "23": {
          "id": 23,
          "data_model": { // En per miljöövervakning
            "1": 0,
            "2": -1
          }
        },
        ...
      ],
      "water_environments": [ 1 ],
      "regions": [ 12, 13 ],
      "data_model": [ 1, 2 ]
    }
  }
  ...
]
````
Det är alltså en lista med ett objekt för varje punkt.
Från objektet sen så kan man se vilka vattenmiljöer/områden och miljöövervakning som pricken är synlig för.
Samt vilken färg pricken får beroende på vald variabel och vald miljöövervakning.

Det är ganska stor lista på ca 500kb data (utan komprimering) 67kb (med gzip).

Man skulle kunna tänka sig att dela upp den så här istället för att slippa det här med entity_id och entity_type:

````json
{
  "vattenförekomster": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          18.20619,
          60.49112
        ]
      },
      "properties": {
        "name": "Öregrundsgrepen",
        "id": 12345,
        "variables": { // En per variabel
          "23": {
            "data_model": { // En per miljöövervakning
              "1": 0,
              "2": -1
            }
          },
          ...
        ],
          "water_environments": [ 1 ],
          "regions": [ 12, 13 ],
          "data_model": [ 1, 2 ]
        }
      }
    }
  ],
  "stationer": [
    ...
  ],
  "bedömningsområden": [
    ...
  ]
}
````
