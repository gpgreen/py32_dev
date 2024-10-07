# py32_dev

KiCad design for a ARM Cortex-M0+ development board. The MCU is a Puya
PY32 Series. The specific part is PY032F030K18T6. This can run at a
maximum of 48 MHz, and has 8 kbyte SRAM and 64 kbyte Flash. A USB C
connector provides 5V power only to the development board. The board
must be programmed with a debugger. External crystals are laid out for
the MCU to use a 32.768 kHz low speed crystal or a 24 MHz high speed
crystal. There is an onboard LDO that provides 500mA of power at
3.3V. A resettable fuse protects the USB port from a short. There is
an LED and push button connected to 2 of the GPIO pins. The value of
the BOOT0 pin can be set to ground or 3.3V permanently via the solder
bridge. A jumper can be used on the pin rails in lieue of the solder
bridge. All available GPIO pins are routed to the 2 18pin headers.

## Changes

- Rev B
  Moved resettable fuse away from USB C connector, giving more room to resolder
  connector pins.

- Rev A
  Original

## Firmware

Example firmware that blinks the LED. When the user pushbutton is pressed,
the frequency of the LED blink will change.

https://github.com/gpgreen/py32-dev-blink

## Boot configuration

To boot from main flash [0x0800_0000]
  Connect J2-4 to J2-5 (or) solder JP5-1 to center post

To boot from System mem [0x1FFF_0000], or Embedded SRAM [0x2000_0000]
  Connect J2-4 to J2-3 (or) solder JP6-3 to center post

There is an embedded boot loader, programmed in production, in the system memory
block. See the reference manual 3.6.2.

## PIN JUMPER SIGNAL ASSIGNMENT
```
                    +-----+
            +--------------------+
            |J3     |     |    J2|
        VDD-|1      +-----+     1|-GND
        GND-|2                  2|-GND
       +3.3-|3                  3|-+3.3
[RESET] PF2-|4                  4|-PF4 [BOOT0_PRE]
[SWCLK]PA14-|5                  5|-GND
[SWDIO]PA13-|6                  6|-GND
        GND-|7       RST        7|-GND
        PF3-|8       +-+        8|-GND
        PA0-|9       |O|        9|-GND
        PA1-|10      +-+       10|-PB7
        PA2-|11                11|-PB6
        PA3-|12                12|-PB5
        PA4-|13                13|-PB4
        PA6-|14                14|-PB3
        PA6-|15   UPB          15|-PA15
        PA7-|16   +-+          16|-PA12 [USER LED - GREEN]
        PB0-|17   |O|          17|-PA11 [USER PUSHBUTTON]
        PB1-|18   +-+          18|-PA8
            |                    |
            +--------------------+
```
## Connections to JTAG

From a 20pin JTAG connector, run wires to the following pins to connect a debugger:

VTRef 1  <-> J3-3
SWDIO 7  <-> J3-6
SWCLK 9  <-> J3-5
RESET 15 <-> J3-4
5V    19 <-> NC
GND   4  <-> J3-2
GND   20 <-> J3-7

## Running SEGGER JLink

Run the JLink GDB server via the following:
```
JLinkGDBServer -if SWD -JLinkDevicesXMLPath ~/.config/SEGGER/JLinkDevices/Puya/PY32/JLinkDevices.xml -device PY32F030xx8
```

GDB can be connected via the following:
```
gdb-multiarch --command=jlink-py32.gdb target/thumbv6m/debug/blink-py32
```

## Links
- [Puya PY32 Series](https://www.puyasemi.com/cpzx3/info_271_aid_247_kid_246.html)
- [Software template for PY32 Series by Jay Carlson](https://github.com/jaydcarlson/py32-template)
- [Fork of template for these boards](https://github.com/gpgreen/py32-dev-blink)
- [Tech documentation for py32f030](https://www.puyasemi.com/uploadfiles/2022/11/PY-MCU%E8%B5%84%E6%96%99-20221117.rar)
