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

# Services


Start add two ints service server:

```
ros2 run demo_nodes_py add_two_ints_server
```

Edit add two ints server code:
```
gedit /opt/ros/jazzy/share/launch_testing_ros/examples/add_two_ints_server.py
```

Vraag een lijst van services op:
```
ros2 service list
```

Vraag informatie op over een service:
```
ros2 service info /add_two_ints
```

Vraag informatie op over een service interface:
```
ros2 interface show example_interfaces/srv/AddTwoInts
```


Roep de service aan vanaf de command line:

```
ros2 service call /add_two_ints example_interfaces/srv/AddTwoInts "{a: 1, b: 2}"
```

Edit add two ints client code:
```
gedit /opt/ros/jazzy/share/launch_testing_ros/examples/add_two_ints_client.py
```

Roep de service aan vanaf een node:
```
ros2 run demo_nodes_py add_two_ints_client
```

# Action Servers
On request

# Launch Files
On request





**Under Construction**