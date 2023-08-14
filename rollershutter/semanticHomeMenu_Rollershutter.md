uid: semanticHomeMenu_Rollershutter
tags: []
props:
  parameters:
    - context: item
      description: Calculated by oh-repeater in Floors&Rooms
      label: Blinds Group
      name: groupItem
      required: false
      type: TEXT
    - description: Calculated by oh-repeater in Floors&Rooms
      label: Blinds Group Label
      name: groupItemLabel
      required: false
      type: TEXT
    - description: Calculated by oh-repeater in Floors&Rooms
      label: Blinds Group Location
      name: groupItemLocation
      required: false
      type: TEXT
    - context: Text
      default: orange
      label: ColorScheme
      name: colorScheme
      required: true
      type: TEXT
    - context: Text
      default: RGB(255,153,0)
      label: RGB ColorScheme
      name: rgbColorScheme
      required: true
      type: TEXT
    - context: Text
      default: FF9900
      label: Hex ColorScheme
      name: hexColorScheme
      required: true
      type: TEXT
timestamp: Aug 4, 2023, 11:00:01 PM
component: f7-card
config:
  style:
    min-width: 360px
  stylesheet: >
    .accordion-nr.open {

      max-height: 400px;
      transition: max-height 0.25s ease-in; 
    }

    .accordion-nr.closed {

      max-height: 0px;
      transition: max-height 0.15s ease-out;
    }
