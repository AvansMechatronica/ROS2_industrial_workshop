# ROS2 industrial manipulation

In deze module leer je hoe je een robotarm kunt besturen met behulp van ROS2. We gebruiken de UFactory xarm6 robotarm in combinatie met een vacuum grijper.

We beginnen met het verkennen van de virtuele omgeving
```bash
ros2 launch manipulation view_environment.launch.py
```

## Opdracht 1
In deze opdracht ga je een nieuwe MoveIt configuratie aanmaken voor de robotarm.

Voordat we de robot kunnen besturen, moeten we een aantal configuratie bestanden aanmaken met behulp van de MoveIt Setup Assistant. Deze bestanden bevatten informatie over de robot, de omgeving en de bewegingen die de robot kan maken.


https://moveit.picknik.ai/main/doc/examples/setup_assistant/setup_assistant_tutorial.html

Je kunt een nieuwe configuratie aanmaken met het volgende commando:
```bash
ros2 launch moveit_setup_assistant setup_assistant.launch.py
```

Vervolgen kies je Create New MoveIt Configuration Package en selecteer je het urdf-bestand van de robot:

```
/home/student/ros2_industrial_ws/src/ROS2_industrial/4_manipulation/manipulation/urdf/environment.urdf.xacro
```
En kies je Load Files.
Nu wordt het urdf-bestand van de robot ingeladen en zie je aan de linkerkant het robot-model.

Rechts staan de verschillende onderdelen van de configuratie die je kunt aanpassen. Voor deze workshop is het voldoende om alleen de volgende onderdelen aan te passen:
* Self-Collisions:
    * Lees de "Optimize Self-Collision Checking" instructies
    * Klik op "Generate Collision Matrix"
    * Bestudeer de gegenereerde matrix door op de verschillende items te klikken
* Virtual Joints (optioneel):
    * Voeg een virtual joint toe tussen de "world" en de "base_link" van de robot, gebruik de Add Virtual Joint knop
    * Kies als type "fixed"
* Planning Groups:
    * Maak een nieuwe planning group aan met de "Add Group" knop
    * Kies als type "Joint Model Group"
    * Geef de groep een naam, bijvoorbeeld "xarm6"
    * Kies voor Kinematic Solver: "kdl_kinematics_plugin/KDLKinematicsPlugin"
    * Kies voor Group Default Planner: "RRTConnect"
    * Voer "Add Kin. Chain" uit
    * Selecteer de "base_link" als Start Link
    * Selecteer de "vacuum_gripper1_suction_cup" als End Link
    * Klik op "Save"
* Robot Poses:
    * Maak een nieuwe 3 poses aan met de Pose Names "Home", "Left", "Right" aan door de "Add Pose" knop
    * Stel de joint waarden in voor elke pose door de sliders te gebruiken
    * Klik op "Save"
* End Effectors:
    * Dit wordt gebruikt om de grijper te definiëren, maar is voor deze workshop niet strikt noodzakelijk
* Passive Joints:
    * Doe niets, deze robot heeft geen passive joints
* ros2_control URDF Modifications:
    * Doe niets, deze robot heeft geen ros2_control componenten
* ROS 2 Controllers:
    * Kies "Auto Add JointTranjectryController Controllers For Eacch Planning Group"
* MoveIt Controllers:
    * Kies "Auto Add MoveItSimpleControllerManager For Each ROS2 Controller"
* Perception;
    * Doe niets, we gebruiken geen perceptie in deze workshop
* Launch Files:
    * Zorg ervoor dat alle Launch Files zijn geselecteerd
* Author Information:
    * Vul je naam en e-mailadres in
* Configuration Files:
    * Selecteer Configuration Save Path:
```
    /home/student/ros2_industrial_ws/src
```
    * Klik op "Generate Package"
    * Sluit de MoveIt Setup Assistant af    
Je hebt nu een nieuwe MoveIt configuratie aangemaakt. Deze bevindt zich in de volgende directory:
```
/home/student/ros2_industrial_ws/src/workshop_moveit_config
```

