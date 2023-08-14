![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Rollershutter_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/RollershutterExpanded_dark.jpg)

The rollershutter card is one of the sub widgets to let you control your rollershutters with a unique look and feel.
Apart from just controlling your rollershutters with sending up and down commands, you can also send predefined values like 50% to your device.
Additionaly you can setup time based opening and closing of rollershutters with the DateTime-trigger for rules.

## Installation and Setup
This widget can be installed via the marketplace. For basic operation, no configuration is needed.

To use the time based triggers, there are some additional steps needed.
- Install the timepicker widget from the marketplace.
  - https://community.openhab.org/t/time-picker/118865
- change lines 49,69,123,143,187 and 218 from
```csv
 YYYY-MM-DDTHH:mm:ss.ZZ
 ```
to
```csv
  - YYYY-MM-DDTHH:mm:ss.SSSZZ
```

- You will need 5 additional items in your rollershutter equipment group, here we take the rollershutters in the childroom as an example
  - A Switch item to enable/disable the automatic/time control [optional]
  - 4 DateTime items for holding the different Times, openWeekday, closeWeekday, openWeekend, closeWeekend [optional]

Example for textual item import
```csv
Group                   RollershutterChild      "Rollershutter Childroom"   <blinds>    (Childroom)          ["Blinds"]                 {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Rollershutter", location="Childroom"]}

Rollershutter           rollershutterChild      "Rollershutter"             <blinds>    (RollershutterChild) ["Control", "Opening"]
Switch                  rollerChildTimeControl  "Timecontrol"               <time>      (RollershutterChild) ["Control", "Timestamp"]
DateTime                rollerOpenChildWeek     "Open Week"                 <time>      (RollershutterChild) ["Control", "Timestamp"]   {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="1"}
DateTime                rollerCloseChildWeek    "Close Week"                <time>      (RollershutterChild) ["Control", "Timestamp"]   {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="2"}
DateTime                rollerOpenChildWeekend  "Open Weekend"              <time>      (RollershutterChild) ["Control", "Timestamp"]   {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="3"}
DateTime                rollerCloseChildWeekend "Close Weekend"             <time>      (RollershutterChild) ["Control", "Timestamp"]   {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="4"}
```
You will then need to add initial states to the 4 items via API-Explorer.

  - Create 4 rules for opening and closing the rollershutter [optional]
    -  When : it is a date and time specified in an item -> choose item "rollerOpenChildWeek"
    -  Then : Send command up to rollershutterChild item
    -  But only if
      - Ephemeris : it is a weekday
      - If rollerChildTimeControl = ON
      - If Rollershutter state != 0

Codepage for the rule:
```csv
configuration: {}
triggers:
  - id: "1"
    configuration:
      itemName: rollerOpenChildWeek
      timeOnly: true
    type: timer.DateTimeTrigger
conditions:
  - inputs: {}
    id: "3"
    configuration:
      offset: 0
    type: ephemeris.WeekdayCondition
  - inputs: {}
    id: "4"
    configuration:
      itemName: rollerChildTimeControl
      state: ON
      operator: =
    type: core.ItemStateCondition
  - inputs: {}
    id: "5"
    configuration:
      itemName: rollershutterChild
      state: "0"
      operator: "!="
    type: core.ItemStateCondition
actions:
  - inputs: {}
    id: "2"
    configuration:
      command: UP
      itemName: rollershutterChild
    type: core.ItemCommandAction
```
Repeat this for all 4 times to control.

## Screenshots

_[🖍 Upload other screenshots if necessary or remove the section.]_

## Changelog
### Version 0.1
- initial release for openHAB 4

## Resources
