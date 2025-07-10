# Raspberry Pi 500 Laptop

Have you ever wanted to make a laptop out of a Raspberry Pi? Yeah? Well, that’s stupid.... Anyways I did and here is how.

It's actually not *that* hard to do make. I tried as much as I could with this project to **NOT** re-invent the wheel and use commercially available solutions when possible.

## Why use a Raspberry Pi 500?

I chose the Raspberry Pi 500 for this project because it is the Pi closest to already being a laptop. It has all of it's IO on one side of the board (which is important), comes with a low-profile keyboard, and even supports an M.2 SSD if you're brave enough. The only major things lacking from the Raspberry Pi 500 to turn it into a laptop is a battery and a display.

There **ARE** more powerful single board computers that could have been used, but they would have required a lot to become a laptop and for what I use a laptop for, the Raspberry Pi 5 is plenty powerful.

## 11.6-inch LCD Display

The display used in this project is a kit from AliExpress that includes a 1080p 11.6-inch display that is normally powered via USB. This display is exactly the right size for the Raspberry Pi 500 as it is the same size as the keyboard. Since the HDMI will need to be routed inside of the case and there isn't much space, a DIY HDMI cable is required. The USB cable to power the display will also need to be run internally, but can be replaced by two 22-gauge wires connected to carry power.

## Batteries & UPS

The batteries used in this project are 10,000mAh 1260110 LiPo Batteries. I have linked the ones I bought on AliExpress, but buy them at your own risk. I have no clue how good their standards are. If you can find a better place to source them, please tell me because buying random batteries off AliExpress feels sussy.

Instead of designing a battery management system for the Pi from scratch, I decided to go with a Raspberry Pi 5 UPS module as that is basically the same thing as what a laptop has. The reason I went with a more expensive UPS module rather than a cheap one is for two reasons: It needs to work with only 2 batteries, and needs to be able to deliver 25W to the Pi. A lot of the cheaper UPS modules cannot actually deliver 25W to the Pi even though they say they "Support Raspberry Pi 5" *cough cough waveshare*.

## Active Cooler

The passive cooler inside of the Raspberry Pi 500 is too big to fit inside the case so an active cooler has to be used instead. The Raspberry Pi 500 does not have a fan header, but you can use GPIO and a python script to control the fan.

## Laptop Hinge

This is one of the things that I meant by not re-inventing the wheel. You could get away with using a 3D printed hinge but honestly, I tried that and the experience was not great. Proper laptop hinges are available and the experience is so much better that it is worth the extra $32. No one likes a floppy laptop.

## Storage

If you don't want to spend extra money on an SSD, you can use the SD card that comes with the Raspberry Pi 500. If you do, there are two options:

### M.2 to USB Enclosure
There are some cheap M.2 to USB enclosures on amazon that can be used and strapped to the back of the laptop. There is no need to buy a high-speed SSD or Enclosure if you do this method because you will be bottlenecked by the USB 3.0 speeds before anything else.

### Add M.2 Slot to the Raspberry Pi 500
If you feel adventurous and have a Hot Air Gun and a microscope, you can add a M.2 Slot to the Raspberry pi 500 for an extra $20. The board itself has all the PCB footprints to support an M.2 drive. It is just missing a couple dozen surface mount components. Adding the slot is **NOT** easy to do though and not recommended if you don't have a lot of patience and soldering experience. There are a dozen 0201 components you need to solder on the board as well as a dozen other tiny components. I managed to do this without any surface mount experience, but it was far from easy.

## Parts List (All prices in CAD)

This list **DOES NOT INCLUDE** consumables like 3D printing filament, screws, solder or wire.

