# EZT3D-T1 3D Printer

I purchased this printer at [AliExpress](https://www.aliexpress.com/item/4001137583437.html) for $140.  I enjoy purchasing the least expensive printer kits I can find and seeing how far I can tweak them to produce good results.  The unit I received is a "T1-B1" model which is slightly different from the one picture in the installation video.

+ My other printer is a heavily modified Tronxy X1 which can now beat a Prusa i3 MK3 on the [AutoDesk FDM benchmark](https://github.com/kickstarter/kickstarter-autodesk-3d) at less than 25% of the cost.  The difference being that the Prusa is an all-day workhorse and the Tronxy requires constant tuning and tweaking to stay in calibration.

## Pre-Assembly Notes

+ The unit I purchased was an Australian 220V model.  I was able to use this in Canada on 110V with no issues by swapping out the line cord.  The power supply is unbranded and has no labelling or voltage selector, but there is what appears to be an active PFC IC inside on the board which indicates that it is voltage auto-sensing.  There was a sticker inside the box also that stated "110-220VAC".  

+ Regardless of where you are located, before building the printer, it is important to check for loose screws in the package.  A couple of the hardware bags had split and there was a loose metal T-Nut INSIDE the power supply.  Had I not caught that the magic smoke would have been released in short order.

+ Connect power to the power supply.  A green LED should light up.  Test the output voltage.  It should be very close to 12V (mine was 12.3).  There will be a lot of wiring around the power supply when done so it is best to check the power supply before building the printer.

+ If you want the flattest bed possible without purchasing glass, tape sheets of sandpaper (I had 120 and 220 grit, so I used those) to a piece of flat material (particle board shelving or countertops are manufactured straight and good for this).  Write a grid on the aluminum side of the bed in permanent marker to see where you have flattened.  Sand the aluminum across the sheets of sandpaper on your flat surface until the marker is gone.  It will be obvious which areas have been smoothed down and which aren't yet.  Mine was significantly concave and took a good 30-45 minutes of hard work to smooth out.  Credit to [this reddit thread](https://www.reddit.com/r/3Dprinting/comments/9fu812/sanding_my_warped_ender_3_bed_to_an_accuracy_of) for the idea!

+ The included carbon delta rods are of very poor quality.  They should be 200MM exactly from hole center to hole center.  The fisheyes screw into the hollow rods.  The rods in my kit did not have all of the fisheyes screwed in evenly so not only were they different lengths, they were all short of 200MM.  This causes a delta printer to have weird geometry problems.  In my case, there were areas of the bed where the print head would not get close enough to the bed to do a first layer.  In addition, two of the rod ends split when the fisheyes were tightened.  I put two zip ties over each split end to close them up and reinforce them and will be adding superglue for additional strength and to keep the fisheyes from rotating.

+ When assembling, make sure the ends of the aluminum extrusions are flush with the acrylic surfaces as per the installation video.  Once belts are installed they are under tension and the belts need to be removed to readjust their positioning.

+ The printer has no part cooling fan but has a header on the board for one.  If you have available wire/connectors, add a part cooling fan power lead to the wiring bundle as you are building the printer to avoid a lot of disassembly and wire movement to add one later

+ Out of the box the hotend puts a lot of heat into parts (moreso than other printers I've worked with) and prints very poorly.  In the "Upgrade Part Models" folder of this repository is a [copy of a duct from a thingiverse user](https://www.thingiverse.com/thing:4513844).  This redirects a small amount of the air from the hotend fan to act as part cooling and tremendously improves print quality as a stopgap until a proper part cooling fan can be installed.  If you have access to another printer, print and install this part as you build the printer.  If not, try to print this as soon as possible using the lowest temperature your filament can tolerate, heated bed at room temperature, and very low speeds.

+ The main board has the USB connector facing downward underneath the printer.  I recommend connecting the board to USB before building the printer, making sure it lights up and responds to an M503 command.  After the printer is built you will need either a right angle USB A adapter or feet to raise the printer enough to allow a cable to plug in and bend.  There is a model for feet in this repository.

## Control Board

+ The control board for the printer is an unbranded board with no visible part number. 

+ It uses an [STM32F103C8 CPU](https://www.st.com/resource/en/datasheet/stm32f103c8.pdf)

+ The stepper drivers are under heatsinks and I am assuming they are A4988 or similar.  XYZ are running 80 steps/MM.

+ The board seems to be running a very cut down, modified version of Marlin 1.0.  It does not respond to many common GCODE commands.  It uses a very small display and has a very limited menu system with no ability to adjust parameters other than temperature and print speed.  Features such as linear advance or mesh bed levelling are unavailable.  This severely limits the print quality that will be acheivable.

+ Marlin support for STM32 boards appears to be a mixed bag and given that, no documentation for the board and the unusual display used leaves little hope for an upgrade to Marlin 2.0.

## Extruder

+ The extruder is a plastic bodied unit with a single drive gear and an idler wheel.  Tension is not adjustable other than replacing the spring.  It appears to be a limiting factor in print speeds so far, with the motion system and hotend supporting more speed than it can keep up with.

## Hotend

+ The hotend is a low cost all-metal E3D V5 clone.  

+ It does not have a PTFE liner so should be suitable for materials such as PETG that require >240C temperatures.  

+ My unit has a poor fit between the heat break and heater block and requires frequent tightening to avoid filament seepage.  

+ The filament is hard to push through the transition between the upper heatsink and the heat break.  This does not help the already anemic extruder.  

+ The heater cartridge is slightly smaller in diameter than the bore in the heatblock.  I have seen this on other low cost-clones.  The heater cartridge can be shimmed with a couple of wraps of aluminum foil to acheive a tighter fit to the heat block and improve heat transfer.

## Frame

+ The acrylic frame is attached to the metal extrusions with only a few screws each.  There is significant flex and wobble.  There is a lot of potential for stiffener parts to be added to increase rigidity.