# Custom Traffic System for FS22

The mod Custom Traffic System enables you to load your own custom traffic system regardless of which map you are playing, without the need to edit the map files.

You can include traffic system vehicles from the base game, maps and even create your own custom vehicles. All this works globally without changing any existing mods. The benefit of this is that your traffic system will be portable between maps and save games (you can even have different traffic systems on multiple savegames on the same map) and it will work even if you update the map.


## USAGE:
1. Rename the file `disabled_customTrafficSystem.xml` to `customTrafficSystem.xml`, the file is found in the `modSettings/FS22_000_CustomTrafficSystem` folder found in your `MyDocuments/MyGames/FarmingSimulator2022` folder.
2. Edit the `<vehicle filename="..." />` XML nodes with your custom traffic (a copy of a default car from the base game is included as an example)
3. Add references to the vehicles you want to include in your traffic system 
4. Enable the mod and enjoy!

See sections below for further details. 


## ADDING NEW VEHICLES:
To add a vehicle to your custom traffic system, all you need to do is refernece the XML file of the vehicle (see section below how to find these) to your `customTrafficSystem.xml` file. 

Add a vehicle node (<vehicle />) to the <vehicles /> section for each vehicle you want to include in your custom traffic system. Make sure the path in the filename attribute is relative to the `customTrafficSystem.xml` or an absolute path (typically `$data/vehicles/cars` for base game vehicles). 

If you want to include the base game vehicle 'vehicle_04' as well as a custom 'fireTruck' you created yourself, the 'customTrafficSystem.xml' could look like this:
    <trafficSystem>
        <vehicles>
            <vehicle filename="$data/vehicles/cars/vehicle_04/vehicle_04.xml" probability="1" probabilityParked="1"/>
            <vehicle filename="myCars/fireTruck.xml" probability="1" probabilityParked="1" />
        </vehicles>
    </trafficSystem>

Ensure that the paths in your custom vehicles (e.g. the fire truck) is relative to the 'customTrafficSystem.xml' file.


## SAVEGAME SPECIFIC CUSTOM TRAFFIC:
1. Make a copy of the 'customTrafficSystem.xml'
2. Rename the copy to 'customTrafficSystem_savegameX.xml' (where X is the number of the savegame, i.e. a number bwtween 1 and 20)
3. Edit the 'customTrafficSystem_savegameX.xml' with your savegame specific settings
4. Repeat step 1-3 for each savegame as needed (if no `customTrafficSystem_savegameX.xml` is found, the generic `customTrafficSystem.xml` will be used)


## ENABLE CUSTOM TRAFFIC ONLY FOR A SPECIFIC SAVEGAME:
You can of course just disable the mod, but you can also rename the 'customTrafficSystem.xml' to 'disabled_customTrafficSystem.xml' and keep the 'customTrafficSystem_savegameX.xml' files.


## EXTRACTING VEHICLES FROM MAPS:
a) Locate the traffic system XML file to find references to the vehicles
b) Copy the XML, I3D and texture for each vehicle into your CustomTrafficSystem folder
c) Add <vehicle /> nodes to your `customTrafficSystem.xml`

### A) Locate traffic system:
Typically a map stores its XML files in a subfolder called 'maps' and the vehicle system is usually in a file name 'trafficSystem.xml'. 

If you cannot find the traffic system XML file directly, open the 'map.i3d' and look for the node that represents the traffic system (typically a transform group name something similaer to "trafficSystem"). On that node you will find a user attribute named 'xmlFile', that is the path to the traffic system XML file.

### B) Copy I3D, XML and textures
In the traffic system XML you will find references to the vehicles (<vehicle /> nodes) used in that traffic system. E.g. for the base game US map you can find this line:
```xml
<vehicle filename="$data/vehicles/cars/vehicle_04/vehicle_04.xml"        probability="1" probabilityParked="1"/>
```

If you want to use this specific vehicle in your custom traffic system, copy the `vehicle_04.i3d.shapes`, `vehicle_04.i3d.shapes` and `vehicle_04.xml` to your CustomTrafficSystem folder (`modSettings/FS22_000_CustomTrafficSystem` folder found in you `MyDocuments/MyGames/FarmingSimulator2022` folder).

Note: If you want to use base game vehicles as in the example above, you only need to reference it in the 'customTrafficSystem.xml' file (no need to copy the files), this is due to these files is always awailable regardless of which map you load.

### C) Add vehicles to the custom traffic system:
For each vehicle you copied in step B, add a vehicle node (<vehicle />) to the <vehicles /> section in the 'customTrafficSystem.xml' file. Make sure the path in the filename attribute is relative to the 'customTrafficSystem.xml'. 

E.g. if you copied the base game 'vehicle_04' to a subfolder called 'US' in the custom traffic system folder, the 'customTrafficSystem.xml' should look like this:
```xml
    <trafficSystem>
        <vehicles>
            <vehicle filename="US/vehicle_04.xml" probability="1" probabilityParked="1" />
        </vehicles>
    </trafficSystem>
```

When you copy the XML file from a map, ensure that the filename attributes of the <assets /> nodes is relative to the 'customTrafficSystem.xml' (and not your 'YOUR_VEHICLE.xml') file, e.g. if you copied the 'vehicle_04' to the subfolder 'US' the 'vehicle_04.xml' file should look like this (the '$data/vehicles/cars/vehicle_04/' path is replaced with 'US/'):
    <assets filename="US/vehicle_04.i3d" filenameParked="US/vehicle_04.i3d" driverNode="3">

