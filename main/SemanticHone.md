  
![grafik](https://github.com/hmerk/semanticHomeMenu/blob/main/screenshots/semanticHomeMenu2_dark.jpg)


The semanticHomeMenu project will give you an unique and easy to setup UI on mobile devices to control your openHAB installation. It is the openHAB 4 successor of the "main_widget" project.
The project is divided into a top level widget (semanticHomeMenu), and some equipment specific second level widgets (_Lights, _Rollershutter, RadiatorControl, _Security, _SecurityKeypad, _Energy).
It is also possible to use the second level widgets standalone or to extend the project with further widgets your own, some innspiration will be given later.

# Installation
Prerequisite for using this project is a well maintained semantic model and a strict naming scheme for several items. Best thing is not to create items individually but always use the "create equipment from Thing" option in main UI. All second level (equipment) widgets will include Group and Item examples for textual import. 
Next step will be to install the top level "semanticHomeModel" widget from the Marketplace and then to create a new page in MainUI which will hold just one widget, the "semanticHomeMenu" widget. This page needs some stylesheet tweaks, so please use the following code for it:
[page code snippet]

- If you want a specific ordering in the floors and/or rooms menu, please add the widgetOrderIndex as metadata to your items in the model.

Example for textual item import
```csv
Group   Attic           "Attic"                     <attic>                             ["Attic"]           {widgetOrder="1"}
Group   FirstFloor      "FirstFloor"                <firstfloor>                        ["FirstFloor"]      {widgetOrder="2"}
Group   GroundFloor     "GroundFloor"               <groundfloor>                       ["GroundFloor"]     {widgetOrder="3"}
Group   Cellar          "Cellar"                    <cellar>                            ["Basement"]        {widgetOrder="4"}

Group   Office          "Office"                    <office>            (Attic)         ["Room"]            {widgetOrder="1"}
Group   Guest           "Guestroom"                 <suitcase>          (Attic)         ["Bedroom"]         {widgetOrder="2"}
Group   CorridorFF      "Corridor Firstfloor"       <corridor>          (FirstFloor)    ["Corridor"]        {widgetOrder="3"}
Group   Childroom       "Childroom"                 <bedroom_blue>      (FirstFloor)    ["Bedroom"]         {widgetOrder="4"}
Group   Bathroom        "Bathroom"                  <bath>              (FirstFloor)    ["Bathroom"]        {widgetOrder="5"}
Group   Bedroom         "Bedroom"                   <bed>               (FirstFloor)    ["Bedroom"]         {widgetOrder="6"}
```

- Install all needed widgets for this project from the marketplace.
- Create an new layout page in openHAB MainUI
- Enter the `Code` tab for the new page and paste the following code

```yaml
config:
  label: HomeMenu
  sidebar: true
  hideNavbar: true
  showFullscreenIcon: false
  hideSidebarIcon: true
  style:
    --f7-block-padding-horizontal: 0px
    --f7-block-padding-vertical: 0px
    --f7-navbar-height: 0
blocks:
  - component: oh-block
    config:
      stylesheet: >
        .block:first-child{
          margin: 0px;
        }
    slots:
      default:
        - component: oh-grid-row
          config: {}
          slots:
            default:
              - component: oh-grid-col
                config: {}
                slots:
                  default:
                    - component: widget:main_widget
                      config: {}
masonry: null
grid: []
canvas: null
```

## Screenshots

## Changelog
### Version 0.1
- initial release for openHAB 4

## Resources
https://github.com/hmerk/semanticHomeMenu/blob/main/main/semanticHomeMenu.yaml
