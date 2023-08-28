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

The Menu is split into multiple specialized widgets that are shown if the model contains the needed data.

* [HomeMenu]
* [semanticHomeMenu]
* [Security widget]
  * including the [Keypad widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Security.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/SecurityPinPad.jpg)
* [Scenes widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Scene.jpg)
* [Lights widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/SwitchableLight.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/DimmableLight.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/ColorLight.jpg)
* [Rollershutter widget]

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Rollershutter.jpg)
  * including the [Time Picker](https://community.openhab.org/t/time-picker/118865)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/RadiatorControl.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/HVAC_dark.jpg)
* The weather widget shown in the screenshots can be found in the community
  * [Actual weather](https://community.openhab.org/t/oh3-main-ui-examples/117928/22)
  * [Weather forecast](https://community.openhab.org/t/oh3-main-ui-examples/117928/30)
  
## Community
Please check [openHAB community]for discussions and proposals.

