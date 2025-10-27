# ROS2 Services

![Image](https://docs.ros.org/en/jazzy/_images/Service-SingleServiceClient.gif)


In deze workshop leer je de basis van ROS2 services. De theorie hiervan wordt gedoceerd, maar kun je ook vinden op deze [website van ROS](https://docs.ros.org/en/jazzy/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Services/Understanding-ROS2-Services.html)

In deze workshop ga je de gemeten hoogte van de doos uit de topics workshop omrekenen van meters naar inches. We gebruiken hiervoor het ROS services mechanisme. Deze service is al voorbereid.
Je kunt de service starten met het volgende commando:
```bash
ros2 run range_sensor metres_to_inches_server
```

Om een lijst te verkrijgen van services die actief zijn gebruik je het commando
```bash
ros2 service list
```
Je krijgt nu een list met alle services die actief zijn. Voor deze opdrachten is alleen de service __/metres_to_inches__ van belang. Er zijn nog een aan services aanwezig die beginnen met __/metres_to_inches__ en gevolgd door worden door __service/....__, deze zijn voor ROS2 intern gebruik.

Elke service wordt gedefineerd door een type. Dit type kun je als volgt opvragen:
```bash
ros2 service type /metres_to_inches
```
Ook van de service kun je het protoptype opvragen:
```bash
ros2 interface proto <service_type>
```
Dit prototype, dat de request/response-structuur van de service beschrijft, is gedefinieerd in een servicebeschrijving welke je kunt vinden in het volgende bestand:
**~/ros2_industrial_ws/src/ROS2_industrial/1_basics/range_sensors_interfaces/srv/ConvertMetresToInches.srv**

```bash
gedit ~/ros2_industrial_ws/src/ROS2_industrial/1_basics/range_sensors_interfaces/srv/ConvertMetresToInches.srv 
```
In deze service beschrijving vind je een opdeling in twee delen gescheiden door __"---"___:
* 1e deel: De service-aanvraag (__request__) vereist slechts één parameter:
    * float64 distance_metres
* 2e deel: Parameters die de service na behandeling terug geeft, __response__ genoemd:
    * float64 distance_inches
    * bool success (deze wordt gebruikt om aan te geven dat er tijdens de service-afhandeling geen fouten zijn opgetreden; deze is altijd aanwezig in de response, maar het gebruik en de waarde worden bepaald door de implementatie)

Je kunt de service met een shell-commando testen, zie voorbeeld hieronder

```bash
ros2 service call /metres_to_inches range_sensors_interfaces/srv/ConvertMetresToInches "{distance_metres : 1.0}"
```
## Opdracht
In deze opdracht ga je een service-aanvraag naar de ConvertMetresToInches-service programmeren. 

Je gaat daartoe het Python programma **assignment2.py** bewerken op bepaalde aangeven plaatsen. Zoek in het bestand naar commentaarregels met "Todo x" en voeg de gevraagde code direct onder elke commentaarregel toe.

In dit programma gebeurt er het volgende:
* Er wordt een subscriber aangemaakt op het topic */box_height_info*
* Als er een bericht op het topic wordt ontvangen dan wordt de *self.box_height_callback* geactiveerd
* In de callback wordt een service-aanvraag gemaakt naar de *ConvertMetresToInches*-service door de *send_request(self, metres)* member-fuctie aan te roepen
* In de response van de service-aanvraag is de hoogte in inches verwerkt. Deze wordt vervolgens afgedrukt in een terminal

## Opdracht (Entry point toevoegen)
Om een python programma met het **ros2 run** commando te starten dient het python programma in ros2 geregistreerd te worden. Deze registratie wordt opgenomen in de **setup.py** van een ros package.

Open daartoe het setup.py bestand in de package vn de **range_sensor**
```bash
gedit ~/ros2_industrial_ws/src/ROS2_industrial/1_basics/range_sensor/setup.py 
```

Voeg het entry point van assignment2.py toe aan de **entry_points-->console_scripts** sectie. 
*Tip: Gebruik als voorbeeld assignment1*

Bijvoorbeeld, voeg in setup.py onder 'entry_points' het volgende toe:

Referentie:[Python Packages](https://docs.ros.org/en/jazzy/How-To-Guides/Developing-a-ROS-2-Package.html#python-packages)

Nadat setup.py gewijzigd is moet je de package opnieuw bouwen met **colcon build**:

```bash
cd ~/ros2_industrial_ws/
colcon build --symlink-install
source install/setup.bash
```

*Let op: De laatste regel dien je daarna in ieder openstaand terminal uit te voeren.

## Opdracht(programmeren)
In het bestand **assignment2.py** vind je op een aantal plaatsen een **Todo x**. Vul onder deze regels de code in die in de Todo beschreven is.
* Laat je inspireren door [Writing a simple service and client Python](https://docs.ros.org/en/jazzy/Tutorials/Writing-A-Simple-Py-Service-And-Client.html), met name de secties over het aanmaken van een service client, het versturen van een request, en het verwerken van de response.
Specifiek, implementeer een ROS2 service client met rclpy door:
- Het aanmaken van een client voor de ConvertMetresToInches-service.
- Het aanmaken van een request-object en het instellen van de benodigde parameter(s).
- Het versturen van de aanvraag met send_request (gebruik async als voorbeeld).
- Het afhandelen van de response in een callback, waarbij je de ontvangen waarde afdrukt.

Zie [Writing a simple service and client Python](https://docs.ros.org/en/jazzy/Tutorials/Writing-A-Simple-Py-Service-And-Client.html) voor voorbeeldcode en patronen.
* Laat je inspireren door [Writing a simple service and client Python](https://docs.ros.org/en/jazzy/Tutorials/Writing-A-Simple-Py-Service-And-Client.html)

## Opdracht(testen)
Om het programma te testen dien je achtereenvolgens de volgende node’s te starten

* Uit opdracht over topics

    * Sensor info publisher

    * Box hoogte berekeningen (assignment1.py)

* Deze opdracht (assignment2.py)
