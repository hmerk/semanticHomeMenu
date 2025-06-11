# semanticHomeMenu
Repository for colaboration in the semanticHomeMenu project

## Vision / About
The idea is to have a UI for [openHAB4](https://www.openhab.org/) that dynamically  configures itself automatically using the data of the [openHAB semantic model](https://www.openhab.org/docs/tutorial/model.html#semantic-model).

It is also possible to use the specialized widgets standalone or to extend the project with further widgets your own, some inspiration will be given later.

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/semanticHomeMenu.jpg)

## History
An openHAB 4 specific version became necessary because we identified some strong performance issues in "main_widget" due to the heavy usage of the oh-repeater component, which is used to gather all semantic information needed to reduce configuration commplexity.

## Concept idea
This main UI widget is based on a proper configuration of the [openHAB semantic model](https://www.openhab.org/docs/tutorial/model.html#semantic-model). The project aims to show all information automatically - if found in the model - mostly without additional configuration by the user.

To help getting more information about an item we make use of an extention of the semantic model via the [uiSemantics](https://community.openhab.org/t/semantic-ui-using-enriched-semantic-to-ease-ui-creation/116882).

The Menu is split into a Top Navigation Bar,

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots//TopNavbar_unselected.jpg)

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/TopNavbar_selected.jpg)

the Body showing multiple specialized widgets (which are shown if the model contains the needed data) 
and the the Bottom Navigation Bar.

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/BottomNavbar_unselected.jpg)

Bottom Navigation Bar with Scenes selected

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/BottomNavbar_ScenesSelected.jpg)

The red indicator badges are shown if there is any alarm, whether security or low battery. Usage and setup will be explained in the security and energy widget documentation.

* [Security widget]
  * including the [Keypad widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Security.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/SecurityPinPad.jpg)
