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
ros2 run demo_nodes_cpp talker
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

## Packages
```
ros2 pkg list
```

## Workspace map structuur
```
cd ~/ros2_industrial_ws
tree -d
```

```
tree -d -L 2
```

## Packages map structuur
```
cd ~/ros2_industrial_ws/src/ROS2_Industrial
tree -d
```


**Under Construction**