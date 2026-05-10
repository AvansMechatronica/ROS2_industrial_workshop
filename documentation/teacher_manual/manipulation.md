# Manipulation  


## MoveIt setup assistant
```
ros2 launch moveit_setup_assistant setup_assistant.launch.py
```

Loop door de stappen van de setup assistant. Gebruik de URDF van de robot die je wilt gebruiken. In deze workshop gebruiken we een UR5 robot.
Maak een package aan voor de moveit config van de robot. In deze workshop gebruiken we `demo_moveit_config`. Sla de config op in de src folder van je workspace.

Starten van de demo van de moveit setup assistant:
```
ros2 launch demo_moveit_config demo.launch.py
```

Demostreer de verschillende mogelijkheden van de moveit configuratie. Laat zien hoe je een plan maakt en uitvoert. Laat ook zien hoe je een plan maakt en uitvoert met een object in de omgeving.

Openen van een bestanden moveit config:

```
ros2 launch demo_moveit_config ros2 setup_assistant.launch.py
```

## Demonstratie van manipulatie opdrachten
```
ros2 launch manipulation environment.launch.py
```

### Met gazebo

```
ros2 launch manipulation environment_w_gazebo.launch.py
```

### MoveIt configuratie

```
ros2 launch manipulation_moveit_config setup_assistant.launch.py
```



