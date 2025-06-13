* [Security widget]
  * including the [Keypad widget]
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/Security_dark.jpg)
  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/SecurityKeypad_dark.jpg)


This widget card will show the members of your configured security groups and the state of your alarm system. For usage, you will need the following groups and items. If you have an alarm system you want integrated in the widget, the state of `securityGroup_PINused` should be `ON`. If not, the keypad widget will be invisible.

- securityGroup
  This group item holds all items of type contact, motion or camera. The state of each item will be shown as a badge. It's essential that item `securityGroup` has the tag `AlarmSystem`.
- securityGroup_mode
  The securityMode item is of type string item which can have the following states (strings): disarmed, armed-away and armed-home. The state will colorize the icons like shown below [inactive - gray, active green or red]
- securityGroup_PIN
  (no idea...)

```
Group        securityGroup                      "Security Group"               ["AlarmSystem"]
Switch       securityGroup_PINused              "Security Group - PIN used?"
String       securityGroup_mode                 "Security Group - Mode"
String       securityGroup_PIN                  "Security Group - PIN"
```

## Changelog
### Version 0.2
### Version 0.1
- initial release for openHAB 4

## Resources
