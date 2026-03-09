# ROS2 industrial manipulation Planning

In deze module leer je hoe je een robotarm kunt besturen met behulp van ROS2. We gebruiken de UFactory xarm6 robotarm in combinatie met een vacuum grijper. Je gaat leren hoe je de moveit setup uit voorgaande module kunt gebruiken om een programma te schrijven dat de robot naar verschillende poses kan bewegen. Daarnaast leer je hoe je de robot naar een specifieke positie kunt laten bewegen die gerefereerd is aan de basis van de robot, wat handig is voor het oppakken van objecten.

We beginnen met het verkennen van de virtuele omgeving
```bash
ros2 launch manipulation view_environment.launch.py
```

## Opdracht 1
In deze opdracht leer je hoe je met een programma de robot kunt aansturen naar een van de poses die je in de setup assistant hebt aangemaakt.

open het bestand:
```
~/ros2_industrial_ws/src/ROS2_industrial/4_manipulation/manipulation/manipulation/assignment1.py
```
Opmerking: dit is een python script, dat je in de toekomst al template voor je eigen programma's kunt gebruiken.

Open het bestand en bestudeer de code.

Pas alleen de volgende functie in het python script aan
```python
def execute_pose(self):
```

In deze functie laat je de robot naar een opgegeven pose laten bewegen die je in de setup assistant hebt aangemaakt. Je kunt hiervoor de functie def move_to_state(self, state_name: str):
```python
move_to_state(self, state_name: str)
```
aanroepen met als parameter de naam van de pose, bijvoorbeeld:
```python
self.move_to_state("my_pose_name")
```

Zorg dat de robot naar de "home" pose beweegt wanneer het programma wordt gestart. Je kunt dit testen door het programma uit te voeren met het volgende commando:
```bash
ros2 run manipulation assignment1
```

Maak het programma zo dat de robot achtereenvolgens naar de volgende poses beweegt:
* Home
* Left
* Right
* Home
* Resting

Plaats je code in de opdracht bij Todo 1 in het python script.

:::{tip}
Zorg ervoor dat je programma zo compact mogelijk is door het gebruik van de "for ... in ...:" syntax van Python.
:::

## Opdracht 2
In deze opdracht leer je hoe je de robot naar een positie kunt laten gaan die gerefereerd is aan de basis van de robot. Dit is handig wanneer je een object wilt oppakken dat zich op een bepaalde positie bevindt ten opzichte van de robot.

je kunt daarvoor de volgende functie gebruiken:
```python
self.move_to_pose(translation, rotation)
```
In deze functie geef je de gewenste positie van het end-effector op in de vorm van een translation (x, y, z) en een rotation in quaternion (x, y, z, w). De translation geeft de positie van het end-effector aan ten opzichte van de basis van de robot, en de rotation geeft de oriëntatie van het end-effector aan.

Vul het programma uit opdracht 2 aan zodat de robot naar de volgende posities beweegt:

* translation = (0.4, -0.4, 0.25) met een rotation = (1.0, 0, 0.0, 0.0)

Plaats je code in de opdracht bij Todo 2 in het python script.

Test het programma en kijk hoe de robot beweegt. 

Het zal je opvallen dat de gripper niet goed georiënteerd is ten opzichte van de tafel. Pas de rotation aan zodat de grijper is gericht naar de tafel, zodat deze een object kan oppakken dat op de tafel ligt.

Gebruike de volgende functie om de rotatie van de gripper aan te passen:

```python
rotation_quaternion = tf_transformations.quaternion_from_euler(roll, pitch, yaw)
```

:::{tip}
Denk zoveel mogelijk in roll, pitch en yaw hoeken, en gebruik de functie quaternion_from_euler om deze om te zetten naar een quaternion. De roll, pitch en yaw hoeken worden gegeven in radians.
* 90 graden is gelijk aan pi/2 radians
* 180 graden is gelijk aan pi radians
* 360 graden is gelijk aan 2*pi radians.
:::
