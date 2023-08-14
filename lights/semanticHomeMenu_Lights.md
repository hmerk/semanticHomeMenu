![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/SwitchableLight_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/DimmableLight_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/ColorLight_dark.jpg)

The Lights widget card used by main_widget will show all kind of lights equipment in a selected room and show controlls based on equipment group members.

## Usage

All lights need to have their own Group (**Group->Equipment->Lightbulb**), even they just have a Switch Item.

- Equipment Group
  - Type: Group
  - Category: light od lightbulb (not used)
  - Semantic Class: Lightbulb
- Switch Item
  - Type : Switch
  - Category: light or lightbulb (not used)
  - Semantic Class: Point
  - Semantic Property: Switch

For a dimmable or color light, the following Items can be configured.
- Dimmer Item (Brightness)
  - Type: Dimmer
  - Category: slider
  - Semantic Class: Point
  - Semantic Property: None
- Color Item (Color control)
  - Type: Color
  - Category: colorlight
  - Semantic Class: Point
  - Semantic Property: None

For a „fancy“ naming, the widget makes use of the uiSemantics.
Information on usage/configuration can be found here

https://community.openhab.org/t/semantic-ui-using-enriched-semantic-to-ease-ui-creation/116882

## Changelog
### Version 0.1
- initial release for openHAB 4

## Resources