slots:
  default:
    - component: f7-row
      config:
        class:
          - justify-content-left
          - align-items-center
          - display-flex
      slots:
        default:
          - component: f7-col
            config:
              class:
                - padding-half
              style:
                height: 100%
                width: 60px
            slots:
              default:
                - component: oh-icon
                  config:
                    height: 100%
                    icon: iconify:mdi:window-shutter
                    style:
                      opacity: 0.7
                    width: 100%
          - component: f7-col
            config:
              class:
                - display-flex
                - flex-direction-column
              style:
                flex-grow: 1
                height: 100%
            slots:
              default:
                - component: f7-row
                  config:
                    style:
                      overflow: hidden
                      width: 100%
                  slots:
                    default:
                      - component: Label
                        config:
                          style:
                            font-size: 16px
                            font-weight: bold
                          text: '=props.groupItemLabel ? props.groupItemLabel : "TBD"'
                - component: f7-row
                  config:
                    class:
                      - display-flex
                      - flex-direction-column
                    style:
                      width: 100%
                  slots:
                    default:
                      - component: Label
                        config:
                          text: '=props.groupItemLocation ? props.groupItemLocation : "TBD"'
                - component: f7-row
                  config:
                    class:
                      - display-flex
                      - flex-direction-row
                      - justify-content-left
                    style:
                      width: 100%
                  slots:
                    default:
                      - component: f7-chip
                        config:
                          style:
                            justify-content: flex-end
                          text: "=items[props.groupItem + '_control'].displayState ? (items[props.groupItem + '_control'].displayState) + ' closed' : items[props.groupItem + '_control'].state + '% closed'"
          - component: f7-col
            config:
              class:
                - display-flex
                - flex-direction-column
              style:
                height: 100%
                min-width: 110px
            slots:
              default:
                - component: f7-col
                  config:
                    class:
                      - no-margin
                      - display-flex
                      - flex-direction-col
                      - justify-content-center
                      - align-items-center
                    style:
                      height: 100%
                      width: 100%
                  slots:
                    default:
                      - component: oh-button
                        config:
                          action: command
                          actionCommand: UP
                          actionItem: =props.groupItem + '_control'
                          class:
                            - no-padding
                          iconF7: arrow_up_circle
                          iconSize: 32
                          style:
                            color: "= props.colorScheme ? props.colorScheme : var(--f7-theme-color)"
                            height: 100%
                      - component: oh-button
                        config:
                          action: command
                          actionCommand: STOP
                          actionItem: =props.groupItem + '_control'
                          class:
                            - no-padding
                          iconF7: stop_circle
                          iconSize: 32
                          style:
                            color: var(--f7-toggle-inactive-color)
                            height: 100%
                      - component: oh-button
                        config:
                          action: command
                          actionCommand: DOWN
                          actionItem: =props.groupItem + '_control'
                          class:
                            - no-padding
                          iconF7: arrow_down_circle
                          iconSize: 32
                          style:
                            color: "= props.colorScheme ? props.colorScheme : var(--f7-theme-color)"
                            height: 100%
          - component: f7-col
            config:
              class:
                - display-flex
                - justify-content-center
                - margin-right
              style:
                width: auto
            slots:
              default:
                - component: oh-link
                  config:
                    action: variable
                    actionVariable: openAccordion
                    actionVariableValue: '=(vars.openAccordion== "null") ? true : !(vars.openAccordion)'
                  slots:
                    default:
                      - component: oh-icon
                        config:
                          icon: f7:ellipsis_vertical
                          style:
                            color: var(--f7-toggle-inactive-color)
                          width: 30px
    - component: f7-block
      config:
        class:
          - no-padding
          - accordion-nr
          - '=vars.openAccordion ? "open" : "closed"'
        style:
          margin-top: 0px
          overflow: hidden
          width: 100%
      slots:
        default:
          - component: f7-block
            config:
              class:
                - no-margin
                - no-padding-left
                - no-padding-right
                - padding-top-half
              style:
                height: 120px
                width: 100%
            slots:
              default:
                - component: oh-chart
                  config:
                    chartType: day
                    height: 80%
                    periodVisible: false
                  slots:
                    grid:
                      - component: oh-chart-grid
                        config:
                          borderWidth: 0
                          height: 100%
                          includeLabels: true
                          top: 0px
                    series:
                      - component: oh-aggregate-series
                        config:
                          aggregationFunction: average
                          backgroundStyle:
                            borderRadius:
                              - 50
                              - 50
                              - 50
                              - 50
                            color:
                              colorStops:
                                - color: "#188df0"
                                  offset: 0
                                - color: white
                                  offset: 1
                              type: linear
                              x: 0
                              x2: 0
                              y: 0
                              y2: 1
                          dimension1: hour
                          gridIndex: 0
                          item: =props.groupItem + '_control'
                          itemStyle:
                            borderRadius:
                              - 50
                              - 50
                              - 50
                              - 50
                            color: lightgray
                          showBackground: true
                          type: bar
                          xAxisIndex: 0
                          yAxisIndex: 0
                    tooltip:
                      - component: oh-chart-tooltip
                        config:
                          orient: vertical
                          show: false
                          trigger: axis
                    xAxis:
                      - component: oh-category-axis
                        config:
                          axisLabel:
                            color: red
                            show: false
                          axisLine:
                            show: true
                          axisPointer:
                            show: false
                          axisTick:
                            interval: 0
                            lineStyle:
                              opacity: 0.5
                            show: true
                          categoryType: day
                          gridIndex: 0
                          nameTextStyle:
                            color: transparent
                          show: true
                    yAxis:
                      - component: oh-value-axis
                        config:
                          gridIndex: 0
                          inverse: true
                          max: 100
                          min: 0
                          show: false
                - component: f7-row
                  config:
                    style:
                      height: 20%
                      margin-left: 10%
                      margin-right: 10%
                      margin-top: 1px
                  slots:
                    default:
                      - component: f7-col
                        slots:
                          default:
                            - component: Label
                              config:
                                text: 0:00
                      - component: f7-col
                        config:
                          class:
                            - display-flex
                            - justify-content-center
                          style: {}
                        slots:
                          default:
                            - component: Label
                              config:
                                text: 12:00
                      - component: f7-col
                        config:
                          class:
                            - display-flex
                            - justify-content-right
                        slots:
                          default:
                            - component: Label
                              config:
                                text: 24:00
          - component: f7-card-footer
            config:
              style:
                background-color: var(--f7-card-footer-bg-color)
            slots:
              default:
                - component: f7-block
                  config:
                    class:
                      - no-padding
                      - no-margin
                    style:
                      width: 100%
                  slots:
                    default:
                      - component: f7-row
                        config:
                          class:
                            - no-padding
                            - no-marging
                          style:
                            width: 100%
                        slots:
                          default:
                            - component: f7-col
                              config:
                                style:
                                  border-style: solid
                                  border-width: 0 2px 0 0
                                  flex-grow: 1
                                  width: 80%
                              slots:
                                default:
                                  - component: f7-row
                                    config:
                                      class:
                                        - margin-bottom-half
                                        - margin-horizontal-half
                                        - justify-content-left
                                        - align-items-center
                                        - display-flex
                                    slots:
                                      default:
                                        - component: Label
                                          config:
                                            text: Preset positions
                                  - component: f7-row
                                    config:
                                      class:
                                        - no-padding
                                        - margin-horizontal
                                        - justify-content-left
                                        - display-flex
                                    slots:
                                      default:
                                        - component: oh-repeater
                                          config:
                                            for: preset
                                            fragment: true
                                            in:
                                              - 0
                                              - 1
                                              - 20
                                              - 50
                                              - 80
                                              - 99
                                              - 100
                                            sourceType: array
                                          slots:
                                            default:
                                              - component: oh-link
                                                config:
                                                  action: command
                                                  actionCommand: =loop.preset.toString()
                                                  actionItem: =props.groupItem + '_control'
                                                  class:
                                                    - margin-half
                                                  style:
                                                    background-color: '=(Number(items[props.groupItem + "_control"].state.split(" ")[0])== loop.preset) ? "var(--f7-toggle-active-color)" : "var(--f7-toggle-inactive-color)"'
                                                    border-radius: 100%
                                                    color: white
                                                    font-weight: bold
                                                    height: 30px
                                                    min-width: 30px
                                                slots:
                                                  default:
                                                    - component: Label
                                                      config:
                                                        text: =loop.preset
                            - component: f7-col
                              config:
                                style:
                                  height: 100%
                                  width: 20%
                              slots:
                                default:
                                  - component: f7-row
                                    config:
                                      class:
                                        - margin-bottom-half
                                        - margin-horizontal-half
                                        - justify-content-left
                                        - display-flex
                                      style:
                                        height: auto
                                    slots:
                                      default:
                                        - component: Label
                                          config:
                                            text: Settings
                                  - component: f7-row
                                    config:
                                      class:
                                        - no-padding
                                        - margin-horizontal
                                        - align-items-center
                                        - display-flex
                                    slots:
                                      default:
                                        - component: oh-link
                                          config:
                                            action: popup
                                            class:
                                              - margin-half
                                            popupOpen: ="."+props.groupItem
                                            style:
                                              background-color: var(--f7-toggle-inactive-color)
                                              border-radius: 100%
                                              color: white
                                              font-weight: bold
                                              height: 30px
                                              min-width: 30px !important
                                          slots:
                                            default:
                                              - component: oh-icon
                                                config:
                                                  height: 80%
                                                  icon: iconify:carbon:event-schedule
    - component: f7-popup
      config:
        class: =props.groupItem + " mainWidget"
        closeByBackdropClick: true
        closeByOutsideClick: true
        closeOnEscape: true
        swipeToClose: true
      slots:
        default:
          - component: f7-row
            config:
              class:
                - margin
                - justify-content-center
                - align-items-center
                - display-flex
              style:
                width: 100%
            slots:
              default:
                - component: f7-col
                  config:
                    class:
                      - justify-content-center
                      - display-flex
                  slots:
                    default:
                      - component: oh-toggle
                        config:
                          item: =props.groupItem + '_scheduleControl'
                - component: f7-col
                  slots:
                    default:
                      - component: Label
                        config:
                          text: Zeitsteuerung
          - component: oh-repeater
            config:
              for: i
              fragment: true
              in:
                - item: _openWeek
                  label: Öffnen Wochentage
                - item: _closeWeek
                  label: Schließen Wochentage
                - item: _openWeekend
                  label: Öffnen Wochenende
                - item: _closeWeekend
                  label: Schließen Wochenende
              sourceType: array
            slots:
              default:
                - component: f7-row
                  config:
                    class:
                      - margin
                      - justify-content-center
                      - align-items-center
                      - display-flex
                    style:
                      width: 100%
                  slots:
                    default:
                      - component: f7-col
                        config:
                          class:
                            - justify-content-center
                            - display-flex
                        slots:
                          default:
                            - component: oh-link
                              config:
                                action: popover
                                popoverOpen: ="."+ props.groupItem + loop.i.item
                                style:
                                  background: transparent
                                  color: black
                                  height: 35px
                              slots:
                                default:
                                  - component: f7-chip
                                    config:
                                      style:
                                        background-color: "#D3D3D3"
                                        color: black
                                      text: =items[props.groupItem + loop.i.item].displayState
                                  - component: f7-popover
                                    config:
                                      backdrop: false
                                      class: =props.groupItem + loop.i.item
                                      closeByBackdropClick: true
                                      closeByOutsideClick: true
                                      closeOnEscape: true
                                    slots:
                                      default:
                                        - component: widget:timepicker
                                          config:
                                            item: =props.groupItem + loop.i.item
                                            timeFormat: 24h
                      - component: f7-col
                        slots:
                          default:
                            - component: Label
                              config:
                                text: =loop.i.label
