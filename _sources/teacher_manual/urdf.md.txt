# URDF

**Under Construction**

:::{caution}
Verwijder COLCON_IGNORE voor aanvang van de demonstratie ut de pacakge `urdf_demo` in de workspace. En bouw de workspace opnieuw. Vergeet niet om na het bouwen de workspace opnieuw te sourcen.
:::

## URDF Demo
```bash
ros2 launch urdf_demo view_demo.launch.py
```
### Uitvoeing van de demo
Voeg vanuit het soultion.urdf.xacro bestand aan het demo.urdf.xacro bestand in stappen toe toe:

#### Mounting plate link
```xml
  <link name="mountingplate_link">
    <visual>
      <origin xyz="0 0 0.0" />
      <geometry>
        <box size="0.6 0.6 0.024" />
      </geometry>
      <material name="red"/>
    </visual>
  </link>
```
#### Mounting plate joint
```xml
  <joint name="mountingplate_joint" type="fixed">
    <origin xyz="-0.4 0.0 0.042" />
    <parent link="baseplate_link" />
    <child link="mountingplate_link" />
  </joint>
```
#### Base link
```xml
  <link name="base_link" />
```

#### Base link joint
```xml
  <joint name="base_link_joint" type="fixed">
    <parent link="mountingplate_link" />
    <child link="base_link" />
    <origin xyz="0.0 0.0 0.01" rpy="0.0 0.0 0.0"/>
  </joint>
```

#### Fanuc robot macro include
```xml
  <xacro:include filename="$(find fanuc_robots)/urdf/lrmate200ic.urdf.xacro"/>
  <xacro:fanuc_lrmate200ic prefix="robot_"/>
```

#### Robot base joint
```xml
  <joint name="robot_base_joint" type="fixed">
    <parent link="base_link" />
    <child link="robot_base_link" />
    <origin xyz="0.0 0.0 0.0" rpy="0.0 0.0 0.0"/>
  </joint>
``` 

#### Enable Joint State Publisher
verwijder het commentaar van de volgende regel in de view_demo.launch.py
```python
    # Nodes started by this launch file.
    nodes_to_start = [
        #joint_state_publisher_node,
        robot_state_publisher_node,
        rviz_node,
    ]
```

#### Vaccuum gripper include
```xml
  <xacro:include filename="$(find ros_industrial_support)/urdf/vacuum_gripper/vacuum_gripper.urdf.xacro"/>
  <xacro:vacuum_gripper_urdf prefix="vacuum_gripper_" joint_prefix="vacuum_gripper_joint"/>
```

#### Gripper to robot joint
```xml
  <joint name="gripper_to_robot" type="fixed">
    <parent link="robot_tool_link" />
    <child link="vacuum_gripper_base_link" />
  </joint>
```

## Xacro
```bash
ros2 run urdf_tutorial xacro_demo -d demo.urdf.xacro
``

## Checking the URDF
```bash
ros2 run urdf_tutorial check_urdf -d demo.urdf.xacro
```

## URDF Solution
```bash
ros2 launch urdf_demo view_solution.launch.py
```

