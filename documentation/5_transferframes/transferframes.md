# ROS2 Industrial Transferframes

In deze opdracht gaan we werken met transfer-frames. We gebruiken een robotarm in een gesimuleerde omgeving (Gazebo) om objecten op te pakken en te verplaatsen. De robotarm is uitgerust met een vacuum-grijper die objecten kan vastpakken. Er is een camera aanwezig die de positie van de objecten kan detecteren en doorgeven aan de robotarm.

Je kunt de virtuele omegving starten met de volgende commando:

```bash
ros2 launch transferframes environment.launch.py 
```
Je zult zien dat Gazebo en RVIZ wordt. In de omgeving zie je een robotarm, een tafel en een camera.

Met de camera kunnen we de positie van objecten detecteren. De camera is gepositioneerd boven de tafel en kijkt naar beneden. De camera stuurt de gedetecteerde objectposities, na het nemen van een foto, door naar een ROS2-topic genaamd `/ros_industrial/sensors/custom_logical_camera/objects`. Dit topic bevat de coördinaten van de objecten in de wereld.

Let op: De camera is een zo gnaamde "logical camera". Dit betekent dat het geen echte beelden of foto's maakt, maar in plaats daarvan de posities van objecten in de wereld doorgeeft. Dit is handig voor simulaties omdat het eenvoudiger is dan het verwerken van echte beelden.

Je kunt objecten op de tafel plaatsen door het volgende commando uit te voeren:

```bash
ros2 launch transferframes spawn_parts.launch.py
```
 Je ziet ze nu verschijnen op de tafel in Gazebo, maar nog niet in RVIZ. Dit komt omdat de objecten nog geen frames hebben.

 Door het nemen van een foto met de camera, worden de objecten gedetecteerd en krijgen ze frames toegewezen. Dit gebeurt automatisch wanneer de camera een foto neemt. Je kunt dit doen door het volgende commando uit te voeren:

```bash
ros2 run ros_industrial_sensors take_photo.py
```

In Rviz kun je nu de frames van de objecten zien. Elk object krijgt een uniek frame toegewezen, zoals `object_1`, `object_2`, etc. Deze frames geven de positie en oriëntatie van de objecten in de wereld aan.

gebruik het volgende commando om de frames te bekijken:

```bash
ros2 run tf2_tools view_frames 
```
dit commado genereert een PDF-bestand genaamd `frames_<date>_<time>.pdf` in de huidige map. Open dit bestand(via de project-explorer) om de hiërarchie van frames te bekijken.

Sluiten van Gazebo en RVIZ doe je met Ctrl-C in de terminal waar je het gestart hebt.


### 5.1 Moveit2 setup
De robot configuratie kun je vinden in de package transferframes_moveit_config. 
1. Open de setup_assistant
2. Voeg een extra robot-pos toe met de naam "drop", de pose moet zo zijn dat de gripper boven de bak hangt.
3. Sla de configuratie op, zorg ervoor dat aleen het srdf-bestand wordt overschreven.

In deze opdrachten maak je de code in het python script "assignment1.py" van de package transferframes af. Het script is al gedeeltelijk ingevuld met TODO x's waar je de code moet aanvullen.

### 5.2 Pas het programma aan met het maken van een foto
* Vul in de TODO 1's in het python script "assignment1.py" van de package transferframes.
Maak een foto met de volgende code:

```python
result, photo = self.camera.take_photo()
```
Deze functie geeft twee waarden terug:
- `result`: Dit is een boolean (True of False) die aangeeft of het maken van de foto succesvol was.
- `photo`: Dit is een lijst van objecten die door de camera zijn gedetecteerd. Elk object in de lijst bevat informatie zoals de naam, positie en oriëntatie.

Druk deze lijst vervolgens af met behulp van de volgende functie:
```python
self.get_logger().info()
```

### 5.3 Maak de basis robot bewegingen

### 5.4 Beweeg naar de opjecten

### 5.5 Pak de objecten op en laat ze in de bak vallen

### 5.6 Verbeter je programma
Maak een functie zoals hier beschreven.
``` Python
def move_to_object(self, part, z_offset = 0.0):
    pass
```

Extra opmerkinge:
De gripper is al in de class X gimplementeerd



## Commando's
Under contruction



[![PickAndPlace Demo](https://img.youtube.com/vi/-zZXw-iZUTo/0.jpg)](https://www.youtube.com/watch?v=-zZXw-iZUTo "PickAndPlace Demo")

Bekijken van de omgeving
```bash
ros2 launch transferframes view_environment.launch.py
```

Starten bestaande moveit-configuratie met setup assistant
```bash
ros2 launch transferframes_moveit_config setup_assistant.launch.py 
```

```bash
ros2 launch ros_industrial_gazebo spawn_parts.launch.py
```

```bash
ros2 launch ros_industrial_gazebo spawn_part_random.launch.py
```

starten opdracht 1
```bash
ros2 run transferframes assignment1 
```

view-frames
```bash
ros2 run tf2_tools view_frames
```
Daarna pdf openen via project navigator