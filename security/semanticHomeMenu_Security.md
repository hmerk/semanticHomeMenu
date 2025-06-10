* [Security widget]
  * including the [Keypad widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Security_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/SecurityKeypad_dark.jpg)


This widget card will show the members of your configured security groups and the state of your alarm system. For usage, you will need the following groups and items in your modell and configured within the main_widget.
- securityGroup [semantic or non semantic]
  The security group holds all items of type contact, motion or camera. The state of ech item will be shown as a badge.
- securityMode
  The securityMode item is of type string item which can have the following states (strings): disarmed, armed-away and armed-home. The state will colorize the icons like shown below [inactive - gray, active green or red]

```csv
String                        semanticHomeMenu_armedHome                    "Your translation of 'ARMED HOME'"
String                        semanticHomeMenu_disarmed                     "Your translation of 'DISARMED'"
String                        semanticHomeMenu_armedAway                    "Your translation of 'ARMED AWAY'"
String                        semanticHomeMenu_smokeDetectors               "Your translation of 'Smoke Detectors'"
String                        semanticHomeMenu_motionDetectors              "Your translation of 'Motion Detectors'"
String                        semanticHomeMenu_surveillance                 "Your translation of 'Surveillance'"
String                        semanticHomeMenu_blinds                       "Your translation of 'Blinds'"
String                        semanticHomeMenu_doors                        "Your translation of 'Doors'"
String                        semanticHomeMenu_windows                      "Your translation of 'Windows'"
```

## Changelog
### Version 0.2
### Version 0.1
- initial release for openHAB 4

## Resources
