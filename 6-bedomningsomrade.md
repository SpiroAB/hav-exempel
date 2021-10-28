#För visning av ett bedömningsområde

````http request
GET https://api/bedomningsomrade/1234
````

````json
{
  "id": 785,
  "namn": "Glommens fiskehamn",
  "vattenmiljö": "Kust och öppet hav",
  "variabler": { // En per variabel
    "328": {
      "namn": "Lättillgänglig fosfor",
      "enheter": { // En per vattenmiljö
        "84": "µg/l",
        "85": "µmol/l",
        "150": "µg/l"
      },
      "beskrivning": "Årsmedelvärden för vinterhalter av oorganisk fosfor, mätt i µmol/l. Oorganisk fosfor är halten fosfor som finns löst i vattnet och som är tillgängligt för upptag av växtplankton och bakterier.",
      "avrundning": 2,
      "viss_id": "DIP"
    }
    ...
  }
  "statusar": { // En för varje variabel
    "328": { // En för varje miljöövervakning
      "1": -1,
      "2": 0
    },
    ...
  },
  "mätningar": { // En för varje variabel
    "328": { // En per miljöövervakning
      "1": [ // En per år i serien
        {
          "år": 1994,
          "värde": 0.3875,
          "trend": 0.3661396,
          "std_fel": 0.1240622,
          "antal": 4
        }
        ...
      ]
    },
    ...
  }
}
````
