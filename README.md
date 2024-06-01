![5v-Power-supply-change](/images/trs-80MotherboardKeyBoard3.jpg?raw=true "Header")
# Restore power from a failing power supply.

These are my notes I made for the choices for my restoration.

This is a slightly altered copy of TRS-80 Model 1 USB-A Power Mod (5V DC conversion) by _Tim Halloran_ 

### https://github.com/hallorant/bigmit/tree/master/model1usb 

Tim's document provides way more options and detail, these are my notes based on his work from his original doc.  
His path is great and is what I followed.  
This is not to take credit for any of his work, its just my path following his great doc.  
So, thanks Tim for your notes that I could follow.  
I'll be using a lot of his words and just altering them some as I log my work to get power working again on my model-1.

The changes required to switch to 5 volts are pretty simple, it but does require a trace cut and the removal of several components from the motherboard.  
Several wires are then soldered in place.  
Finally, a 5-pin DIN to USB-A cable is constructed.  
I run mine now on just a small USB power plug, the same as you use for a phone.  Seems handy and easy.  
The outside of the computer is unmodified and is indistinguishable from a stock Model 1.  
The power switch still works just as normal as does the reset button.  
For my change I replaced the 4116 memory with 4164 (64K used as 16K).  
This simplifies the modification and allows the entire computer to run off 5V DC power.  
I'll look after this at maybe to enabling all 64k of the mem. I saw an article on the change and Ill see if thats an option.

Other Helpful information found on:  
*  https://mattpilz.com/trs-80-model-1-repair-guide/
*  www.trs-80.org.uk   march 2023 edition of TRS-8-bit


 
## Here are the things I ordered before I started the change.
- [ ] Order from Jameco.com
* 2306439 210-7 SWITCH,DIP,SPST,7-POS,14-PIN,LOW PROFILE,SLIDE RAISED  SWITCH,DIP,SPST,7-POS ___________ 2 EA $0.3500 
  https://www.jameco.com/z/210-7-James-Electronics-Low-Profile-DIP-Switch-Slide-Raised-7-Position-SPST-14-Pin-DIP_2306439.html
* 41662 4164-150 IC,4164-150,DIP-16, DRAM,64KX1,150NS(MCM6665- 15/MB8264-15) 64KX1 DIP-16 DRA  ______ 10 EA $2.1900  
  https://www.jameco.com/z/4164-150-Major-Brands-IC-4164-150-DRAM-65-536-Bit-65-536x1-150ns-with-Page-Mode-DIP-16_41662.html

- [ ] Order from amazon
* https://www.amazon.com/gp/product/B09FF4RLQN/ref=ppx_yo_dt_b_asin_title_o08_s00?ie=UTF8&th=1 ______  USB cable
* https://www.amazon.com/gp/product/B09N1J8Z8N/ref=ppx_yo_dt_b_asin_title_o04_s01?ie=UTF8&psc=1 ______ 3-5-pin male and female din audio adaptor 
 


## Modifying the Model 1 computer  
Tim covers this in his doc providing some background and theory behind our changes  
What we want to do is bypass the power regulation circuits on the motherboard.  
The trick is to channel the power around the active power regulation circuits (that create the heat in a stock Model 1).  
Also we do not want to remove the big transistors.  
What we want is a clean path to the DC power out to the voltage  rails.

![5v-Power-supply-change](/images/image003.jpg)

Tims pencil marks give some insight into earlier attempts and can be ignored.  
The red-X's show where we will remove components and the green show the clear path out of the power regulation circuits to the motherboard logic.  
If we swap out the memory we can make a 5V only system.  
This removes the need for the DC-to-DC converter, however, there is snag.  
If you look at the memory chip pinouts for the 4164 (64K using 16K) in the diagram below, in both cases, we have to get 5V on the lines where previously there was 12V.  
We can safely ignore the -5V lines.

| Data Sheet | Old and New|
| ------------- | ------------- |
| ![5v-Power-supply-change](/images/image006.png)  | ![5v-Power-supply-change](/images/mem.jpg)   |

To get 5V where the stock computer had 12V is easy. Simply connect Z1 pin 3 to Z1 pin 12 (connected to Z2 pin 3).  
This will channel 5V over to the (old) 12V lines and make them 5V as well.  
#### To summarize
- [ ] Change all the memory chips (Z13 through Z20) from 4116's to 4164's
- [ ] Ignore the -5V path (bottom of the diagram above) it will not be used. 
- [ ] Connect 5V DC power into the 5V power grid (the left hand side of R4 as presented below). Bridge Z1 pin 3 to Z1 pin 12 (connected to Z2 pin 3) to change the 12V path to 5V. 
 
## Starting the power cable build and then the changes to the Model 1 motherboard.
### Building the power cable  

- [ ] Soldering the USB-A connector  


