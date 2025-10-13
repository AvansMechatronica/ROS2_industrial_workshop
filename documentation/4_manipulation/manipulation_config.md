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

