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
For complete usage of this project, you need to create some groups (equiments) in your semantic model, see the following example for textual item import (change to your individual needs).
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
269
```

For some group items of the security widget, you might not have member items. You should still make the group items, otherwise you'll receive a lot of log entries like `[WARN] ... Attempting to send a state update of an item which doesn't exist: gDoorsOpen`.
These categories will be invisible in the security widget though, as long as the state of the empty group items is `0.0`. That is the state that openHAB gives to empty group items. However, it's possible this doesn't happen immediately, so you might want to update these states yourself (e.g. in the console with command `openhab:update gBlindsOpen 0.0`).
```
Group:Number:COUNT(ON)        gSmokeAlarm                                   "Smokealarm"                     <smoke>
Group:Number:COUNT(ON)        gBatteryLow                                   "Empty Batteries"                <lowbattery>
Group:Number:COUNT(OPEN)      gWindowsOpen                                  "Windows Open"                                         
Group:Number:COUNT(OPEN)      gDoorsOpen                                    "Doors Open"                                           
Group:Number:COUNT(ON)        gMotionDetected                               "Motion Detected"                                      
Group:Number:COUNT(ON)        gCamerasDetecting                             "Cameras Detecting something"                          
Group:Number:COUNT(ON)        gBlindsOpen                                   "Blinds open"                                          
```
All these items will create the general structure shown in the top navigation menu and will also create the red notification badges in the bottom navigation bar.

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
