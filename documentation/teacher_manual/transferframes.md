# Transferframes


## Demo van transferframes
```bash
ros2 launch manipulation environment_w_gazebo.launch.py
```

Enable TF in RVIZ.

Disable RobotModel & MotionPlanning in RVIZ om de transferframes goed zichtbaar te maken.(doe dat bijvoorbeeld tijdens een beweging van de robot)

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

