---
title: "PiFire Hardware"
permalink: /hardware
sort: 2
---
## Hardware Configuration

In this section, we'll describe out to get your PiFire system built out in hardware. 

### Getting Started

The fastest way to get up and running is to utilize one of the PCB designs. There are several to choose from, having their individual strengths and use cases. 

* **4.x.x PCB (and modules)** - The state of the art currently is the 4.x.x PCB set which consists of a main board that connects to the Raspberry Pi (Connects to almost any Raspberry Pi model with 40 pin header).  The main board must be paired up with a probe board (i.e. ADS1115 carrier board, or other probe device board(s)) as well as a relay/fan board. These boards are not as compact as the next board on this list, but has the most flexible/scalable options.
  * [Links to these boards below.](#links-to-the-pcbs-in-the-4xx-family-of-pifire-boards)
* **Compact PWM PCB** - Designed by user [@weberbox](https://github.com/weberbox), this compact board includes a power supply, relays, and PWM circuitry on-board.  This board was designed to be utilized as an all-in-one unit that could be utilized with most installations, even portable smoker units!  This board is compatible with Raspberry Pi Zero W/2W models, but needs pin headers to be soldered to the backside of the Pi Zero board. While compact, you will be limited on just the features included with this board.  
  * _OSHWLab PCB w/DC Fan PWM Version: [https://oshwlab.com/zipster85/pifire-controller-pwm-1.2](https://oshwlab.com/zipster85/pifire-controller-pwm-1.2)_
  * _Handy BOM List for the above PCB: [https://github.com/nebhead/PiFire/files/9720705/PiFire-PWM-1.2-2022-BOM.xlsx](https://github.com/nebhead/PiFire/files/9720705/PiFire-PWM-1.2-2022-BOM.xlsx)_

* **3.0.x, 2.0.x PCBs** - Legacy PCB designs to be used with Raspberry Pi Zero W / 2W models.  These PCB designs are no longer recommended, but are still perfectly usable.
  * _[Link to Appendix-A: Legacy Hardware](https://nebhead.github.io/PiFire/appendix-a)_

* **Custom Build** - For the brave and curious, there is always the option to build your own from scratch as well, without using a PCB, which is described in [Appendix-A: Legacy Hardware](https://nebhead.github.io/PiFire/appendix-a).  

### 4.x.x PCB Details

The 4.x.x PCB is designed as a standard Raspberry Pi Hat that is compatible with most Raspberry Pi models including the Raspberry Pi Zero W/2W, Raspberry Pi 2/3/3a/3b/4/5.  This hat will not work with the compute modules.  

The PCB has mounting holes that fit standard stand-offs for the Raspberry Pi models mentioned above, such that the boards can be securely mounted together.  This board also incorporates keepouts so that it can be used as a hat with most of the Raspberry Pi boards. 

Some particular upgrades from previous revisions of the PCB:
1. Some GPIOs have been re-assigned because they had conflicts with other functionality or had undesirable behavior on boot/shutdown (i.e. the TXD/RXD pins).  
2. This board removes the selector switch (used to select the OEM controller) and replaces it with an on/off power switch option using the native power on/off capability on the Raspberry Pi (i.e. graceful shutdown and power-up).
3. This board does have an optional I2C EEPROM to store overlays. This is not currently implemented and should not be populated. 
4. There is an optional 12V input to pass through to the PWM Fan board. 
5. Two SPI headers are included with selectable chip enable pins and voltage levels.  This allows the ability support two different SPI devices such as a display and a RTD probe reading chip. 
6. The 1-Wire interface has been added to support the DS18B20 reference probe.  
7. All un-used GPIO pins as well as power and ground pins are broken out into a separate header that can be used for miscellaneous options. 

#### Links to the PCBs in the 4.x.x family of PiFire Boards

The 4.x.x Main Board PCB is part of a family of PCBs that can be used together to create a full PiFire system.  Generally speaking you need the Main Module/Board, a Relay Control Board and a Probe Device board to have a basic PiFire system.  

Click through the following links to see the board readme's for more information about the designs, the interactive BOM lists (i.e. hardware needed), schematics, layouts, 3D-printable cases, etc.  There are also instructions for ordering PCBs through JLCPCB, however you may be able to purchase these boards from others who may have extra boards on our Discord.

**Main Module/Board** (required)
* [Main Board v4.x.x](https://github.com/nebhead/pifire-main-module-nopwr)

**Relay/Fan Control Boards** (choose one)
* [Mechanical Relay Module](https://github.com/nebhead/pifire-relay-module)
* [Solid State Relay Module](https://github.com/nebhead/pifire-relay-module-SSR)
* [Solid State Relay + PWM DC Fan Module](https://github.com/nebhead/pifire-relay-pwm-module-ssr) - Original Design
* [Solid State Relay + PWM DC Fan Module Alternate](https://github.com/nebhead/pifire-relay-pwm-module-ssr-alt) - Updated Design (Designed with help from @labmonkeyrat on Discord)

**Probe Device Board** (optional)
* [ADS Board](https://github.com/nebhead/pifire-ads-board) - This board can be chained with more ADS boards to 'stack' up to 16 probe inputs.  

#### General 4.x.x PCB Architecture

Sometimes it is easier to understand how a project is built out by looking at the general architecture.  I've created a high-level diagram of the project so that you can get an idea of how all of this should be connected up. 

The first diagram is of the AC Fan Version of the system.  This version only requires a 5V power supply and only uses a portion of the headers to connect to a relay board.  Technically speaking, in this configuration you could use an off the shelf relay board if you wanted to wire this up yourself.

![PCB 4.x.x Diagram AC Fan](/img/PiFire-PCB-v4-Diagram.jpg)

The second diagram is of the DC PWM Fan version of the system.  You'll notice that this version utilizes a 5V/12V power-supply and the specially design relay/PWM Fan board.  

![PCB 4.x.x Diagram DC Fan](/img/PiFire-PCB-v4-Diagram-PWM.jpg)

#### PCB 4.x.x Pinout

Due to space constraints on the PCB silkscreen layer, most of the pins for the JST connectors are unmarked.  Thus I'm providing a handy set of images for the pinout of the major unmarked JST connectors. 

___Buttons & Encoder Header___

![PCB 4.x.x Pinout Buttons](/img/PiFire-PCB-v4-Pinout-Buttons.jpg)

___1-Wire Header___ - _Used for the DS18B20 reference probe.  Great for using as a reference to tune your other probes._

![PCB 4.x.x Pinout 1-Wire](/img/PiFire-PCB-v4-Pinout-1Wire.jpg)

___Relay and PWM Fan Headers___ - _If you are not using the DC Fan, then only the top header needs to be populated._

![PCB 4.x.x Pinout Relay / Fan](/img/PiFire-PCB-v4-Pinout-Relay-Fan.jpg)

___Auxiliary SPI Header___ - _If you are already using the display SPI header, this can be used for another SPI based device such as the MAX38165 RTD probe device._

```note
You must bridge solder jumpers on the back the board to select Chip Enable 0, Chip Enable 1 or GPIO6 (CE0/CE1/GPIO6) and 3.3V or 5V.  Do not bridge both 3.3V and 5V or CE0 and CE1 at the same time or you may damage your system.
```

![PCB 4.x.x Pinout Auxiliary SPI](/img/PiFire-PCB-v4-Pinout-SPI-AUX.jpg)

___Display SPI Header___ - _If you are using a SPI based display like the ILI9341, then this header should match the pinout for that display._

```note
You must bridge solder jumpers on the back the board to select Chip Enable 0 or 1 (CE0/CE1) and 3.3V or 5V.  Do not bridge both 3.3V and 5V or CE0 and CE1 at the same time or you may damage your system.
```

![PCB 4.x.x Pinout Display SPI](/img/PiFire-PCB-v4-Pinout-SPI-Display.jpg)

___I2C Headers___ - _All of the I2C headers pinouts are identical and can be used for any of the I2C devices including the ADC board, an I2C display, or an I2C distance device._

### Displays

PiFire doesn't require a display to be attached, but it is a nice addition to have.  The following are some supported options.  These can be selected during the initial configuration wizard. 

* **SSD1306** - Standard 1" OLED display with I2C interface (64Hx128W).  It's pretty tiny, but it does the job and it can be found very cheap if you are willing to order direct from China.  This is what was used for the initial/default implementation on the PiFire project. Make sure you get the all-white display and not the two-color (yellow/blue) display.  Example linked below.  (Raspberry Pi I2C Pin Mapping listed below)
  * [Amazon Link](https://www.amazon.com/Hosyond-Display-Self-Luminous-Compatible-Raspberry/dp/B09T6SJBV5/)

* **ILI9341 Based Display** - Many versions of this display are available from different sources.  I've built the ILI9341 support around the 240Hx320W SPI version of this.  Note that there are currently some 4" versions of this display, but they have a larger resolution and are not currently supported. **Also note that there are 'V' variants of the display which are also not currently supported.**  
  * [Amazon Link](https://www.amazon.com/Display-Module-240320-4-Wire-Screen/dp/B07KPD4DHD)  (Pin Mapping listed below)

* **ST7789 Based Display** - Again, many revisions of this are available from many different sources. Both a 240x240 and 320x240 screen resolution is currently supported. **Also note that there are 'V' variants of the display which aren't officially supported. However, there is an experimental library that you can try, which is available in the configuration wizard options.**  
  * [Amazon Link](https://www.amazon.com/gp/product/B07MH93747)

* **DSI Touch Display** - Since the v1.7.0 release of PiFire, a DSI Touch based display has been introduced for the Raspberry Pi full sized board.  Note that DSI is not supported by the Pi Zero or Pi Zero 2 boards.  Note that performance may be slow when using this display due to the system requirements for displaying full screen graphics.  
  * [Amazon Link](https://www.amazon.com/gp/product/B0B455LDKH)

### Physical Input

Some display types allow for physical inputs to control PiFire at the grill itself.  Currently, either buttons or a rotary encoder are available as input options (aside from touchscreen controls on a DSI touch display).  

#### Button Input

For Button Input, the following is an example of how tactile switches can be wired, with pullups.  The 4.x.x PCB has the GPIO inputs exposed at a JST header.  You'll need to build or source a button board to be used with this design.

![Button Input Schematic](/img/PiFire-PiSide-ButtonInput.jpg)

___Pins Assigned for Button Input on the v4.x.x Board___
* **GND**
* **B_UP - GPIO 14** - Up Input Button
* **B_ENT - GPIO 15** - Enter Input Button
* **B_DOWN - GPIO 16** - Down Input Button
* **3.3V**

[See Button/Encoder header pinout above...](#pcb-4xx-pinout)

```note
[@weberbox](https://github.com/weberbox) has also created a very useful button board that can be used to simplify the button input.  Note that this board is designed with active HIGH inputs and should be configured HIGH in your modules setup.

* EasyEda Button PCB: [https://easyeda.com/zipster85/pifire-buttons](https://easyeda.com/zipster85/pifire-buttons)
```

#### Rotary Encoder Input

Rotary encoders offer a simple alternative to implementing buttons.  The KY040 encoder is supported by some display types with the below pin assignment on the 4.x.x PCB.  

___Pins Assigned for Rotary Encoder Input on the v4.x.x Board___
* **GND**
* **GPIO 14** - CLK (Clock) (_Marked as B_UP on the PCB_)
* **GPIO 15** - SW (Switch) (_Marked as B_ENT on the PCB_)
* **GPIO 16** - DT (Data) (_Marked as B_DOWN on the PCB_)
* **3.3V**
* 
[See Button/Encoder header pinout above...](#pcb-4xx-pinout)

No additional board is needed as the pullups/pulldowns are already included on the KY040 boards. [Amazon Link](https://www.amazon.com/WayinTop-Degree-Encoder-Development-Arduino/dp/B07T3672VK)

### Distance Sensors

PiFire supports a few options for distance sensors to detect pellet levels in the hopper.

* **VL53L0X** _(RECOMMENDED)_ - Time of flight sensor with I2C interface.  This sensor allows the ability to measure the hopper pellet level quite easily and reliably. While it can be a bit expensive on Amazon, this can be obtained from other vendors (directly from China) for relatively cheap. (Raspberry Pi I2C Pin Mapping listed below)
  * [Amazon Link](https://www.amazon.com/gp/product/B071DW8M8V)

* **HCSR04** - Ultrasonic Sensor with GPIO interface.  This sensor hasn't been tested, but the module support is provided for potential use/testing if desired. These sensors are cheap and ubiquitous.  
  * [Amazon Link](https://www.amazon.com/HC-SR04-Ranging-Detector-Ultrasonic-Distance/dp/B01GNEHJNC)

### User Builds

If you're interested in seeing more builds from other users, we have a discussions thread [here](https://github.com/nebhead/PiFire/discussions/28) where others have posted pictures of their unique builds.  In addition to the discussions thread above, the [discord server](https://discord.gg/F9mbCrbrZS) is a great place to see and share build photos and experiences. 
