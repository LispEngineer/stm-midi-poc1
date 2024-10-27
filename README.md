# MIDI Synthesizer Proof of Concept 1

* Author: [Douglas P. Fields, Jr.](mailto:symbolics@lisp.engineer)
* My portions Copyright 2024 Douglas P. Fields, Jr.
* My portions License: Creative Commons Attribution-ShareAlike 4.0
  * AKA `CC BY-SA 4.0`
  * [See LICENSE.md](LICENSE.md) or [CC site](https://creativecommons.org/licenses/by-sa/4.0/deed.en)
* Started 2024-09-28
* Last updated 2024-10-25

More documentation to come.

# Miscellaneous Notes

* Designed in [KiCAD 8](https://www.kicad.org/)
* LCSC part numbers included for assembly by [JLCPCB](https://jlcpcb.com/)
* Footprints, models, etc., by their respective authors
* Some footprints, schematics, models are from these sources:
  * [Component Search Engine](https://componentsearchengine.com)
  * [Snap EDA](https://snapeda.com)
  * [EasyEDA](https://easyeda.com)
* Useful tools:
  * [EasyEDA2KiCAD](https://github.com/uPesy/easyeda2kicad.py)
* Feedback is welcome

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
* PCB Layout:
  * Take 3 in progress
  * (Take 1 was a 2-layer PCB)
  * (Take 2 extended that to a 4-layer with two signal layers)
  * (Take 3 is a Manhattan routing manual re-do of the whole routing)


## TODOs

* Find a much smaller Opto-isolator for MIDI than the one chosen here
* Use a 4-pin 32kHz clock?

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


# BOM Notes

* Docs say you need a 4.7 uF ceramic capacitor with low ESR DS11853 Rev 9 page 105
  * Samsung CL10A475KO8NNNC works *but* Datasheet doesn't say what the ESR is, just "low ESR"
  * [Notes on the Cap](https://community.st.com/t5/stm32-mcus-products/how-supply-stm32f446ret6/td-p/635424)


# Notes for future

* Use fewer header types, they're all extended parts
* 