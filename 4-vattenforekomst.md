# För visning av en vattenförekomst
När man klickar på prick på kartan.

Även här så hämtar jag en rätt stort objekt med all data jag behöver. För att t ex inte behöva hämta ny data om besökaren väljer att titta på en annan variabel i vattenförekomsten.

````http request
GET /api/vattenforekomst/12345
````

````jsonc
{
  "id": 12345,
  "namn": "N m Hallands kustvatten",
  "område": "Kattegatt",
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
      "avrundning": 2, // Olika variabler kan visas med olika många värdesiffror. 
      "viss_id": "DIP"
    }
    ...
  },
  "statusar": { // En för varje variabel
    "328": { // En för varje miljöövervakning
      "1": {
        "status": 1,
        "p_värde": 4.243,
        "median": 1.435,
        "bästa_station": 785
      },
      ...
    },
    ...
  },
  "stationer": { // En per station
    "785": {
      "namn": "Glommens fiskehamn",
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
    ...
  }
}
````
Jag väljer många gånger att använda object istället för listor det gör att jag när jag redan vet vilken variabel och miljöövervakning som är vald, så kan jag lättare hämta värden utan att behöva filtrera fram rätt värde ur en lista:
````php
# PHP

// Värden från ett filter.
$selected_station_id = 785;
$selected_variable_id = 328;
$selected_data_model = 1;

$serie = $data["stationer"][$selected_station_id]["mätningar"][$selected_variable_id][$selected_data_model];
````
Och har då direkt listan.

I annat fall så behöver jag hela tiden filtrera ut värden från listor och då blir det snabbt väldigt repetitivt och många fler rader. 
