# semanticHomeMenu

[Screenshot]

# About
The semanticHome project will give you an unique and easy to setup UI on mobile devices to control your openHAB installation. It is the openHAB 4 successor of the "main_widget" project.
The project is divided into a top level widget (semanticHomeMenu), and some equipment specific second level widgets (_Light, _ColorLight, _DimmableLight, _Rollershutter, RadiatorControl, _Security, _Energy).
It is also possible to use the second level widgets standalone or to extend the project with further widgets your own, some innspiration will be given later.

# History
A openHAB 4 specific version became necessary because we identified some strong performance issues in "main_widget" due to the heavy usage of the oh-repeater componente, which are used to gather all semantic information needed to reduce configuration commplexitiy.

# Structure
The top level widget will show you three diferent part (blocks):
_TopNavigationBar_
The TopNavigationBar will give you three entries when starting:
- Home
  - The Home menu will show you a specific ButtonNavigationBar including Security, Scenes, Appliances and Energy
- Floors
  - The Floors menu will read all your floors from the semantic model and present them in a second row as a swipeable list.
- Rooms
  - The Rooms menu is the same like the Floors Menu, but for the rooms. Selecting the Rooms menu without selecting a particular floor will give you an unfiltered list of all rooms available in your model.
   
_BodyBlock for specific widgets_
- This block is used to show you the specific widgets which will be explained in their own readme's.
  
_BottomNavigationBar_
This block will show you two different navigaion menus, depending on yhour choice of pressing Home or Rooms/Floors
 

# Installation
Prerequisite for using this project is a well maintained semantic model and a strict naming scheme for several items. Best thing is not to create items individually but always use the "create equipment from Thing" option in main UI. All second level (equipment) widgets will include Group and Item examples for textual import. 
Next step will be to install the top level "semanticHomeModel" widget from the Marketplace and then to create a new page in MainUI which will hold just one widget, the "semanticHomeMenu" widget. This page needs some stylesheet tweaks, so please use the following code for it:
[page code snippet]

- If you want a specific ordering in the floors and/or rooms menu, please add the widgetOrderIndex as metadata to your items in the model.

Example for textual item import
```csv
Group   Attic           "Attic"                     <attic>                             ["Attic"]           {widgetOrder="1"}
Group   FirstFloor      "FirstFloor"                <firstfloor>                        ["FirstFloor"]      {widgetOrder="2"}
Group   GroundFloor     "GroundFloor"               <groundfloor>                       ["GroundFloor"]     {widgetOrder="3"}
Group   Cellar          "Cellar"                    <cellar>                            ["Basement"]        {widgetOrder="4"}

Group   Office          "Office"                    <office>            (Attic)         ["Room"]            {widgetOrder="1"}
Group   Guest           "Guestroom"                 <suitcase>          (Attic)         ["Bedroom"]         {widgetOrder="2"}
Group   CorridorFF      "Corridor Firstfloor"       <corridor>          (FirstFloor)    ["Corridor"]        {widgetOrder="3"}
Group   Childroom       "Childroom"                 <bedroom_blue>      (FirstFloor)    ["Bedroom"]         {widgetOrder="4"}
Group   Bathroom        "Bathroom"                  <bath>              (FirstFloor)    ["Bathroom"]        {widgetOrder="5"}
Group   Bedroom         "Bedroom"                   <bed>               (FirstFloor)    ["Bedroom"]         {widgetOrder="6"}
```
The weather widget shown in the screenshot above can be found in the community:
[forecast widget]
[actual weather widget]
To use these widgets, the following prerequisits apply [unless you are comfortable to tweak the code yourself] :
[weather prerequisits]

Next would be to install the other widgets from the marketplace:
- Security
- SecurityKeypad
- Energy
- Light
- DimmableLight
- ColorLight
- Rollershutter
- RadiatorControl
- HVAC
- timepicker [please note, for openHAB, the timepicker widget needs to be tweaked  in line xxx

## Screenshots

## Changelog

### Version 0.1
- initial release for openHAB 4

## Resources
