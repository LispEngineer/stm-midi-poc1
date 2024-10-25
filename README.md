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

# Status

* Schematic: Done
* LCSC part IDs: Done
* Schematic symbols: Done
* Footprints: Done
* 3D models: Done
* PCB Layout:
  * Take 3 in progress
  * (Take 1 was a 2-layer PCB)
  * (Take 2 extended that to a 4-layer with two signal layers)
  * (Take 3 is a Manhattan routing manual re-do of the whole routing)

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

Finally, the signal layers will be filled with GND at the end.