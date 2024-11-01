# MIDI Synthesizer Proof of Concept 1

**Feedback is very welcome!**

* Author: [Douglas P. Fields, Jr.](mailto:symbolics@lisp.engineer)
* My portions Copyright 2024 Douglas P. Fields, Jr.
* My portions License: Creative Commons Attribution-ShareAlike 4.0
  * AKA `CC BY-SA 4.0`
  * [See LICENSE.md](LICENSE.md) or [CC site](https://creativecommons.org/licenses/by-sa/4.0/deed.en)
* Started 2024-09-28
* Last updated 2024-10-25

Overviews:
* Front 3D View
  ![Front 3D View](stm-midi-poc1-3d-front-head-on-1.png)
* [Schematic PDF](stm-midi-poc1.pdf)
* [Board Plots as PDF](plots/stm-midi-poc1__Assembly.pdf)
* [Interactive BOM](bom/ibom.html)

Design documents:
* [Design notes](Design.md)
* Designed in [KiCAD 8](https://www.kicad.org/)
* LCSC part numbers included for assembly by [JLCPCB](https://jlcpcb.com/)


# Production Runs

## Run 1

* Submitted: 2024-10-27
* Git Commit: `6f9e281abe9c22ef3b995376c3df42217fc04524`
* Producer: JLCPCB
* Boards: 5
* Assemblies: 2
* [BOM](jlcpcb/production_files/BOM-stm-midi-poc1.csv)
* [CPL](jlcpcb/production_files/CPL-stm-midi-poc1.csv)
* [Gerbers](jlcpcb/production_files/GERBER-stm-midi-poc1.zip)
* JLCPCB Corrected Part Placement
  ![JLCPCB Corrected Part Placement](9042618026565632-Produce_DanZhi.SMT_Snapshot.Top.8392316A_Y2.SMT024102760115.png)
* [JLCPCB Submission](<jlcpcb-production/run1-20241027/stm-midi-poc1 6f9e281abe9c22ef3b995376c3df42217fc04524_Y2.zip>)
* Status: Production complete; in DHL's hands for delivery Nov 8


# Miscellaneous Notes

* Footprints, models, etc., by their respective authors
* Some footprints, schematics, models are from these sources:
  * [Component Search Engine](https://componentsearchengine.com)
  * [Snap EDA](https://snapeda.com)
  * [EasyEDA](https://easyeda.com)
* Useful tools:
  * [EasyEDA2KiCAD](https://github.com/uPesy/easyeda2kicad.py)

# KiCAD Configuration Notes

Using EasyEDA2KiCAD:

* Create a Path Substitution
  * Use main KiCAD window: Prefernces -> Configure Paths...
  * `EASYEDA2KICAD`
  * [Git Repository](https://github.com/LispEngineer/KiCAD_Libraries)
* Create a Footprint Library
  * `easyeda2kicad` Nickname
  * `${EASYEDA2KICAD}/easyeda2kicad.pretty`
* Create a Symbol Library
  * `easyeda2kicad` Nickname
  * `${EASYEDA2KICAD}/easyeda2kicad.kicad_sym` Library Path

# Status

* Schematic: Done
* LCSC part IDs: Almost Done
  * Need non-Red LEDs
* Schematic symbols: Done
* Footprints: Done
* 3D models: Done
* PCB Layout: Done
* Production 1 run: Done - in shipping


## TODOs

* Find a much smaller Opto-isolator for MIDI than the one chosen here
* Use a 4-pin 32kHz clock?
* RN1 footprint and 3D model look a little bit off - footprint is a bit too small?
* Test points/pins

# Board Layout Notes

4-layer design with Signal/GND/GND/Signal for EVT board.

Will do most important routing first on the top copper layer:
* Decoupling/bypass capacitors
* Clock signals
* High speed signals
  * USB
  * DAC
  * SWD

Remaining signals will be routed using "Manhattan routing."
That is, one signal layer will run up/down, the other will
run left/right, mostly.
* Top layer: up/down
* Bottom layer: left/right

After that, do these routings:
* Audio signals
* MIDI signals
* SPI
* I²C
* UI (Buttons, LEDs)
* GPIO
* Power

Fill in some positive power areas with fill.

Finally, the signal layers will be filled with GND at the end,
and the ground planes should be stitched together with lots
of vias.

## After Layout Is Done

* DRC check
* Cleanup Tracks & Vias


# BOM Notes

* Docs say you need a 4.7 uF ceramic capacitor with low ESR DS11853 Rev 9 page 105
  * Samsung CL10A475KO8NNNC works *but* Datasheet doesn't say what the ESR is, just "low ESR"
  * [Notes on the Cap](https://community.st.com/t5/stm32-mcus-products/how-supply-stm32f446ret6/td-p/635424)


# Notes for future

* Use fewer header types, they're all extended parts
* Find a smaller opto-isolator, or a dual one
  * Remember MIDI is < 50 kHz
* Don't use the Resistor Network - due to the Extended parts fee from JLC
  * OTOH there are no 56Ω resistors in the Basic parts library