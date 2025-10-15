# ROS2 industrial manipulation Pick and Drop

In deze opdrachten gaan we een robotarm gebruiken om object(in dit geval een battery) op te pakken en te verplaatsen naar een andere locatie, in dit geval een bak. 

Je kunt de simualtie omgeving starten met de volgende commando's:

```bash 
ros2 launch manipulation environment_w_gazebo.launch.py
```

Je zult zien dat er naast RVIZ ook Gazebo wordt gestart. Er zit enig verschil tussen de twee omgevingen. Gazebo is een fysische simulator, dus objecten kunnen vallen, rollen, botsen etc. RVIZ is een visualisatie tool en heeft geen fysische eigenschappen.

in gazebo kun je nu een object spawen met de volgende commando's:

```bash
ros2 launch manipulation spawn_battery.launch.py
```

Je ziet nu een battery op de tafel verschijnen in Gazebo. Dit opject is nog niet zichtbaar in RVIZ. Dit komt omdat RVIZ alleen de robot en de omgeving laat zien, maar niet de objecten die in Gazebo zijn gespawnd. We zullen dit later bij de opdrachten van transfeur frames behandelen.
 De Opdracht is in twee delen opgesplitst.
1. Het bewegen van de robot arm naar de battery toe en vervolgens naar de bak.
2. Het daadwerkelijk oppakken van de battery en droppen van de battery in de bak door het aansturen van de vacuum-gripper.

Sluit de simulatie af met CTRL+C in de terminal waar je de simulatie hebt gestart.

## Opdracht 4.1 Verplaatsen van de battery op de tafel naar en bak
In deze opdracht ga je de robot arm bewegen naar de battery en vervolgens naar de bak. Hiervoor kun je gebruik maken van de moveit2 commando's die we in de vorige opdrachten hebben behandeld.

### 4.1.1 Moveit2 setup
De robot configuratie kun je vinden in de package maniplaution_moveit_config. 
1. Open de setup_assistant
2. Voeg een extra robot-pose toe met de naam "drop", de pose moet zo zijn dat de gripper boven de bak hangt
3. Sla de configuratie op, zorg ervoor dat aleen het srdf-bestand wordt overschreven.

### 4.1.2 Pas het prograam aan
De battery staat op de tafel op de volgende positie:
- x: 0.4
- y: -0.4
- z: 0.18

- roll: 3.1415927
- pitch: 0.0
- yaw: 0.0

In quaternion: [1.0, 0.0, 0.0, 0.0]

Deze positie is relatief ten opzichte van de robot basis.

De robot moet de volgende stappen uitvoeren:
1. Beweeg naar de "home" positie
2. Beweeg naar de positie boven de battery (x: 0.4, y: -0.4, z: (0.18 + 0.12))
3. Beweeg naar de positie van de battery (x: 0.4, y: -0.4, z: 0.18)
4. Beweeg terug naar de positie boven de battery (x: 0.4, y: -0.4, z: (0.18 + 0.12))
5. Beweeg naar de "home" positie
6. Beweeg naar de "drop" positie
7. Beweeg terug naar de "home" positie
8. Sluit het programma af

Instructies:
1. Pas het pyhton script "assignament2.py" van de package manipulation aan op de plaatsen van TODO 1.
2. Voeg de "assignament2.py" aan de setup.py van de pacakge manipulation toe zodat deze als een commando kan worden uitgevoerd.
3. Start de simulatie omgeving zoals hierboven beschreven.
4. Run het script met het volgende commando:
```bash
ros2 run manipulation assignament2
```
5. Controleer of de robot de juiste bewegingen maakt. Maak eventueel verbeteringen aan het script. Zodat de bewegingen vloeiend zijn.
6. Verbeter het script door een functie te maken die de bewegingen rond het battery uitvoert. Deze functie moet de volgende parameters hebben:

```python
def move_to_battery(self, pose, z_offset = 0.0):
    # beweeg naar de positie van het battery met z_offset
```


## Opdracht 4.2 Battery oppakken met de vacuum gripper
In deze opdracht ga je de robot arm gebruiken om de battery op te pakken en te verplaatsen. Hiervoor moet je de gripper aansturen. De gripper kan worden aangestuurd door een waarde naar het "/vacuum_gripper/control/enable" te sturen.

Start de simulatie omgeving zoals hierboven beschreven. 

Probeer met de "ros2 topic" commando's informatie te krijgen over de gripper. Belangrijk hierbij is dat je het message type achterhaald.

Pas het script "assignament2.py" aan:
In het script is een al voorbereide class VacuumGripper(Node) gemaakt. Deze class heeft de volgende functies:
- __init__(): initialiseerd de node en de publisher van de gripper
- pull(): stuurt een specefieke waarde het topic van de gripper om deze te activeren
- release(): stuurt een specefieke waarde het topic van de gripper om deze te deactiveren

Voeg aan het script bij de TODO 2's de code aan om: de gripper te laten functioneren.

Test je script en kijk of de robot de battery  oppakt en in de bak laat vallen.

Je kunt altijd een nieuwe battery spawnen met het volgende commando:
```bash
ros2 launch manipulation spawn_battery.launch.py
```

