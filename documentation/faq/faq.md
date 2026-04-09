# Veel gestelde vragen (FAQ)

In deze sectie vindt u antwoorden op veelgestelde vragen over ROS2 en de workshop. 

## Wanneer moet ik `colcon build` gebruiken?
Het `colcon build --symlink-install` wordt alleen gebruikt voor de volgende situaties:
* Er zijn bestanden aan een ROS2 package toegevoegd
* Er is een nieuwe ROS2 package gemaakt
* De inhoud van een `C` of `C++` bestand is gewijzigd
* De inhoud van de setup.py van een Python package is gewijzigd
* De inhoud van `package.xml` of `CMakeLists.txt` is gewijzigd

Na de build dien je altijd het volgende commando in `alle openstaande` terminals uit te voeren:
```
source ~/my_ur_ws/install/setup.bash
```

## Hoe kan ik een onherstelbare fout die ik in een bestand heb gemaakt terugdraaien? 
Omdat de workshop is opgezet met behulp van Git, kunt u eenvoudig teruggaan naar een vorige versie van een bestand. Gebruik het volgende commando in de terminal:
```
git checkout -- <bestandsnaam>
``` 
:::{caution}
Als je het bestand al gecommit hebt, moet je eerst de commit ongedaan maken voordat je terug kunt gaan naar een vorige versie van het bestand. Gebruik hiervoor het volgende commando:
```
git reset --hard HEAD~1
```
Doe dit in de directory van het bestand dat je wilt terugdraaien.
:::

## Waar kan ik meer informatie vinden over ROS2 commando's en Linux commando's?
Er zijn verschillende cheat sheets beschikbaar die u kunnen helpen bij het snel opzoeken van belangrijke commando's en concepten. Bekijk de [Cheat sheets](../references/cheatsheets/cheatsheets.md) voor meer informatie.