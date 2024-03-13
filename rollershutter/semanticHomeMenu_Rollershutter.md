![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Rollershutter.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/RollershutterExpanded.jpg)

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

Example for textual item import (TBC)
```csv
Group                   rollershutterGroup      "Rollershutter Childroom"   <blinds>    (Childroom)          ["Blinds"]                 {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Rollershutter", location="Childroom"]}

Rollershutter           rollershutterGroup_Control      "Rollershutter"             <blinds>    (rollershutterGroup_Control) ["Control", "Opening"]
Switch                  rollershutterGroup_TimeControl  "Timecontrol"               <time>      (rollershutterGroup_Control) ["Control", "Timestamp"]
DateTime                rollershutterGroup_OpenWeek     "Open Week"                 <time>      (rollershutterGroup_Control) ["Control", "Timestamp"]   {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="1"}
DateTime                rollershutterGroup_CloseWeek    "Close Week"                <time>      (rollershutterGroup_Control) ["Control", "Timestamp"]   {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="2"}
DateTime                rollershutterGroup_OpenWeekend  "Open Weekend"              <time>      (rollershutterGroup_Control) ["Control", "Timestamp"]   {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="3"}
DateTime                rollershutterGroup_CloseWeekend "Close Weekend"             <time>      (rollershutterGroup_Control) ["Control", "Timestamp"]   {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="4"}
```

Example item file for with knx channel binding
```csv
Group           EG                    "Erdgeschoss"         <groundfloor>             ["Location"]
Group           EG_KU                 "Küche"               <kitchen>          (EG)   ["Location"]
Group           EG_WZ                 "Wohnzimmer"          <location>         (EG)   ["Location"]
Group           EG_EZ                 "Esszimmer"           <location>         (EG)   ["Location"]
Group           EG_GZ                 "Gästezimmer"         <location>         (EG)   ["Location"]
Group           EG_BZ                 "Badezimmer"          <location>         (EG)   ["Location"]
Group           EG_SZ                 "Schlafzimmer"        <location>         (EG)   ["Location"]

Group           rollershutterGroup          "Rolladen Badezimmer"        <rollershutter>     (EG_BZ)         ["Blinds"]                   {uiSemantics="uiSemantics"[preposition=" im", equipment="Rolladen", location="Badezimmer"]}
Rollershutter   rollershutterGroup_Control        "Control"                    <rollershutter>     (EG_BZ_RS)      ["Control" ,"Opening"]       {uiSemantics="uiSemantics"[preposition=" im", equipment="Rolladen", location="Badezimmer"], channel="knx:device:bridge:generic:EG_BZ_RS"}
Switch          rollershutterGroup_TimeControl    "Zeitplan"                   <time>              (EG_BZ_RS)      ["Control", "Timestamp"]
DateTime        rollershutterGroup_OpenWeek       "Öffnen Wochentags"          <time>              (EG_BZ_RS)      ["Control", "Timestamp"]     {stateDescription=" "[pattern="%1$tH:%1$tM"], widget="widget:semanticHomeMenu_Simple24hTimepicker", listWidget="widget:semanticHomeMenu_Simple24hTimepicker"}
DateTime        rollershutterGroup_CloseWeek      "Schließen Wochentags"       <time>              (EG_BZ_RS)      ["Control", "Timestamp"]     {stateDescription=" "[pattern="%1$tH:%1$tM"], widget="widget:semanticHomeMenu_Simple24hTimepicker", listWidget="widget:semanticHomeMenu_Simple24hTimepicker"}
DateTime        rollershutterGroup_OpenWeekend    "Öffnen Wochenende"          <time>              (EG_BZ_RS)      ["Control", "Timestamp"]     {stateDescription=" "[pattern="%1$tH:%1$tM"], widget="widget:semanticHomeMenu_Simple24hTimepicker", listWidget="widget:semanticHomeMenu_Simple24hTimepicker"}
DateTime        rollershutterGroup_CloseWeekend   "Schließen Wochenende"       <time>              (EG_BZ_RS)      ["Control", "Timestamp"]     {stateDescription=" "[pattern="%1$tH:%1$tM"], widget="widget:semanticHomeMenu_Simple24hTimepicker", listWidget="widget:semanticHomeMenu_Simple24hTimepicker"}
```


