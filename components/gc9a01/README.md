## GC9A01

Support for GC9A01 chipset round LCD modules

Collected from PRs referenced within [ESPHome issue #1699][esphome-issue-1699],
plus some of my own tweaks

Example usage:

```yaml
external_components:
- source: github://smkent/esphome@main
  components: [ gc9a01 ]

esphome:
  on_boot:
    priority: 600
    then:
    - light.turn_on: lcd_round_backlight

output:
- id: !extend lcd_round_backlight_output
  platform: ledc
  pin: 20

light:
- platform: monochromatic
  output: "lcd_round_backlight_output"
  id: "lcd_round_backlight"
  name: "Display backlight"
  default_transition_length: 400ms

spi:
  mosi_pin: 6
  clk_pin: 4

display:
- platform: gc9a01
  reset_pin: GPIO0
  cs_pin: 7
  dc_pin: 5
  rotation: 180
  eight_bit_color: false
  auto_clear_enabled: false
  lambda: |-
    it.line(0, 0, 100, 50);
```
