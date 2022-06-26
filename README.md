
# Ender 3 S1: SKR Mini E3 V3.0 Installation
This guide covers the installation of the BigTreeTech SKR Mini E3 V3.0 into the Creality Ender 3 S1.



## Introduction

#### Why would anyone want to do this?
I started this project because I was bored and because I have a compulsive need to take 3D printers apart. There are, however, a few advantages:

1: Ender 3 S1 motherboards powered by the STM32F401 chip have only 256K of flash memory (compared to 512K in the STM32F103-powered variants). This means that there is not enough space for fully-featured Marlin firmware, and useful features like universal bed leveling (UBL) must be compromised. The SKR Mini E3 V3.0 is powered by STM32G0B0 or STM32G0B1 chips, and both have 512K of flash.
 
2: The SKR Mini supports Neopixel RGB LEDs, so if you want your setup to have that gamer aesthetic, you can do that, although you may need an additional cheap add-on board to do that depending on how many lights you're sporting. This guide does not cover the addition of these lights, but if you have the official Creality light bar for the S1, this guide will cover its installation.

3: The stock Ender 3 S1 motherboard uses TMC2208 stepper drivers. These are not compatible with linear advance, which is a valuable tool for improving print quality (https://help.prusa3d.com/article/linear-advance_2252). The SKR Mini uses TMC2209 drivers, which are compatible.

4: The stock Ender 3 S1 motherboard favors proprietary ribbon cables over standard connections. Only the bed thermistor and heater connections are standard. The SKR Mini uses only standard connections, so this opens the door for other extruder/hotend combinations if one so chooses.

#### Umm actually, I use Klipper on the stock S1 and I use linear advance all the time.

No you don't. You use pressure advance, which is a similar technique that attempts to accomplish the same thing as linear advance. See here for an explanation of the differences: https://3dprinting.stackexchange.com/questions/18681/what-is-the-difference-between-linear-advance-and-pressure-advance?rq=1

#### Do I lose anything by installing this board?

The Creality laser engraver attachment will not work with this board. It might be possible to get it working, but I'm not touching that and I doubt anyone else will.

The SD card and USB port cutouts in the faceplate do not align with the SKR Mini, so you'll have to either leave it off or do some cutting. If only there was a large community of makers and designers out there that could help with this...

#### What firmware is compatible with this board?

I used mriscoc Professional Firmware, and I've made this code and build available, but any firmware compatible with the S1 (including Klipper) should work with minimal porting.

https://github.com/mriscoc/Ender3V2S1


## Materials

To do this, you will need the following:

1. SKR Mini E3 V3.0 (https://www.biqu.equipment/en-fr/products/bigtreetech-skr-mini-e3-v2-0-32-bit-control-board-for-ender-3)

2. 4 x stepper motor cables. I used these: https://www.amazon.com/dp/B09JVKTQW1

3. 2 x limit switch cables. For the x limit switch, I would recommend no shorter than 50 cm. I made my own limit switch cables but something like this would work fine: https://www.amazon.com/SOOWAY-Printer-Limited-Mechanical-Accessories/dp/B07XDQ96FQ. To be clear, you don't need new limit switches, just the cables. I couldn't find a cable-only listing.

4. Zip ties for cable management

5. Jumper wires. This is the easiest way to rewire the DACAI (stock S1) screen for use with the SKR mini. More elegant solutions can be found with some Googling, but this is what I used: https://amazon.com/gp/product/B07GD2BWPY

6. Filament sensor cable
This one is a little tricky. The stock cable connects to the sensor with a 3 pin xh 2.54 connector and to the expansion board in the printer with a 3 pin ph 2.0 connector. We will be removing the expansion board and connecting to the SKR mini directly using an xh 2.54 connector, so you have two options: find a cable with a pH 2.0 3 pin plug and a 3 pin xh 2.54 connector that is long enough to reach the SKR from where the expansion board is, or get a really long cable that has 3 pin xh 2.54 connectors on both sides and go straight from the sensor to the board. I can't find any examples of either cable available for sale, so you'll have to do some hunting if you don't want to make your own.

7. Official Creality LED bar extension cable
This is another tricky one. The LED bar plugs into the expansion board with a 3 pin xh 2.54 connector (although only 2 pins are used). We need to extend the cable down to the power supply so we can connect it directly. Something like this will work with some minor modification that I'll cover later, but you might need to link both of them together to get enough length: https://www.amazon.com/RuiLing-Connector-Extended-Quadcopter-Rechargeable/dp/B07K452L5Y

8. Sprite Extruder Breakout Cable

This part is the trickiest one to source. As far as I know, the only way to get this cable is to buy the Sprite Extruder Pro full upgrade kit (https://www.3djake.com/creality-3d-printers-spare-parts/sprite-extruder-pro-upgrade-kit). It's not cheap and it can be hard to get, but it might be a good option if you were planning on getting a Sprite Pro anyway. Barring that, you'll have to make your own. If you want to make your own, you'll need the following:

   * 26 AWG, 1.0 mm pitch, AWM2651 ribbon cable with at least 24 wires, 1.16 m long. I used this: https://www.ebay.com/itm/334418583959. It's 28 AWG but I couldn't find any 26 AWG. 28 works fine though.

   * 1 x 24-pin IDC female header socket connector, 2.0 mm pitch.    https://www.aliexpress.com/item/2251801537002415.html

   * 2 x ferrules
   
   * 2 x xh 2.54 2 pin connectors

   * 1 x xh 2.54 3 pin connector

   * 1 x xh 2.54 4 pin connector

   * 1 x xh 2.54 5 pin connector

   * xh crimps, crimping tool, ferrule crimping tool

Assemble the cable per the following diagram. Wires labeled NC are not used. They can be cut off and discarded.

![279457776_528201855413994_5611961213153261827_n](https://user-images.githubusercontent.com/21251502/175834915-9b917591-e566-4f89-9b6c-b4fb4ac3028d.jpg)


## Installation Procedure

1. Unplug the cables from all stepper motors and limit switches. Unplug the sprite extruder cable.

2. Remove the faceplate (the plate where the SD card and USB port holes are) and bottom of the S1. Be careful when removing the bottom. The motherboard cooling fan must be unplugged before it can be removed.

3. Unplug all cables from the stock S1 motherboard. Note that many connections are covered in hot glue. This must be removed.

4. Unscrew the expansion board (the board where the z axis motor, LED light bar and filament sensor plugs into).

5. Remove all cables, and the original motherboard, from the printer except for any cables connected to the power supply, the bed thermistor cable and the bed heater cable.

6. Connect the stepper motor cables to the x, y and both z stepper motors. Feed the cables down to the motherboard area through the same holes that the original cables used. Do the same with the 24-pin end of the sprite breakout cable.

7. Connect the limit switch cables to the x and y limit switches, and feed them down to the motherboard area.

8. If you have the Creality LED light bar, prepare and install your extension cable by doing the following:
  
  * Plug the light bar's xh 3 pin connector into the 3 pin socket of your extension cable.

  * Cut off the unused 3rd cable and discard it.

  * Cut off the 3 pin connector at the end of the extension cable so that the 2 remaining wires are free.

  * Strip the wires so that about 3-5 mm of bare wire is showing.

  * If you look at the power supply, you will see some screw terminals that are labeled V+ and V-. Unscrew any unused terminal that is labeled V-. Place the bare wire that extends from the middle position of the 3 pin connector used by the LED bar under the screw terminal, and screw it down until it is secure. Do the same with the other wire using an unused V+ terminal.

9. For the filament sensor, if you decided to use a long 3 pin xh male-male connector, connect this cable to the sensor and feed it down to the motherboard area using the same channels that the stock cable used. If you used the extension cable connect it to the stock ph 2.0 connector and feed the other end down to the motherboard area. In either case, make sure the connecter that reaches the motherboard is configured per the following diagram:

![filament sensor diagram](https://user-images.githubusercontent.com/21251502/175834935-5977a9e7-3129-4e54-9695-f66fa25f39d8.png)

10. Connect all cables to the SKR mini per the following table:

![wiring diagram](https://user-images.githubusercontent.com/21251502/175834947-6702b760-99b9-4b7f-9450-cad1b066bfbb.png)


11. The following screen instructions are assuming you've plugged the screen in like so:

![PXL_20220626_210406185](https://user-images.githubusercontent.com/21251502/175834974-c92db4a3-fd3d-4258-a132-0d76be6cfc05.jpg)


  11a. Plug jumper wires of the specified colors into the header on the SKR mini labeled EXP1, and into the end of the screen connector cable, per the following diagram:

![Screen diagram](https://user-images.githubusercontent.com/21251502/175834984-fdc67468-457d-467a-89bc-42fb70ff5c49.png)

12. Screw the the SKR mini into the printer using whichever mount point you want. I chose the one that makes the SD card slot and USB port flush with the front of the printer.

13. Use zip ties to clean up your cable situation. Make sure there's enough room for the motherboard fan to rest above the SKR mini when the bottom is put back on.

14. Place the firmware.bin file included on this GitHub page onto the root of a micro SD card formatted in FAT32.

15. Put the bottom back on.

16. Put the micro SD card into the board and fire it up! If you did everything right, you should be good to go.

## Troubleshooting

# Nothing happens when I turn on the board

Check the connection from the power supply to the board. If you messed up the polarity (red wire left, black wire right), you probably blew the yellow 20 amp fuse that's on the board. Luckily, this is an easy and cheap replacement. These fuses can be found at any hardware or auto parts store. Don't ask me how I know.

# The filament runout sensor isn't working

If the filament runout sensor is wired correctly, it should blink briefly when powered on, show no light when empty and show a solid blue light when full. If the sensor never lights up, or if the light is permanently on, you have wired it incorrectly.

# [Printer component] isn't working

If you're using homemade cables, check the connections. It's a good idea to test the continuity of every wire on every cable you make with a multimeter. Make sure that the xh crimps are seated correctly and that they don't get pushed out when plugged into the board.