You will then need to add initial states to the 4 items via API-Explorer.

  - Create 4 rules for opening and closing the rollershutter [optional]
    -  When : it is a date and time specified in an item -> choose item "rollershutterGroup_OpenWeek"
    -  Then : Send command up to rollershutterGroup_Control item
    -  But only if
      - Ephemeris : it is a weekday
      - If rollershutterGroup_TimeControl = ON
      - If Rollershutter state != 0

Codepage for the rule:
```csv
configuration: {}
triggers:
  - id: "1"
    configuration:
      itemName: rollershutterGroup_OpenWeek
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
      itemName: rollershutterGroup_TimeControl
      state: ON
      operator: =
    type: core.ItemStateCondition
  - inputs: {}
    id: "5"
    configuration:
      itemName: rollershutterGroup_Control
      state: "0"
      operator: "!="
    type: core.ItemStateCondition
actions:
  - inputs: {}
    id: "2"
    configuration:
      command: UP
      itemName: rollershutterGroup_Control
    type: core.ItemCommandAction
```
Repeat this for all 4 times to control.

Cosing rule for workdays:
```csv
configuration: {}
triggers:
  - id: "1"
    configuration:
      itemName: rollershutterGroup_CloseWeek
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
      itemName: rollershutterGroup_TimeControl
      state: ON
      operator: =
    type: core.ItemStateCondition
  - inputs: {}
    id: "5"
    configuration:
      itemName: rollershutterGroup_Control
      state: "100"
      operator: <=
    type: core.ItemStateCondition
actions:
  - inputs: {}
    id: "2"
    configuration:
      command: DOWN
      itemName: rollershutterGroup_Control
    type: core.ItemCommandAction
```

Opening rule for weekends:
```csv
configuration: {}
triggers:
  - id: "1"
    configuration:
      itemName: rollershutterGroup_OpenWeekend
      timeOnly: true
    type: timer.DateTimeTrigger
conditions:
  - inputs: {}
    id: "3"
    configuration:
      offset: 0
    type: ephemeris.WeekendCondition
  - inputs: {}
    id: "4"
    configuration:
      itemName: rollershutterGroup_TimeControl
      state: ON
      operator: =
    type: core.ItemStateCondition
  - inputs: {}
    id: "5"
    configuration:
      itemName: rollershutterGroup_Control
      state: "0"
      operator: "!="
    type: core.ItemStateCondition
actions:
  - inputs: {}
    id: "2"
    configuration:
      command: UP
      itemName: rollershutterGroup_Control
    type: core.ItemCommandAction
```

Closing rule for weekends:
```csv
configuration: {}
triggers:
  - id: "1"
    configuration:
      itemName: rollershutterGroup_CloseWeekend
      timeOnly: true
    type: timer.DateTimeTrigger
conditions:
  - inputs: {}
    id: "3"
    configuration:
      offset: 0
    type: ephemeris.WeekendCondition
  - inputs: {}
    id: "4"
    configuration:
      itemName: rollershutterGroup_TimeControl
      state: ON
      operator: =
    type: core.ItemStateCondition
  - inputs: {}
    id: "5"
    configuration:
      itemName: rollershutterGroup_Control
      state: "100"
      operator: <=
    type: core.ItemStateCondition
actions:
  - inputs: {}
    id: "2"
    configuration:
      command: DOWN
      itemName: rollershutterGroup_Control
    type: core.ItemCommandAction
```


## Screenshots

_[🖍 Upload other screenshots if necessary or remove the section.]_

## Changelog
### Version 0.1
- initial release for openHAB 4

## Resources
