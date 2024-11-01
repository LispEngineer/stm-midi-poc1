# Doug's MIDI Synth Board

* [Douglas P. Fields, Jr.](mailto:symbolics@lisp.engineer)
* Copyright 2024, Douglas P. Fields, Jr.
* License: Creative Commons Attribution-ShareAlike 4.0
  * AKA `CC BY-SA 4.0`
  * [See LICENSE.md](LICENSE.md) or [CC site](https://creativecommons.org/licenses/by-sa/4.0/deed.en)

Project Documentation:
* [Hardware requirements](https://docs.google.com/document/d/1ovH1onACyaObaqHR-o14pt8njggKNDry9VQSeMS2iqw/edit#heading=h.xvwzye5fndkg)

STM Hardware Development:
* [AN4661 Getting started with STM32F7 Series MCU hardware development](https://www.st.com/resource/en/application_note/an4661-getting-started-with-stm32f7-series-mcu-hardware-development-stmicroelectronics.pdf)
* [AN4938 Getting started with STM32H7{4,5}xI/G MCU hardware development](https://www.st.com/resource/en/application_note/an4938-getting-started-with-stm32h74xig-and-stm32h75xig-mcu-hardware-development-stmicroelectronics.pdf)
* [AN5419 Getting started with STM32H7{2,3}... Line hardware development](https://www.st.com/resource/en/application_note/an5419-getting-started-with-stm32h723733-stm32h725735-and-stm32h730-value-line-hardware-development-stmicroelectronics.pdf)
* [AN4879 USB hardware and PCB guidlines using STM32 MCUs](TODO)
* [AN5225 Introduction to USB Type-C® Power Delivery](TODO)
  * See Section 10 - `Type C with no Power Delivery`

STM Documents:
* [DS11853 Rev 9 - STM32F2{2,3}xx Datasheet](TODO)

STM Discussions:
* [Forum: Recommended schematic review](https://community.st.com/t5/stm32-mcus/how-to-conduct-a-stm32-self-schematic-review-pt-1/ta-p/49593)
  * [Part 2](https://community.st.com/t5/stm32-mcus/how-to-conduct-a-stm32-self-schematic-review-pt-2/ta-p/49595)
* [StackOverflow STM32](https://electronics.stackexchange.com/questions/611915/schematic-review-for-stm32-basic-development-board)
* [STM32 Design in KiCAD](https://vivonomicon.com/2018/05/05/your-own-hardware-designing-an-stm32-development-board/)

Schematic References:
* [Ksoloti Core 0.6](https://github.com/ksoloti/ksoloti)
  * [STM32F429ZGT6 (LQFP 144)](https://www.st.com/en/microcontrollers-microprocessors/stm32f429zg.html#overview) with SDRAM
  * [Schematics](https://ksoloti.github.io/5-resources.html)
* [Daisy Seed](TODO) - schematic not available
* [Teensy 4.1](TODO) - Renesas, not STM32
* [Blue Pill](https://stm32-base.org/boards/STM32F103C8T6-Blue-Pill.html)
  * [More on Blue Pill](https://www.hackster.io/MakerIoT2020/remaking-the-stm32-blue-pill-d3ae30)
* [Pimoroni Pico Audio Pack PIM544](https://shop.pimoroni.com/products/pico-audio-pack?variant=32369490853971)
  * [PCM5102A I2S DAC](https://www.ti.com/product/PCM5102A)
  * [PCM5102 and STM32](http://elastic-notes.blogspot.com/2020/11/use-pcm5102-with-stm32_76.html)
  * [Wikipedia I²S](https://en.wikipedia.org/wiki/I%C2%B2S)
* [ubld.it MIDI-Mini Breakout Board](https://ubld.it/midi-mini)


# Schematic Notes

* Using STM32F722xx with LQFP64 pinout

* Vbat - See DS11853 Rev 9 - Connect to "VDD when no external battery 
  and [no] external super-capacitor are present."


## USB-C in 2.0 Mode

* [Wiring post](https://www.eevblog.com/forum/projects/usb-type-c-(usb2-0)-wiring/)
  - A6 to B6 (D+) to D+ on the micro
  - A7 to B7 (D-) to D- on the micro
  - A4 to A9 to B4 to B9 (VBUS) to VCC (+5V) on the micro
  - A5 (CC1) to GND via 5k1 Resistor
  - B5 (CC2) to GND via another 5k1 Resistor
  - A1 to A12 to B1 to B12 (GND) to Ground
* [Another wiring post](https://www.eevblog.com/forum/projects/minimal-wiring-for-usb-c-jack/)
* [Kicad Post](https://forum.kicad.info/t/how-to-connect-a-ft232rl-to-a-usb-type-c-connector/18557/2)
* Where is the official specification for this?
* [GND & Shield](https://electrical.codidact.com/posts/279876/285004#answer-285004)

## Power

* [STM LD1117](https://www.st.com/resource/en/datasheet/ld1117.pdf) - 800mA
* [STM LD39050](https://www.st.com/resource/en/datasheet/ld39050.pdf) - 500mA
* [AMS1117-3.3](http://www.advanced-monolithic.com/pdf/ds1117.pdf) - 1A
* [AP2161](https://www.digikey.com/en/products/base-product/diodes-incorporated/31/AP2161/66238)
  * C176957 & C2149802

## Misc Components

* Ferrite Bead: 
* [16 MHz Oscillator](https://jlcpcb.com/partdetail/YangxingTech-X322516MMB4SI/C112972)
* USB-C ESD Protection: STM USBLC6-2
* [32k Crystal Notes](https://community.st.com/t5/stm32-mpus-products/lse-crystal-for-st32mp1-fc-135-38-768-khz/td-p/679119)
  * [Phil's Lab Math](https://youtu.be/aVUqaB0IMh4?t=1619&si=jmx2GFCgxkBLzdWy)
  * Load Capacitors
  * 7pF osc
  * Estimate 3-5pF of stray capacitance
  * 7 - 5 = 2 x 2 = 4 pF
  * 7 - 3 = 4 x 2 = 8 pF
  * 7 - 4 = 3 x 2 = 6 pF
* [Push Button Wiring](https://www.youtube.com/watch?v=JZsC34jfbEg)
* [TRS MIDI](https://midi.org/specification-for-use-of-trs-connectors-with-midi-devices)
* [ubld.it MIDI Breakout Schematic](https://ubld.it/wp-content/uploads/2023/10/MIDI_BOB_MV_Mini_Schematic_RevA.pdf)
* [DeftAudio Teensy MIDI Schematic](blob:https://github.com/08e4b098-b5fc-4c80-bbc1-2535837214dd)
* [Component Search Engine](https://componentsearchengine.com/)
* [JLC Component Catalog](https://yaqwsx.github.io/jlcparts/#/) Third party tool
* Resettable fuse: SMD0603-200L

## Opto-Isolator Alternatives

* [Toshiba TLP2361](https://toshiba.semicon-storage.com/us/semiconductor/product/isolators-solid-state-relays/detail.TLP2361.html)
  * Package: SOIC-6
  * [Mouser](https://www.mouser.com/ProductDetail/Toshiba/TLP2361TPLE?qs=HVbQlW5zcXUn%252BfokbzIatg%3D%3D&utm_id=10348264317&gad_source=1)
  * [LCSC](https://www.lcsc.com/product-detail/Optocouplers---Logic-Output_TOSHIBA-TOSHIBA-TLP2361V4-TPL%2CE_C123773.html)
* [Vishay VO0600](https://www.vishay.com/en/product/84607/)
  * Package: SOIC-8
  * [LCSC](https://www.lcsc.com/product-detail/Logic-Output-Optoisolators_Vishay-Intertech-VO0600T_C5830851.html)
  * [Mouser](https://www.mouser.com/ProductDetail/Vishay-Semiconductors/VO0600T?qs=xCMk%252BIHWTZMQ6VardsKvcQ%3D%3D)
* [TI ISOM8710](https://www.ti.com/product/ISOM8710)
  * Package: SOIC-5
  * [Mouser](https://www.mouser.com/ProductDetail/Texas-Instruments/ISOM8710DFFR?qs=1Kr7Jg1SGW%2Fig%2FeXrQnwtQ%3D%3D)
  * [LCSC](https://www.lcsc.com/product-detail/Modules_Texas-Instruments-ISOM8710DFFEVM_C17217617.html) -
    not currently available
* [TI ISOM8711](https://www.ti.com/product/ISOM8711)
  * Package: SOIC-5
  * [Mouser](https://www.mouser.com/ProductDetail/Texas-Instruments/ISOM8711DFFR?qs=HoCaDK9Nz5f4%252B%2FwLVK60Ow%3D%3D)
  * [LCSC](https://www.lcsc.com/product-detail/Optocoupler-Emulator-Optocoupler-Replacement_Texas-Instruments-ISOM8711DFFR_C22399679.html) - 
    not currently available
* [TI ISOM8110]() - also look at ISOM8115
  * Package: SOIC-4
  * [LCSC](https://www.lcsc.com/product-detail/Optocoupler-Emulator-Optocoupler-Replacement_Texas-Instruments-ISOM8110DFGR_C22431318.html) -
    not currently available
  * [Mouser](https://www.mouser.com/ProductDetail/Texas-Instruments/ISOM8110DFGRQ1?qs=IKkN%2F947nfCR7%2Fv949luTw%3D%3D)
  * [Mouser 8115](https://www.mouser.com/ProductDetail/Texas-Instruments/ISOM8115DFGRQ1?qs=olJun0bQHM8UNDPuYUCEKw%3D%3D)
* [H11L1]()
  * Available in DIP models, e.g., PDIP-6
  * Mouser doesn't stock Everlight models
  * [Mouser OnSemi H11L1M](https://www.mouser.com/ProductDetail/onsemi-Fairchild/H11L1M?qs=P36CEcFBmYxn5ViwkIckpw%3D%3D)
  * Everlight [LCSC](https://www.lcsc.com/product-detail/Logic-Output-Optoisolators_Everlight-Elec-H11L1S-TA_C78589.html) - plenty in stock, SMD


# DF0997 UART/I2C Display

I tested this with an FT-232 and RealTerm on Windows.
[GitHub](https://github.com/DFRobot/DFRobot_LcdDisplay)
has library source code. [Wiki](https://wiki.dfrobot.com/_SKU_DFR0997_I2C_UART_2_inch_Color_Serial_Command_Screen#target_16)
has documentation.

* UART: 9,600 bps 8-N-1
  * I tried 57,600 but it seems fixed at 9,600
* Clear screen: 0x55 0xAA 0x01 0x1D
* Draw a black pixel: 0x55 0xAA 0x0E 0x02 0x00 0x00 0x00 0x00 0x60 0x00 0x60 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF
* Set background color to green: 0x55 0xAA 0x04 0x19 0x00 0xFF 0x00
  * This keeps the various black pixels still black (!)
* If you plug in a USB-C to your Windows computer, it shows up as 
  a USB drive with 8MB capacity
  * Lots of `.png` files in various directories
  * They call this the "U-Disk"


# KiCAD 8 Notes

## Plugins

* [JLC PCB Fabrication Toolkit](https://github.com/bennymeg/Fabrication-Toolkit)
* [KiCAD JLCPCB tools](https://github.com/Bouni/kicad-jlcpcb-tools)
* Alternate Kicad Library
* Generic Symbol Library
* 4ms Kicad Libraries
* Schematic Blocks Plug-In
* Simple Libraries
* Git plugin
* PCBWay
  * Fabrication Toolkit
  * Plug-in for KiCad


## EasyEDA imports

* Use [this tool](https://github.com/uPesy/easyeda2kicad.py)


## Copper Zones

* After placing them, you have to calculate their fills
  before they'll do anything!
  * Hit `b` hotkey


# Git for Windows notes

## Powershell

* `start-ssh-agent.cmd`


# JLCPCB Notes

Using the JLCDFM automated analyzer:

* Silkscreen line width needs to be > 0.15mm
  * This means a lot of letters are too thin by default
* Ensure that silkscreen does not cover any holes
* Have at least 3.05mm from any through hole components to
  SMD components (THT to SMD)
* Slot widths have to be 0.81mm
  * The USB-C slots seem to be 0.6mm
* All Vias are warned as unconnected
* The micro and Ohm unicode symbols do not import into JLCPCB BOM properly

KiCAD 8 notes:
* Create a special field for JLCPCB manufacturing:
  * File -> Schematic Setup → General → Field Name Templates
  * LCSC - JLC PCB Part number
  * DPFNOTES - Doug's notes on the part
  * DPFURL - URL to a spec sheet on the part

Utilities:
* [Component Catalog](https://yaqwsx.github.io/jlcparts/#/) - 3rd party site
* [Importer](https://forum.kicad.info/t/post-v7-new-features-and-development-news/40144/29)
* [EasyEDA loader](https://forum.kicad.info/t/footprints-from-jlcpcb/47051/8)

# JLCPCB Components

Components:
* [STM32F722RET6](https://jlcpcb.com/partdetail/Stmicroelectronics-STM32F722RET6/C118207)
  * LCSC C118207
* [Mini pushbutton](https://jlcpcb.com/partdetail/XkbConnection-TS_1187A_B_AB/C318884)
  * Mfr TS-1187A-B-A-B XKB
  * LCSC C318884
* [32k Crystal](https://jlcpcb.com/partdetail/SeikoEpson-Q13FC13500004/C32346)
  * LCSC C32346