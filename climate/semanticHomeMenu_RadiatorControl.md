* [RadiatorControl widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/RadiatorControl.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/RadiatorControlExpanded.jpg)

The RadiatorControl card will show all radiator controls (thermostats) in a selected room and show controls based on equipment group members.
Group members have to follow the naming shown in the example Items definition.

## Usage

Example for textual item import (TBC)
```csv
Group                   RadiatorChild               "Radiator Childroom"    <radiator>      (Childroom)     ["RadiatorControl"]             {uiSemantics="uiSemantics"[preposition=" in the ", equipment="Radiator", location="Childroom"]}

String                  modeHeatingChild            "Heating Mode"          <heating>       (RadiatorChild) ["Control", "Temperature"]
// Some devices have numeric mode values, use a number item instead
// Number               modeHeatingChild            "Heating Mode"          <heating>       (RadiatorChild) ["Control", "Temperature"]
Number:Temperature      targetTempHeatingChild      "Target Temperature"    <temperature>   (RadiatorChild) ["Setpoint", "Temperature"]
Number:Temperature      ambientTempHeatingChild     "Ambient Temperature"   <temperature>   (RadiatorChild) ["Measurement", "Temperature"]
Number:Dimensionless    batteryLevelHeatingChild    "Batterylevel"          <batterylevel>  (RadiatorChild) ["Measurement", "Voltage"]      {stateDescription=" "[pattern="%.0f %%"]}
Switch                  lowBatteryHeatingChild      "LowBattery"            <lowbattery>    (RadiatorChild) ["LowBattery", "Voltage"]
Switch                  timeControlHeatingChild     "Timecontrol Childroom" <time>          (RadiatorChild) ["Control", "Timestamp"]
DateTime                comfortOnChildWeek          "Comfort Week"          <time>          (RadiatorChild) ["Control", "Timestamp"]        {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="1"}
DateTime                ecoOnChildWeek              "ECO Week"              <time>          (RadiatorChild) ["Control", "Timestamp"]        {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="2"}
DateTime                comfortOnChildWeekend       "Comfort Weekend"       <time>          (RadiatorChild) ["Control", "Timestamp"]        {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="3"}
DateTime                ecoOnChildWeekend           "ECO Weekend"           <time>          (RadiatorChild) ["Control", "Timestamp"]        {stateDescription=" "[pattern="%1$tH:%1$tM"],widgetOrder="4"}
```
## Changelog
### Version 0.1
- initial release for openHAB 4.0

## Resources
