# ROS Basics

## ROS Nodes

Lijst van ROS commando's:
```
ros2 <enter>
```

Lijst van ROS nodes:
```
ros2 node list
```
Start een talker node:
```
ros2 run demo_nodes_py talker
```

Start een listener node:

```
ros2 run demo_nodes_py listener
```

Vraag een lijst van nodes op:
```
ros2 node list
```

Vraag informatie op over een node:
```
ros2 node info /talker
```

Uit de volgende opdracht in een nieuwe terminal:
```
ros2 run rqt_graph rqt_graph
```

## ROS Packages
```
ros2 pkg list
```

## ROS Workspace map structuur
```
cd ~/ros2_industrial_ws
tree -d
```

```
tree -d -L 2
```

## ROS Packages map structuur
```
cd ~/ros2_industrial_ws/src/ROS2_Industrial/1_basics/range_sensor
tree -d
```

## Demo van history commando
```
history
```

# ROS Topics

## Talker
Start een talker node:
```
ros2 run demo_nodes_py talker
```
### ROS2 Topics
Lijst van ROS2 topics:
```
ros2 topic list
```
Afdrukken van de data van een topic:
```
ros2 topic echo /chatter
```
Informatie over een topic:
```
ros2 topic info /chatter
```

Edit talker code:
```
gedit /opt/ros/jazzy/share/launch_testing_ros/examples/talker.py
```

## Listener
Start een listener node:
```
ros2 run demo_nodes_py listener
```
Node list:
```
ros2 node list
```

Topic list:
```
ros2 topic list
```

## Demo Sensor publisher

Start een sensor info publisher node:
```
ros2 run range_sensor sensor_info_publisher_simulation 
```

Topic list:
```
ros2 topic list
```

Topic echo:
```
ros2 topic echo /range_sensor_info
```

Topic info:
```
ros2 topic info /range_sensor_info
```

# Interfaces

Start een sensor info publisher node:
```
ros2 run range_sensor sensor_info_publisher_simulation 
```

Topic list:
```
ros2 topic list
```

Topic echo:
```
ros2 topic echo /range_sensor_info
```

Message type info:
```
ros2 interface show range_sensor_msgs/RangeSensorInfo
```

Interface list:
```
ros2 interface list
```

Interface list met filter:
```
ros2 interface list | grep Range
```

Interface show:
```
ros2 interface show sensor_msgs/Range
```






**Under Construction**