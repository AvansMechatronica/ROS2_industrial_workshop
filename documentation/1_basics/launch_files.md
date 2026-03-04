# ROS2 Launch files

In de opdrachten van `ROS2 topics` en `ROS2 services` hebben we al gezien hoe we nodes kunnen starten vanuit de command line. Maar wat als we meerdere nodes tegelijk willen starten? Dan kunnen we gebruik maken van launch files.

In de launch file `assignment1_2.launch.py` van de package `range_sensor` (in de map `launch`) zijn al een aantal nodes gedefinieerd. Deze nodes worden automatisch gestart wanneer we de launch file uitvoeren.

Dit zijn de nodes die worden gestart:
- `sensor_info_publisher`: Deze node simuleert een afstandssensor en publiceert de gemeten afstand op het topic `sensor_info`.
- `box_height_meters`: Deze node publiceert de hoogte van de doos in meters op het topic `box_height`.

Deze nodes heb je gemaakt in de opdrachten van `ROS2 topics`.

Om de launch file uit te voeren, gebruik je het volgende commando in de terminal:

```bash
ros2 launch range_sensor assignment1_2.launch.py
```

Wanneer je dit commando uitvoert, zullen beide nodes automatisch starten en zullen ze de respectievelijke topics blijven publiceren totdat je de launch file stopt (met Ctrl+C).
    
Je kunt de output van de nodes bekijken in de terminal waar je de launch file hebt uitgevoerd. Je zult zien dat beide nodes actief zijn en hun berichten blijven publiceren.

Je kunt in een andere terminal ook de nodes die gestart zijn bekijken met het volgende commando:

```bash 
ros2 node list
``` 

Natuurlijk kun je ook de topics bekijken die worden gepubliceerd:
```bash
ros2 topic list
```

## Opdracht 1: Uitbreiding van het launch bestand
Breid het 'assignment1_2.launch.py' bestand uit met de node die je hebt gemaakt in `ROS2 services`   
:::
{tip}
Gebruik als voorbeeld de nodes die al in het launch bestand staan. Je kunt deze nodes kopiëren en aanpassen voor jouw nieuwe node.
:::

## Opdracht 2: Testen
Start de launch file en controleer of alle nodes correct worden gestart. Gebruik de terminal om te controleren of de topics worden gepubliceerd en of de service correct werkt. Je kunt ook gebruik maken van `rqt_graph` om de communicatiestromen tussen de nodes te visualiseren.

