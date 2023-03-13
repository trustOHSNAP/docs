You’ll need to be running KiCad version 6 or higher and also grab copies of some third-party symbol & footprint libraries:

- [SparkFun KiCad Libraries](https://github.com/sparkfun/SparkFun-KiCad-Libraries)
- [DigiKey KiCad Library](https://github.com/Digi-Key/digikey-kicad-library)
- [Savenlid KiCad Library](https://github.com/savenlid/kicad)

There will be a (hopefully) one-time annoying step of having to manually prepend namespace identifiers when adding each top-level directory inside the SparkFun and savenlid repos (“SparkFun-“ and “savenlid-“, respectively) but DigiKey already has a nice “dk_” prefix.

I had to create a couple of custom symbols and footprints that couldn’t be found anywhere else. I put these into the project-local ohsnap-symbols.kicad_sym file and ohsnap-footprints.pretty directory, respectively.

I’ve chosen specific models and footprints for every component and populated each of their “Model” and “Datasheet” fields. These choices primarily take into account the practicalities of manual assembly on the Voltera and, to a lesser degree, cost. If you feel that we should be using alternative components, let’s discuss.

For the OHSNAP Server PCB layout, there are a number of constraints. You’ll want to dig through the:

1. Voltera website (especially [circuit design guidelines](https://docs.voltera.io/v-one/v-one-fundamentals/circuit-design-guidelines))
2. [Voltera community forums](https://community.voltera.io)
3. [NUC980 datasheet](https://www.nuvoton.com/export/resource-files/DS_NUC980_Series_EN_Rev1.11.pdf)
4. Datasheets for the two LDOs (see links in schematic)
5. Datasheets for critical discretes, especially the XTAL

A few critical points on designing for printing on the Voltera:

- I’m hoping we can keep the board size at 3x4”. I made the appropriate Edge.Cuts boundary in the PCB already, but if you run out of room, we can go up to 4x5. Please try to leave at least 0.125” / 3mm margins along all sides - meaning no components, no holes, and no traces. 
- Minimum trace width is 8 mils (0.2032 mm). Minimum clearance is the same.
- Keeping all components on one side is ideal because then reflow is automatic, but I suspect that the bypass caps will end up needing to be underneath the MPU. All of that has to be manual soldering work so let’s keep it to a minimum.
- There are two supported hole sizes for now (I’m working on expanding this to four): Small holes for vias are 0.7mm via hole / 1.1mm via size, and large holes for thru-holes are 1.6mm via hole / 2.2 mm via size.
- KiCad hole to hole clearance should be 0.94mm
- We’ll almost certainly want a ground plane on the bottom. Here are ground plane settings: Set the Width setting to less than 14 mil (0.014”) and the Isolate setting to 16 mil or more.
- Use the Legacy zone fill strategy
- Remember that there is no separate silkscreen layer. Component references will be printed in the same conductive ink as the traces and pads, so try to position reference designators far enough away from components and traces so as not to cause shorts.