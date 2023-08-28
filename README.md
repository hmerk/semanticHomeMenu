# semanticHomeMenu
Repository for colaboration in the semanticHomeMenu project

## Vision / About
The idea is to have a UI for [openHAB4](https://www.openhab.org/) that dynamically  configures itself automatically using the data of the [openHAB semantic model](https://www.openhab.org/docs/tutorial/model.html#semantic-model).

It is also possible to use the specialized widgets standalone or to extend the project with further widgets your own, some inspiration will be given later.

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Startscreen.jpg)

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