| My Cable | Model 1 power connector from the TRS-80 micro computer technical reference handbook| Pin Example| Diagram|
| ------------- | ------------- | ------------- | ------------- |
|<img src="https://github.com/kdcgarber/5v-Power-supply-change/blob/main/images/Powercable.jpg" width="400" height="280">  | ![5v-Power-supply-change](/images/image005.jpg)   | ![5v-Power-supply-change](/images/image006.jpg)  | ![5v-Power-supply-change](/images/image010.png)   |


 
Note: in the image above red is 5V and green is ground.  
A good reference I used to see the ports better is here:  
* http://cpmarchives.classiccmp.org/trs80/mirrors/kjsl/www.kjsl.com/trs80/mod1intern.html

I took one of the usb cables I purchased and remove the usb-c end.  
I stripped back the cable and tinned the wires to be attached to the 5-pin Male DIN Audio Connector I purchased also.  
Make sure you add the cable cover to the wire before you begin to attach the wires so that its there after the connection is made.  
After the wires were all attached I checked the connections with the continuity tester on your multimeter.   
Then closed up the connector end. 

### Now for the real work removing/altering things
When you take the existing components out do it carefully and save them.  
If you have to you can reverse the modification. Here is a picture of what this should look like when the parts are removed. 

<img src="https://github.com/kdcgarber/5v-Power-supply-change/blob/main/images/trs-80-motherboard.jpg" width="125%" height="125%">

- [ ] Remove the DRAM chips  
Start off by removing the socketed Z13-Z20 memory chips. Removing components  
- [ ] Remove two DIP chips: Z1 and Z2 
- [ ] Remove resistors: R4, R7, R8, R13, and R18  
- [ ] Remove capacitor C8 entirely.  
- [ ] Unsolder and disconnect only the + side of C9 (near the power switch).  
  

Setup the power switch  
Flip the computer over to the back and focus near the power connector and power switch.  
- [ ] We need to do a trace cut and solder a wire from pin 5 of the power connector to the right position on the switch. 

<img src="https://github.com/kdcgarber/5v-Power-supply-change/blob/main/images/image013.jpg" width="35%" height="35%">

Use the continuity tester on your multimeter to ensure this is all correct.  
- [ ] Check that the connection on pin 4 of the power connector is not shorted to the pin close to it. Also be sure your trace cut is not conducting. I used a Exacto knife to do the trace cut (just to be sure) but great care is required.  
The trace cut isolates the power switch lead we will use to connect power to the motherboard.  
- [ ] To do this turn the board around to show the chips. You need to position the positive lead of C9 to reach the third connection back on the left hand side of the power switch.  
Add a bit of shrink wrap to ensure the C9 lead doesn't connect with any other power switch terminals. 

<img src="https://github.com/kdcgarber/5v-Power-supply-change/blob/main/images/image014.jpg" width="35%" height="35%">

- [ ] We'll also insert a wire of about 4 inches that will connect to the motherboard.
      The picture below shows what this should look like prior to soldering.
      Trim and solder the wire connected to the power switch to the R4 hole closest to the power switch. 
 
<img src="https://github.com/kdcgarber/5v-Power-supply-change/blob/main/images/image015.jpg" width="35%" height="35%">

- [ ] Finally, we need to bridge the old 12V grid to the old 5V grid so everything is 5V DC.  
To do this, I then soldered a sockets into Z1 (and optionally Z2) and use a 7 switch DIP.  
This is shown in the image below. Be sure to turn off all the switches except 3 (which is on).  
  
<img src="https://github.com/kdcgarber/5v-Power-supply-change/blob/main/images/image016.jpg" width="35%" height="35%">

### ----  The modification is complete  --------------------------------- 
 
- [ ] Testing your modification and putting the memory back  
Ensure your power switch is off on the Model 1 computer. Hook up the power cable and connect it to a USB charger.  
For all this testing I suggest you use a clip to connect the negative lead of your multimeter to the side of C9 not connected to the power switch (as we do on a stock Model 1).  
- [ ] (TEST 1: Any Power?) Before powering this on check the pin on the power switch one up toward where you press the switch. This should read around 5V DC.  
- [ ] (TEST 2: Motherboard Grid Okay?) Power on the machine. Test that pin 8 of any of the DRAM sockets (any of Z13 through Z20) is 5V DC.    Pin 9 should be 5V DC.  
If any of these tests fails. Stop, something is wrong. Double-check the instructions and see if you shorted something with a solder connection.  
If these tests pass shut off the computer and disconnect the power cable.  
- [ ] Carefully insert your memory. On the bench connect the power cable, you monitor cable, and the keyboard. Turn on the monitor and then the computer. It should work as a Model 1 is expected to work.  
 
If your computer doesn't go, check voltages when the machine is turned on.  
Do they look okay?  Use the TRS-80 micro computer technical reference handbook to isolate the problem.  
Also, Refer to Tim's Doc.  Its what I used and created my notes from his two options.
 
### Backout if needed.  
You can reverse the modification (if you were careful with Z1 and Z2). Just socket Z1 and Z2, undo all the new stuff, and put all the old parts where they belong. Move the wire under the power switch to reconnect the trace cut. I've done this several times. The only real danger is that you destroyed Z1 and Z2 when you took them out. 

