# semanticHomeMenu
Repository for colaboration in the semanticHomeMenu project

## Vision / About
The idea is to have a UI for [openHAB4](https://www.openhab.org/) that dynamically  configures itself automatically using the data of the [openHAB semantic model](https://www.openhab.org/docs/tutorial/model.html#semantic-model).

It is also possible to use the specialized widgets standalone or to extend the project with further widgets your own, some inspiration will be given later.

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/semanticHomeMenu2_dark.jpg)

## History
An openHAB 4 specific version became necessary because we identified some strong performance issues in "main_widget" due to the heavy usage of the oh-repeater component, which is used to gather all semantic information needed to reduce configuration commplexity.

## Concept idea
This main UI widget is based on a proper configuration of the [openHAB semantic model](https://www.openhab.org/docs/tutorial/model.html#semantic-model). The project aims to show all information automatically - if found in the model - mostly without additional configuration by the user.

To help getting more information about an item we make use of an extention of the semantic model via the [uiSemantics](https://community.openhab.org/t/semantic-ui-using-enriched-semantic-to-ease-ui-creation/116882).

The Menu is split into multiple specialized widgets that are shown if the model contains the needed data.

* [HomeMenu]
* [semanticHomeMenu]
* [Security widget]
  * including the [Keypad widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Security_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/SecurityKeypad_dark.jpg)
* [Scenes widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Scene_dark.jpg)
* [Lights widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/SwitchableLight_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/DimmableLight_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/ColorLight_dark.jpg)
* [Rollershutter widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Rollershutter_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/RollershutterExpanded_dark.jpg)
* [RadiatorControl widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/RadiatorControl_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/RadiatorControlExpanded_dark.jpg)
* [HVAC widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/HVAC_dark.jpg)
* The weather widget shown in the screenshots can be found in the community
  * [Actual weather](https://community.openhab.org/t/oh3-main-ui-examples/117928/22)
  * [Weather forecast](https://community.openhab.org/t/oh3-main-ui-examples/117928/30)
  
## Community
Please check [openHAB community]for discussions and proposals.

