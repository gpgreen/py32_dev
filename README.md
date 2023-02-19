# py32_dev

KiCad design for a ARM Cortex-M0+ development board. A USB C connector
provides 5V power only to the development board. The board must be
programmed with a debugger. External crystals are laid out for the MCU
to either use a 32.768 kHz low speed crystal or a 24 MHz high speed
crystal. The MCU is a Puya PY32 Series. The specific part is
PY032F030K18T6. This can run at a maximum of 48 MHz, and has 8 kbyte
SRAM and 64 kbyte Flash. There is an onboard LDO that provides 500mA
of power at 3.3V. A resettable fuse protects the USB port from a
short. There is an LED and user push button connected to 2 of the GPIO
pins. All available GPIO pins are routed to the 2 18pin headers.  puya
py32 cortex m0 development board

## Firmware
Example firmware that blinks the LED and changes blink frequency when the push button is pressed is located at:

## Links
- [[https://www.puyasemi.com/cpzx3/info_271_aid_247_kid_246.html][Puya PY32 Series]]
- [[https://github.com/jaydcarlson/py32-template][Software template for PY32 Series by Jay Carlson]]