* [Raspberry Pi 500](https://www.raspberrypi.com/products/raspberry-pi-500/) $90
* [11.6 inch LCD Display and Driver](https://www.aliexpress.com/item/1005007374742213.html?spm=a2g0o.order_list.order_list_main.5.871c1802cOe4MF) $60
* Two [10,000mAh 1260110 LiPo Batteries](https://www.aliexpress.com/item/1005005251229107.html?spm=a2g0o.order_list.order_list_main.20.871c1802cOe4MF) $34
* [Framework 13 inch Laptop Hinge](https://frame.work/ca/en/products/display-hinge-kit?v=FRANFB0002) #32
* [Raspberry Pi 5 UPS Board](https://www.amazon.ca/dp/B087FXLZZH) $87
* [Raspberry Pi 5 Active cooler](https://www.amazon.ca/dp/B0CQYGHL9D) $16
* DIY HDMI Cable (three parts)
  *  [10cm Ribbon Cable](https://www.adafruit.com/product/3560) $1.50
  *  [Micro HDMI Plug](https://www.adafruit.com/product/3557) $6.50
  *  [Mini HDMI Plug](https://www.adafruit.com/product/3552) $6.50
* Optional Parts
  * [Cheap USB M.2 Enclosure](https://www.amazon.ca/dp/B0BXLFXLDS) $26
  * [Cheap M.2 SSD](https://www.amazon.ca/dp/B07ZGK3K4V) $30

### Sub total: $334 CAD (+$56 for SSD)

## Required Tools

* Basic Soldering gear (Soldering Iron, Solder, Wire strippers)
* 3D printer (OR 3D printing service like JLCPCB)
* Wire Cutters
* Kapton tape

# Instructions

## Disassemble the Raspberry Pi 500

The Raspberry Pi 500 has **no screws** holding the case together. It is held together entirely by clips between the keyboard and the bottom case. To disassemble, insert a flat head screwdriver into the gap between the keyboard and the bottom case and push the clips in to release the keyboard. Work around the entire case doing this. **DO NOT FORCE THE KEYBOARD OFF**. There is a ribbon cable connecting the keyboard to the Raspberry Pi 500 that needs to be detached before continuing.

Once you have the case open and the keyboard disconnected, there are 4 screws that need to be undone. After that the board can be removed from the bottom half of the case and the passive cooler can be removed.

## Preparing the Raspberry Pi 500 board

If you don't care about having the GPIO connector available on your laptop, I would recommend cutting it off as it will make connecting all of the required GPIO pins easier. I also removed the Ethernet port on my Raspberry Pi since it was really tall and interfered with a previous case design, but that may not be necessary anymore.

You will also need to solder on some 22-gauge wires onto a USB port to power the fan and the display driver. I would recommend using the USB 2 Port as it has a simpler Pin out. Solder 2 wires onto the 5V line and 2 onto one of the grounds. I would recommend first twisting and soldering the two wires together and then attaching them to the pad. Leave yourself a lot of extra wire so that we can cable manage later.

## Preparing the UPS Board

To make the UPS board fit inside the case, we need to cut off almost all of the IO. You need to cut off the GPIO connector on both sides of the board, the 18650-battery connector, as well as the 5V in and 5V out connectors. The only connector that you **CANNOT** remove is the USB C connector. That is how we will charge the Raspberry Pi.

After all the connectors have been removed, you will have to bridge Pin 2 and 4 (the 5V Pins) as well as two GND Pins (I bridged 30, 32, and 34). These will function as the 5V and GND lines for the Raspberry Pi and will need to be connected to the same pins on the Raspberry Pi 500. I would recommend waiting until it is installed in the case before doing this though so you can properly size the wires.

There is also two jumpers you have to solder together for Auto start and auto charge.

It may be possible to use one of the 5V output connectors instead of GPIO, but im not sure. The UPS is designed to provide power through those GPIO pins and power accessories with the 5V output connectors so the 5V output connectors may have a current limit on them.

## Preparing the Batteries

IF your batteries came with a built-in protection circuit, it is important that you remove it. The UPS already has its own battery protection circuit and double dipping on protection circuits isn't good. If you don't remove it, I doubt anything catastrophic would happen, but it probably wont work as intended.

## 3D Printing a Lithophane

Since the LCD I chose has an exposed backlight, I designed the display case to fit a lithophane. To make a Lithophane, you can use [itslitho](https://itslitho.com/) to create a free lithophane from an image. The Lithophane itself should be 229.8mm wide by 94.8mm tall with a border of 5mm. The border should have a thickness of 2mm. The website can be a bit buggy though.

## Preparing the Case

If your 3D printer is big enough to print the top and bottom in one piece, then you can skip this step.

I designed the two bottom pieces to slot together tightly so you may need to do a little bit of cleanup on the pieces if your printer is not the best. Once you get the pieces connected and sitting flush, put your soldering iron on low heat and run it over the seam to fuse the two parts together. Same thing for the top pieces but the lithophane has no slots so just insert it into the lithophane cut out and fuse the seam.

If you are planning on finishing the case with paint or by polishing, I would recommend doing it now before we put any components inside the case.

## Measuring and cutting the wires

Now that we have all the parts prepped, screw the Raspberry Pi 500, Display Driver and the UPS into the case and put the batteries in below the boards. After that we will measure and cut each length of wire we need.

For the batteries and the UPS, you will need to use thicker gauge wire (I would recommend 20 or 18 gauge) since the Raspberry Pi 5 can draw up to 5A. If you don't have thicker gauge wire, you could use two 22-gauge wires connected in parallel instead.

Measure and cut wires between the batteries and the two positive and negative battery terminals of the UPS. Then between Pin 2 and 4 of the UPS and Pin 2 and 4 of the Raspberry Pi 500. Do the same thing for the GND wires (I did pin 30 and 34).

For the Display driver, we will be connecting it to one set of wires that we pulled off the USB port. Grab one pair of wires from the USB port and bring the 5V wire to the top of the top left capacitor (easier to connect there than the USB port itself) and the GND to the leftmost or rightmost pad on the USB C port. Leave enough wire to be able to cable manage and then trim the extra.

## Connecting the Batteries and UPS

Before you continue any further, remove the boards from the case and make sure that the batteries you are going to use are charged to the same level. Measure with the voltage with a multimeter and if the batteries are more than 0.1V apart **DO NOT USE THEM**.

Take the Boards out of the case and solder the wires into place that you measured and cut. If you have a proper battery strip welder, I would recommend using that instead of a soldering iron. If you use a soldering iron be as quick and don't do everything at once (tin the wire beforehand, tin the strip, let the battery cool down, and then connect both quickly) to avoid heating up the battery too much.

When soldering the UPS to the Raspberry Pi 500, make sure that you are connecting both Pin 2 and 4 together as well as two grounds. GPIO pins are technically only rated for 2-3A so we need to use both of the 5V pins.

Put all the boards back into the case and solder on the Display Driver cables. The 5V cable goes to the top of the leftmost capacitor, and the GND goes to the leftmost or rightmost pad on the USB C connector. These connections are a lot smaller and more fragile so it is best to do it while it is in the case.

## Connecting the Fan

Since the Raspberry Pi 500 doesn't have a fan port, we will need to take the connector off and manually solder our own wires in. The red (5V) and black (GND) should go to the other pair of wires we pulled off the USB port, and the yellow wire (PWM) should go to GPIO Pin 6. 

There is no proper mounting holes for the fan so to secure it I would recommend just Kapton taping it to the board. Some sacrifices need to be made when using off the shelf components.

## Mounting the Display and hinge

It is almost impossible to attach the ribbon cable for the display after installing so make sure to do it now. There are 8 M2 screws to hold the Display inside of its case that you can screw in now. I would also recommend screwing the hinge into the display side of the case first as it is easier to screw the bottom side.

If you are having trouble screwing the hinge in while holding it, try to screw the screws in before putting the hinge on to create the threads.

## Final touches

The only thing left to do at this point is connect the ribbon cables for the display and HDMI, cable managing them the best you can and connecting the keyboard. I would recommend folding the Display drivers ribbon cable loosely and then taping it to itself with Kapton tape.


## OPTIONAL Storage

If you want an external SSD you can double sided tape or velcro the external SSD to the top side of your case.

If you are adventurous enough to want to solder the M.2 Drive on, here is a rough guide/parts list on how to do it by [ChoptecOfficial](https://x.com/ChoptecOfficial/status/1868350222671478982). I will update this later with a proper tutorial on how I did this.

# Software

The only special software required for it is this [Raspberry Pi 5 GPIO Fan Script](https://github.com/franganghi/Raspberry-Pi5-PWM-Fan-Control) which can easily be installed.
