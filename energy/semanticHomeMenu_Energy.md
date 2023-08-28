* [HVAC widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/LowBattery.jpg)

The Eergy widget card used by semanticHomeMenu will by default show information about empty batteries as an accordion list.

![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/LowBatteryExpanded.jpg)

### Usage
Example for textual item import (TBD)
```csv
Group                   hvacChild               "HVAC Childroom"       <climate>            (Childroom) ["HVAC"]    {uiSemantics="uiSemantics"[preposition=" in the ", equipment="HVAC", location="Childroom"]}

Switch                  powerHvacChild          "HVAC Power"           <switch>             (hvacChild) ["Control", "Power"]
Number:Temperature      targetTempHvacChild     "Target Temperature"   <temperature>        (hvacChild) ["Setpoint", "Temperature"]
Number:Temperature      ambientTempHvacChild    "Ambient Temperature"  <temperature>        (hvacChild) ["Measurement", "Temperature"]
String                  modeHvacChild           "HVAC Mode"            <temperature_cold>   (hvacChild) ["Control", "Temperature"]
String                  fanspeedHvacChild       "Fanspeed"             <qualityofservice>   (hvacChild) ["Control", "Wind"]
String                  vanesHvacChild          "Vanes Position"       <movecontrol>        (hvacChild) ["Control", "Opening"]
// Some devices have numeric values for mode, fanspeed and vanes position, use a number item instead
// Number               modeHvacChild           "HVAC Mode"            <temperature_cold>   (hvacChild) ["Control", "Temperature"]
// Number               fanspeedHvacChild       "Fanspeed"             <qualityofservice>   (hvacChild) ["Control", "Wind"]
// Number               vanesHvacChild          "Vanes Position"       <movecontrol>        (hvacChild) ["Control", "Opening"]

```

Control Mode, Fanspeed and Vane Position use Item options. More Information with example for different thermostats will follow.

## Changelog
### Version 0.1
- initial release for openHAB 4

## Resources
