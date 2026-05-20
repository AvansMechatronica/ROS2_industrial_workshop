# Transferframes


## Demo van transferframes
```bash
ros2 launch manipulation environment_w_gazebo.launch.py
```

Enable TF in RVIZ.

Disable RobotModel & MotionPlanning in RVIZ om de transferframes goed zichtbaar te maken.(doe dat bijvoorbeeld tijdens een beweging van de robot)

### view_frames
```bash
ros2 run tf2_tools view_frames
```

## Demo van maken foto met logic-camera
Open de environment met daarin een logic-camera.(in nieuwe terminal)
```bash
ros2 launch transferframes environment.launch.py
```

Spawn objecten op de tafel(in nieuwe terminal)
```bash
ros2 launch transferframes spawn_part_random.launch.py
```

of

```bash
ros2 launch transferframes spawn_parts.launch.py
```

Neem foto(in nieuwe terminal)
```bash
ros2 run ros_industrial_sensors take_photo.py
```
:::{note}
In een virtuele omgeving moet je soms 2 keer een foto nemen om de TF-frams van de gedetecteerde objecten te zien verschijnen in RVIZ.
:::
Toon de namen van de frames door in RVIZ bij TF de optie "Show Names" aan te zetten. 


### view_frames
```bash
ros2 run tf2_tools view_frames
```
Er wordt een PDF gegenereerd met daarin een overzicht van alle frames en hun onderlinge relaties. In deze PDF kun je de frames van de gedetecteerde objecten terugvinden, evenals hun relatie tot andere frames in het systeem. De pdf staat in de map waar je het commando hebt uitgevoerd.

### Tonen van specefiek transfer in terminal
```bash
ros2 run tf2_ros tf2_echo base_link tool_link
```

:::{note}
Helaas zie ik de frames van de objecten niet verschijnen in tf2_echo. Ik vermoed dat dit komt doordat deze frames alleen zichtbaar zijn in RVIZ en niet in de terminal. Onduidelijk waarom dit het geval is, aangezien de frames wel zichtbaar zijn in RVIZ. Mogelijk heeft dit te maken met de manier waarop de frames worden gepubliceerd of gefilterd in de terminal.
:::
