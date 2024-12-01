# Atari Lynx for Analogue Pocket Core with support for Analogizer-FPGA adapter
* Analogizer V1.0.0 [30/11/2024]: Added initial support for Analogizer adapter (RGBS, RGsB,   YPbPr, Y/C, SVGA Scandoubler) and SNAC (included PSX DS/DS2). The PSX DS/DS2
  can be used in **Digital DPAD** mode (ignores the analog sticks, regardless of the ANALOG button setting on the controller) or in **Analog DPAD** mode (left analog stick is mapped to DPAD movements)
* Analogizer V1.0.0 [01/12/2024]: Added support for PSX Digital gamepads (SCPH-1010, SCPH-1080, Dance Mats?) 
  
Adapted to Analogizer by [@RndMnkIII](https://github.com/RndMnkIII) based on **budude2** Atari Lynx for Analogue Pocket (https://github.com/budude2/openfpga-AtariLynx).
The core can output RGBS, RGsB, YPbPr, Y/C SVideo and composite and SVGA scandoubler(0%, 25%, 50% 75% scanlines and HQ2x) video signals. 

| Video output | Status | SOG Switch(Only R2,R3 Analogizer) |
| :----------- | :----: | :-------------------------------: |     
| RGBS         |  ✅    |     Off                           |
| RGsB         |  ✅    |     On                            |
| YPbPr        |  ✅🔹  |     On                            |
| Y/C NTSC     |  ✅    |     Off                           |
| Y/C PAL      |  ✅    |     Off                           |
| Scandoubler  |  ✅    |     Off                           |

🔹 Tested with Sony PVM-9044D

| :video_game:            | Analogizer A/B config Switch | Status |
| :---------------------- | :--------------------------- | :----: |
| DB15                    | A                            |  ✅    |
| NES                     | A                            |  ✅    |
| SNES                    | A                            |  ✅    |
| PCENGINE                | A                            |  ✅    |
| PCE MULTITAP            | A                            |  ✅    |
| PSX DS/DS2 Digital DPAD | B                            |  ✅    |
| PSX DS/DS2 Analog  DPAD | B                            |  ✅    |

The Analogizer interface allow to mix game inputs from compatible SNAC gamepads supported by Analogizer (DB15 Neogeo, NES, SNES, PCEngine, PSX) with Analogue Pocket built-in controls or from Dock USB or wireless supported controllers (Analogue support).

All Analogizer adapter versions (v1, v2 and v3) has a side slide switch labeled as 'A B' that must be configured based on the used SNAC game controller.
For example for use it with PSX Dual Shock or Dual Shock 2 native gamepad you must position the switch lever on the B side position. For the remaining
game controllers you must switch the lever on the A side position. 
Be careful when handling this switch. Use something with a thin, flat tip such as a precision screwdriver with a 2.0mm flat blade for example. Place the tip on the switch lever and press gently until it slides into the desired position:
```
     ---
   B|O  |A  A/B switch on position B
     ---   
     ---
   B|  O|A  A/B switch on position A
     ---
``` 

The following options exist in the core menu to configure Analogizer:
* **240p** Check: Enable/Disable doubled resolution.
* **SNAC Adapter** List: None, DB15,NES,SNES,PCE,PCE Multitap, SNES swap A,B<->X,Y buttons, PSX (Digital DPAD), PSX (Analog DPAD).
* **SNAC Controller Assignment** List: several options about how to map SNAC controller to P1 Pocket controls. The controls not mapped to SNAC by default will map to Pocket connected controllers (Pocket built-in or Dock).
* **Analogizer Video Out** List: you can choose between RGBS (VGA to SCART), RGsB (works is a PVM as YPbPr but using RGB color space), YPbPr (for TV with component video input),
Y/C NTSC or PAL (for SVideo o compositive video using Y/C Active adapter by Mike S11), RGBHV for SVGA monitor Scandouble video output.

-----------------------------------------------------------------------------------------------------

# Atari Lynx for Analogue Pocket
Ported from the original core developed at https://github.com/MiSTer-devel/AtariLynx_MiSTer

Please report any issues encountered to this repo. Issues will be upstreamed as necessary.

## Installation
To install the core, copy the `Assets`, `Cores`, and `Platform` folders over to the root of your SD card. Please note that Finder on macOS automatically _replaces_ folders, rather than merging them like Windows does, so you have to manually merge the folders.

Place the Atari Lynx bios in `/Assets/lynx/common` named "lynxboot.img".

## Usage
ROMs should be placed in `/Assets/lynx/common`.

## Features

### Supported
* Fast Forward
* CPU GPU Turbo
* Orientation: rotate video by 90
* 240p mode: doubled resolution, mainly for CRT output (Rotation does not work in this mode)
* Flickerblend: 2 or 3 frames blending like real Lynx Screen

### In Progress
* Save States and Sleep

## Refresh Rate
Lynx uses custom refresh rates from ~50Hz up to ~79Hz. Some games switch between different modes. To compensate you can either:
* Live with tearing
* Buffer video: triple buffering for clean image, but increases lag
* Sync core to 60Hz: Run core at exact 60Hz output rate, no matter what internal speed is used