* [Scenes widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Scenes.jpg)
* [Lights widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/SwitchableLightOff.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/DimmableLightOff.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/ColorLightOff.jpg)
* [Rollershutter widget]

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Rollershutter.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/RadiatorControl.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/HVAC.jpg)
* The weather widget shown in the screenshots can be found in the community
  * [Actual weather](https://community.openhab.org/t/oh3-main-ui-examples/117928/22)
  * [Weather forecast](https://community.openhab.org/t/oh3-main-ui-examples/117928/30)
  
### Usage
For complete usage of this project, you need to create some groups (equiments) in your semantic model, see the following example for textual item import (change to your individual needs)
```csv
Group                         gHome                                         "Home"                                                                                                       ["Building"]
Group                         gIndoor                                       "Building"                       <house>               (gHome)                                               ["Indoor"]
Group                         gOutdoor                                      "Outdoor"                        <garden>              (gHome)                                               ["Outdoor"]
Group                         gAttic                                        "Attic"                          <attic>               (gIndoor)                                             ["Attic"]                          {widgetOrder="11"}
Group                         gCorridorAttic                                "Corridor Attic"                 <corridor>            (gAttic)                                              ["Corridor"]                       {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Corridor", location="Attic"],widgetOrder="12"}
Group                         gOffice                                       "Office"                         <office>              (gAttic)                                              ["Room"]                           {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Office", location="Attic"],widgetOrder="13"}
Group                         gGuestroom                                    "Guestroom"                      <bedroom>             (gAttic)                                              ["Bedroom"]                        {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Guestroom", location="Attic"],widgetOrder="14"}
Group                         gFirstFloor                                   "First Floor"                    <firstfloor>          (gIndoor)                                             ["FirstFloor"]                     {widgetOrder="21"}
Group                         gCorridorFirstfloor                           "Corridor FF"                    <corridor>            (gFirstFloor)                                         ["Corridor"]                       {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Corridor", location="First Floor"],widgetOrder="22"}
Group                         gChildroom                                    "Childroom"                      <boy_1>               (gFirstFloor)                                         ["Bedroom"]                        {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Childroom", location="First Floor"],widgetOrder="23"}
Group                         gBathroom                                     "Bathroom"                       <bath>                (gFirstFloor)                                         ["Bathroom"]                       {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Bathroom", location="First Floor"],widgetOrder="24"}
Group                         gBedroom                                      "Bedroom"                        <bedroom>             (gFirstFloor)                                         ["Bedroom"]                        {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Bedroom", location="First Floor"],widgetOrder="25"}
Group                         gGroundFloor                                  "Ground Floor"                   <groundfloor>         (gIndoor)                                             ["GroundFloor"]                    {widgetOrder="31"}
Group                         gEntrance                                     "Corridor GF"                    <corridor>            (gGroundFloor)                                        ["Corridor"]                       {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Corridor", location="Ground Floor"],widgetOrder="32"}
Group                         gToilet                                       "Toilet"                         <toilet>              (gGroundFloor)                                        ["Bathroom"]                       {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Toilet", location="Ground Floor"],widgetOrder="33"}
Group                         gKitchen                                      "Kitchen"                        <kitchen>             (gGroundFloor)                                        ["Kitchen"]                        {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Kitchen", location="Ground Floor"],widgetOrder="34"}
Group                         gDiningroom                                   "Diningroom"                                           (gGroundFloor)                                        ["DiningRoom"]                     {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Dininroom", location="Ground Floor"],widgetOrder="35"}
Group                         gLivingroom                                   "Livingroom"                     <sofa>                (gGroundFloor)                                        ["LivingRoom"]                     {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Livingroom", location="Ground Floor"],widgetOrder="36"}
Group                         gBasement                                     "Basement"                       <cellar>              (gIndoor)                                             ["Basement"]                       {widgetOrder="41"}
Group                         gCorridorCellar                               "Corridor Basement"              <corridor>            (gBasement)                                           ["Corridor"]                       {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Corridor", location="Basement"],widgetOrder="42"}
Group                         gLaundry                                      "Laundryroom"                    <washingmachine>      (gBasement)                                           ["LaundryRoom"]                    {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Laundryroom", location="Basement"],widgetOrder="43"}
Group                         gBoilerRoom                                   "Boilerroom"                     <heating>             (gBasement)                                           ["BoilerRoom"]                     {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Boilerroom", location="Basement"],widgetOrder="44"}
Group                         gHobbyroom                                    "Hobbyroom"                                            (gBasement)                                           ["Room"]                           {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Hobbyroom", location="Basement"],widgetOrder="45"}
Group                         gGarden                                       "Garden"                         <garden>              (gOutdoor)                                            ["Garden"]                         {widgetOrder="51"}
Group                         gShed                                         "Shed"                           <garden>              (gOutdoor)                                            ["Location"]                       {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Shed", location="Garden"],widgetOrder="52"}
Group                         gTerrace                                      "Terrace"                        <terrace>             (gOutdoor)                                            ["Room"]                           {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Terrace", location="Garden"],widgetOrder="53"}
Group:Number:COUNT(ON)        gSmokeAlarm                                   "Smokealarm"                     <smoke>
Group:Number:COUNT(ON)        gBatteryLow                                   "Empty Batteries"                <lowbattery>
Group:Number:COUNT(OPEN)      gWindowsOpen                                  "Windows Open"                                         
Group:Number:COUNT(OPEN)      gDoorsOpen                                    "Doors Open"                                           
Group:Number:COUNT(ON)        gMotionDetected                               "Motion Detected"
```

### Translatable strings
Most of the labels in the widget are retrieved from items, but there are also some default labels, which are in English. If you want to keep them in English, you can leave the state of the string items below as `NULL`; then the default labels will appear. Technically, they will also appear if you don't create these string items, but then your log will see a lot of entries like this:
```
22:15:13.036 [WARN ] [se.internal.SseItemStatesEventBuilder] - Attempting to send a state update of an item which doesn't exist: semanticHomeMenu_home
```
Add these items:
```
Group                         gSemanticHomeMenu_strings                     "Strings for the semanticHomeMenu"
String                        semanticHomeMenu_home                         "semanticHomeMenu string for 'Home'"                             (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_floors                       "semanticHomeMenu string for 'Floors'"                           (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_rooms                        "semanticHomeMenu string for 'Rooms'"                            (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_security                     "semanticHomeMenu string for 'Security'"                         (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_scenes                       "semanticHomeMenu string for 'Scenes'"                           (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_appliances                   "semanticHomeMenu string for 'Appliances'"                       (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_energy                       "semanticHomeMenu string for 'Energy'"                           (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_system                       "semanticHomeMenu string for 'System'"                           (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_lights                       "semanticHomeMenu string for 'Lights'"                           (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_rollers                      "semanticHomeMenu string for 'Rollers'"                          (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_climate                      "semanticHomeMenu string for 'Climate'"                          (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_batteryAttention             "semanticHomeMenu string for ' batterie(s) need(s) attention'"   (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_batteries                    "semanticHomeMenu string for 'Batteries'"                        (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_armedHome                    "semanticHomeMenu string for 'ARMED HOME'"                       (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_disarmed                     "semanticHomeMenu string for 'DISARMED'"                         (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_armedAway                    "semanticHomeMenu string for 'ARMED AWAY'"                       (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_smokeDetectors               "semanticHomeMenu string for 'Smoke Detectors'"                  (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_motionDetectors              "semanticHomeMenu string for 'Motion Detectors'"                 (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_surveillance                 "semanticHomeMenu string for 'Surveillance'"                     (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_blinds                       "semanticHomeMenu string for 'Blinds'"                           (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_doors                        "semanticHomeMenu string for 'Doors'"                            (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_windows                      "semanticHomeMenu string for 'Windows'"                          (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_noMotion                     "semanticHomeMenu string for 'NO-Motion'"                        (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_motion                       "semanticHomeMenu string for 'MOTION'"                           (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_open                         "semanticHomeMenu string for 'OPEN'"                             (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_closed                       "semanticHomeMenu string for 'CLOSED'"                           (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_alarm                        "semanticHomeMenu string for 'ALARM'"                            (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_ok                           "semanticHomeMenu string for 'OK'"                               (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_on                           "semanticHomeMenu string for 'ON'"                               (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_off                          "semanticHomeMenu string for 'OFF'"                              (gSemanticHomeMenu_strings)
String                        semanticHomeMenu_municipality                 "The name of your municipality"                                  (gSemanticHomeMenu_strings)
```

If you want to use translated labels, update their state e.g. by running a script like this JavaScript code:
```js
var stringarray = [
  ['semanticHomeMenu_home', 'the string of your choice'],
  ['semanticHomeMenu_floors', 'the string of your choice'],
  ['semanticHomeMenu_rooms', 'the string of your choice'],
  ['semanticHomeMenu_security', 'the string of your choice'],
  ['semanticHomeMenu_scenes', 'the string of your choice'],
  ['semanticHomeMenu_appliances', 'the string of your choice'],
  ['semanticHomeMenu_energy', 'the string of your choice'],
  ['semanticHomeMenu_system', 'the string of your choice'],
  ['semanticHomeMenu_lights', 'the string of your choice'],
  ['semanticHomeMenu_rollers', 'the string of your choice'],
  ['semanticHomeMenu_climate', 'the string of your choice'],
  ['semanticHomeMenu_batteryAttention', 'the string of your choice'],
  ['semanticHomeMenu_batteries', 'the string of your choice'],
  ['semanticHomeMenu_armedHome', 'the string of your choice'],
  ['semanticHomeMenu_disarmed', 'the string of your choice'],
  ['semanticHomeMenu_armedAway', 'the string of your choice'],
  ['semanticHomeMenu_smokeDetectors', 'the string of your choice'],
  ['semanticHomeMenu_motionDetectors', 'the string of your choice'],
  ['semanticHomeMenu_surveillance', 'the string of your choice'],
  ['semanticHomeMenu_blinds', 'the string of your choice'],
  ['semanticHomeMenu_doors', 'the string of your choice'],
  ['semanticHomeMenu_windows', 'the string of your choice'],
  ['semanticHomeMenu_municipality', 'the string of your choice']?
  ['semanticHomeMenu_noMotion', 'the string of your choice'],
  ['semanticHomeMenu_motion', 'the string of your choice'],
  ['semanticHomeMenu_open', 'the string of your choice'],
  ['semanticHomeMenu_closed', 'the string of your choice'],
  ['semanticHomeMenu_alarm', 'the string of your choice'],
  ['semanticHomeMenu_ok', 'the string of your choice'],
  ['semanticHomeMenu_on', 'the string of your choice'],
  ['semanticHomeMenu_off', 'the string of your choice'],
]

for (var x = 0; x < stringarray.length; x++) {
  items[stringarray[x][0]].postUpdate(stringarray[x][1])
}
```

The drawback of these string items is that  that their value is changed to `NULL` when openHAB restarts. There are few solutions for this problem:
1. Create a rule that is triggered on a system event (e.g. level 80 (Things initialized)). The code might be the JavaScript code mentioned above.
2. Install and configure [`MapDB` persistence](https://www.openhab.org/addons/persistence/mapdb/) to keep track of the latest value of all member items of `gSemanticHomeMenu_strings`, and have these values restored on openHAB restart.


## Community
Please check [openHAB community]for discussions and proposals.

## Credits
Thanks to 
- @Dimitris for creating the design specs
- @Nic02 for creating the widgets
- @JustinG for his excellent support when we strugled with design and functionality
- @NicoR for his style and code optimizations

and anyone else I have forgotten

## Resources
https://github.com/hmerk/semanticHomeMenu/blob/main/main/semanticHomeMenu.yaml