Alvorens de nieuwe configuratie te gebruiken, moet je de de package bouwen met colcon build en velvolgens de omgeving opnieuw sourcen:
```bash
cd ~/ros2_industrial_ws
colcon build --symlink-install
source install/setup.bash
```
Je kunt de configuratie bewerken met het volgende commando:
```bash 
ros2 launch workshop_moveit_config setup_assistant.launch.py (dit werkt helaas niet altijd)
```

Voor de volgende opdrachten gebruiken we een al voorbereide MoveIt configuratie.

Je kunt deze configuartie bewerken met het volgende commando:
```bash
ros2 launch manipulation_moveit_config setup_assistant.launch.py 
```
Aandachtspunten:
* De MoveIt configuratie is gebaseerd op de urdf.xacro file in de manipulation package
* De MoveIt configuratie is gebaseerd op de planning group "arm" die de kinematic chain van "base_link" tot "link_eef" bevat 
* Pas in de confugratie alleen de volgende onderdelen aan:
    * Self-Collisions
    * Configuration Files, zorg ervoor dat alleen het volgende bestand geselecteerd zijn:
        * config/manipulation_environment.srdf.
        Let op: De andere bestanden zijn niet correct geconfigureerd en kunnen problemen veroorzaken.

Bestudeer de "Robot Poses" in de setup assistant. Deze poses worden gebruikt in de opdrachten. Voeg eventueel extra "eigen" pose toe. De poses worden opgeslagen in het bestand:
```
config/manipulation_environment.srdf
```
van de manipulation package.
Bestudeer dit bestand, je kunt hier ook handmatig poses aan toevoegen.

## Opdracht 2
In deze opdracht leer je hoe je de configuratie kunt testen in een gesimuleerde omgeving met rviz.      
Start de gesimuleerde omgeving met het volgende commando:
```bash
ros2 launch manipulation environment.launch.py
``` 
Met de knoppen in de rviz interface kun je de robot bewegen naar de verschillende poses die je in de setup assistant hebt aangemaakt. Selecteer de juiste planning group (bijvoorbeeld "xarm6") en vervolgens een Goal State (bijvoorbeeld "Home", "Left" of "Right"). Klick vervolgens op Plan om te kijken hoe de robot beweegt. Met Execute kun je de beweging uitvoeren. Je kunt Plan en Execute ook combineren door op Plan and Execute te klikken.

Ook kun je ook zelf een doelpositie selecteren door op de robot te klikken en deze te verslepen.

Wanneer een fysieke robot met het systeem is verbonden, kun je de bewegingen ook op de echte robot uitvoeren.

## Opdracht 3
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

Zorg ervoor dat je programma zo compact mogelijk is door het gebruik van de "for ... in ...:" syntax van Python.


## Commando's
Under contruction

![image](https://control.ros.org/rolling/_images/ros2_control_overview.png)


![image](https://control.ros.org/rolling/_images/ros2_control_mobile_manipulator_control_arch_multi_robots_in_one_controller_manager.png)
Bekijken van de omgeving
```bash
ros2 launch manipulation view_environment.launch.py
```

Starten nieuwe moveit-configratie in setup assistant
```bash
ros2 launch moveit_setup_assistant  setup_assistant.launch.py
```

Starten bestaande moveit-configuratie met setup assistant
```bash
ros2 launch manipulation_moveit_config setup_assistant.launch.py 
```

## Opdracht 1
Maken nieuwe moevit configuratie
Testen nieuwe moveit configuratie




## Opdracht 1
```bash
ros2 launch manipulation environment.launch.py
```

starten opdracht1
```bash
ros2 run manipulation assignment1 
```
## Opdracht 2
```bash
ros2 launch manipulation environment_w_gazebo.launch.py
```
```bash
ros2 launch manipulation spawn_battery.launch.py
```


```bash
ros2 run manipulation assignment2
```
