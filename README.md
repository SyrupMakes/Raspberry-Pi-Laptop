# Raspberry Pi 500 Laptop

Have you ever wanted to make a Laptop out of a Raspberry Pi? Yeah? Well thats stupid.... Anyways I did and here is how.

It's actually not *that* hard to do make. I tried as much as I could with this project to **NOT** re-invent the wheel and use commercially available solutions when possible.

## Parts List (All prices in CAD)

This list **DOES NOT INCLUDE** consumeables like 3D printing filament, screws, solder or wire.

* [Raspberry Pi 500](https://www.raspberrypi.com/products/raspberry-pi-500/) $90
* [11.6 inch LCD Display and Driver](https://www.aliexpress.com/item/1005007374742213.html?spm=a2g0o.order_list.order_list_main.5.871c1802cOe4MF) $60
* 2x [10,000mAh 1260110 LiPo Batteries](https://www.aliexpress.com/item/1005005251229107.html?spm=a2g0o.order_list.order_list_main.20.871c1802cOe4MF) $34
* [Framework 13 inch Laptop Hinge](https://frame.work/ca/en/products/display-hinge-kit?v=FRANFB0002) #32
* [Raspberry Pi 5 UPS Board](https://www.amazon.ca/dp/B087FXLZZH) $87
* [Raspberry Pi 5 Active cooler](https://www.amazon.ca/dp/B0CQYGHL9D) $16
* DIY HDMI Cable (three parts) $15 https://www.adafruit.com/product/3560 https://www.adafruit.com/product/3557 https://www.adafruit.com/product/3552
* Optional Parts
⋅⋅⋅⋅* [Cheap USB M.2 Enclosure](https://www.amazon.ca/dp/B0BXLFXLDS) $26
⋅⋅⋅⋅* [Cheap M.2 SSD](https://www.amazon.ca/dp/B07ZGK3K4V) $30

### Sub total: $334 CAD (+$56 for SSD)

## Required Tools

* Basic Soldering gear (Soldering Iron, Solder, Wire strippers)
* 3D printer (OR 3D printing service like JLCPCB)
* Wire Cutters


## Why use a Raspberry Pi 500?

I chose the Raspberry Pi 500 for this project because it is the Pi closest to already being a laptop. It has all of it's IO on one side of the board (which is important), comes with a low profile keyboard, and even supports an M.2 SSD if you're brave enough. The only major things lacking from the Raspberry Pi 500 to turn it into a Laptop is a battery and a display.

There **ARE** more powerful single board computers that could have been used, but they would have required a lot to become a laptop and for what I use a laptop for, the Raspberry Pi 5 is plenty powerful.

## 11.6 inch LCD Display

The display used in this project is a kit from Aliexpress that includes a 1080p 11.6 inch display that is normally powered via USB. This display is exactly the right size for the Raspberry Pi 500 as it is the same size as the keyboard. Since the HDMI will need to be routed inside of the case and there isn't much space, a DIY HDMI cable is required. The USB cable to power the display will also need to be run internally, but can be replaced by two 22 gauge wires connected to carry power.

## Batteries & UPS

The batteries used in this project are 10,000mAh 1260110 LiPo Batteries. I have linked the ones I bought on Aliexpress, but buy them at your own risk. I have no clue how good their standards are. If you can find a better place to source them, please tell me because buying random batteries off Aliexpress feels sussy.

Instead of designing a battery management system for the Pi from scratch, I decided to go with a Raspberry Pi 5 UPS module as that is basically the same thing as what a laptop has. The reason I went with a more expensive UPS module rather than a cheap one is for two reasons: It needs to work with only 2 batteries, and needs to be able to deliver 25W to the Pi. A lot of the cheaper UPS modules cannot actually deliver 25W to the Pi even though they say they "Support Rasppberry pi 5" *cough cough waveshare*.

## Active Cooler

The passive cooler inside of the Raspberry Pi 500 is too big to fit inside the case so an active cooler has to be used instead. The Raspberry Pi 500 does not have a fan header, but you can use GPIO and a python script to control the fan.
