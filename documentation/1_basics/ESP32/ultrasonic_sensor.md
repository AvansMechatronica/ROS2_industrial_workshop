# Topics met een ultrasoon sensor

Bij deze opdrachten gaan we aan de slag met een ultrasoon sensor. Met een ultrasoon sensor kun je afstanden meten. In voorgaande opdrachten hebben we deze sensor gesimuleerd. Om een sensor te kunnen gebruiken in ROS2, moet deze eerst worden gekoppeld aan een microcontroller. In dit geval gebruiken we een ESP32 device. Dit device zal vervolgens de data van de ultrasoon sensor publiceren op een ROS2 topic. In deze opdrachten gebruiken we een SFR-04 ultrasoon sensor, maar er zijn ook andere types beschikbaar die vergelijkbare functionaliteit bieden.

Om de koppeling tussen het ESP32 device en ROS2 _jazzy tot stand te brengen, maken we gebruik van microROS. microROS is een implementatie van ROS2 die speciaal is ontworpen voor microcontrollers. Hiermee kunnen we ROS2-functionaliteit integreren in kleine embedded systemen zoals de ESP32.

## Opdracht 1: Installeren en configureren van microROS-agent
Voordat we de ESP32 kunnen programmeren, moeten we ervoor zorgen dat de microROS-agent correct is geïnstalleerd en geconfigureerd op je computer. De microROS-agent fungeert als een brug tussen de microcontroller en het ROS2-ecosysteem, waardoor de data van de ultrasoon sensor kan worden gepubliceerd op een ROS2 topic.

De microROS-agent kan worden geïnstalleerd en geconfigureerd met de volgende stappen:
```bash
mkdir -p ~/microROS_agent_ws/src
cd ~/microROS_agent_ws/src

# Verkrijg de juiste ROS2 distributie
git clone -b jazzy https://github.com/micro-ROS/micro-ROS-Agent.git

cd ..
# Build de microROS agent
colcon build --symlink-install
source install/setup.bash
echo "source ~/microROS_agent_ws/install/setup.bash" >> ~/.bashrc
```


## Opdracht 2: Aansluiten van de ultrasoon sensor op de ESP32
![image](../../images/ESP32/srf-04.jpg)

|    ESP32 Pin     | SFR-04 Pin |
|:----------------:|:----------:|
|        5V        |    VCC     |
|       GND        |    GND     |
| SR04_TRIG_PIN(*) | Trig       |
| SR04_ECHO_PIN(*) | Echo       |

## Opdracht 3: Programmeren van de ESP32 met microROS
Het ESP32 device moet worden geprogrammeerd om de ultrasoon sensor aan te sturen en de gemeten data te publiceren op een ROS2 topic. Hiervoor gebruiken we Visual Code met Platform IO, wat een handige omgeving biedt voor het ontwikkelen van embedded software. In deze stap zullen we de code schrijven die de ultrasoon sensor aanstuurt, de afstand meet en deze informatie publiceert op het ROS2 topic **/sensor_info**.

## Starten van de microROS-agent
Voordat we de ESP32 kunnen testen, moeten we de microROS-agent starten op je computer. Dit is essentieel omdat de agent de communicatie tussen de ESP32 en ROS2 mogelijk maakt. Je kunt de microROS-agent starten met het volgende commando in je terminal:
```bash
ros2 run micro_ros_agent micro_ros_agent udp4 --port 8888
```

## Opdracht 4: Testen van de ultrasoon sensor
Nadat het device is geprogrammeerd kun je de werking controlleren met;
```bash
ros2 topic echo /sensor_info
```

## Opdracht 5: Testen van de ultrasoon sensor in een ROS2 omgeving



In dit voorbeeld wordt een SFR-04 ultrasoon sensor gekoppeld aan den ESP32 device. Nadat deze is geprogrammeerd zal dit device een topic **/sensor_info** publiceren. Met de ultrasoon sensor kun je vervolgens een afstand meten.

## Algemene microROS informatie
Informatie over het installeren van microROS kun je [hier](../../references/microros/microros.md) vinden.

## Openen van een microROS project
Open met Visual Code project van de range-sensor in de volgende map (alleen map selecteren):
```text
~/ros2_industrial_ws/src/ROS2_industrial/1_basics/ESP32/ultrasonic_sensor
```

## SRF-04 aansluiten
 
 (*) Deze pin-aansluitingen (van je gekozen ESP32 device) kun je vinden in het *platformio.ini* bestand:
```bash
gedit ~/ros2_industrial_ws/src/ROS2_industrial/1_basics/ESP32/ultrasonic_sensor/platformio.ini
``` 

{octicon}`alert;2em;sd-text-info` Je dient wel eertst de microROS-agent te starten. 

[Brief instructions programming ESP32 devices with VisualCode/Platform IO](instructions_programming_esp32.md)