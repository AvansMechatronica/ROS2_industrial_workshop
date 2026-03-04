# ROS2 Creating packages for Python applications

In deze opdrachten ga je een ROS2 package aanmaken waarin je Python nodes kunt plaatsen. Deze nodes kunnen vervolgens worden gestart met het **ros2 run** commando.

## Opdracht 1: Package aanmaken
Maak een ROS2 package aan genaamd **time_publisher** met de volgende commandostructuur:
```bash
ros2 pkg create --build-type ament_python time_publisher
```
:::{hint}
Voer dit commando uit in de src map van je workspace:
```bash
cd ~/ros2_industrial_ws/src
```
:::


Nadat je dit commando hebt uitgevoerd, zal er een nieuwe map genaamd **time_publisher** worden aangemaakt in de src map van je workspace. Deze map bevat de basisstructuur van een ROS2 package, inclusief een setup.py bestand dat nodig is voor het bouwen van de package.

## Opdracht 2: Python node aanmaken
Maak een Python node aan zoals beschreven is in de opdracht over [ROS2 topics](https://avansmechatronica.github.io/ROS2_industrial_workshop/1_basics/topics.html#opdracht-1-7-tijd-publisher-uitdaging). Plaats deze node in de map **time_publisher/time_publisher**. Zorg ervoor dat je de nodige aanpassingen maakt in de setup.py van de package, zodat de node correct kan worden gebouwd en uitgevoerd.

## Opdracht 3: Bouwen
Bouw de package met **colcon build** 
:::{hint}
1. Voer dit commando uit in de root van je workspace: `~/ros2_industrial_ws`
2. Gebruik de `--symlink-install` optie bij `colcon build`.
:::

## Opdracht 4: Testen
Test of je Python node correct werkt door de node te starten met het **ros2 run** commando. Controleer of de node correct functioneert en of de verwachte output wordt weergegeven in de terminal.

```bash
ros2 run time_publisher time_publisher_node
```
