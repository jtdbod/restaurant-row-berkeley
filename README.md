# restaurant-row-berkeley
Bonsai workflows and analysis scripts for running mice behavior in Restaurant Row

# Restaurant Row Instructions

### Updated 11/16/20

1.	The restaurant row files have been moved to D:\Restaurant Row Bonsai\restaurant-row-berkeley\
2.	Before getting mouse, turn on the Neurophotometrics controller. Turn the 470 nm and 560 nm LEDs on and set their power to 100. Slide the Play/Pause button UP so that you can see the blue+green light coming out of the fiber tip.
3.	Start by plugging in the power supplies for the servos (black with blue light, leftmost socket) and feather boards (the one with the 4 usb cables plugged into it.
4.	Then, plug in the transparent USB cables for the two DAQ Arduinos. They are color coded red and white.
5.	Open “test_servos.bonsai” workflow. Test to ensure all servers are working (open = keys 1-4, closed = keys q,w,e,r) and that the pellet dispensers are working (turn on dispensing by pressing keys a,s,d,f). Use tweezers to remove pellet and ensure a new one is dispensed and that bonsai is dispensing correctly.
6.	Open “5s-wait_60pct-rewareded.bonsai”. 
7.	At the bottom of the workflow, open the <Timestamps & Save Events> Node and then select the <Csvwriter> node.
8.	Update the filename to ”RR_Day###_epoch-#_ID-A2A###XX_FP-YH”, where epoch number =2 for the 1s wait 80% reward, XX=earmark, Y=L or R hemishere. Save to the “rr_data” folder. 
9.	If doing fiber photometry after the animal is fully trained, update the filename for in the “CsvWriter” and “Photometry Writer” nodes attached to “FP3001” node.
10.	Turn off the lights, turn on red lights. 
11.	Get mouse from colony and record their weight.
12.	Slide the Neuropho4tometrics Play/Pause slider DOWN to pause the LED output.
13.	Reduce the power setting on the Neurophotometrics controller to 0.6 for both channels.
14.	Press the MODE button until BSC2 is displayed on the screen.
15.	Test the fiber output by sliding the Play/Pause button UP. You should see alternating blue and green light. 
16.	Slide the Play/Pause button DOWN to pause the LED output and Neurophotometrics recording. 
17.	Place cage in RR and plug the fiber into the mouse. Place the mouse in the center of RR.
18.	Start the bonsai workflow. Ensure the feeders are in the correct position before starting the Bonsai workflow
19.	Activate each camera using VirtualDub. Be sure to click “Disconnect” afterwards.
20.	 Press “4” on the keyboard to begin recording.
21.	Bring the mouse from the center of RR and place them at the exit of R4 and facing R1.
22.	Once the mouse is running, slide the Play/Pause button UP on the Neurophotometrics controller to start FP recording.
23.	Run mouse for 1 hour
24.	When done, press STOP in the Bonsai workflow to stop recording. Slide the Play/Pause button DOWN on the Neurophotometrics controller.
25.	When done, remove mouse to home cage. Clean RR setup with acetic acid and water
26.	Supplement food ONLY if animal falls below 85%. For older mice, 85% should be taken from their lean weight or their average weight when fed 3g of pellets a day.
27.	When done for day, unplug LEDs, unplug Arduino USBs, unplug Feather board power supply, and unplug servo power supply. Turn off the LEDs and the Neurophoteometrics system.

# TROUBLESHOOTING

**Multiple pellets are dispensing**

The pellet hopper is loose. Remove the hopper and use air can and tweezers to remove all pellets. Replace the hopper with a slight twist motion and tape it secure.

**Pellet dispenser is jammed (making noise)**

The pellet hopper is on too tight. Try gently turning it counter clockwise. Ensure tape holds it in place if it starts to come loose.

**Bonsai counting single pellets as 100s of pellets**

Funny bug in Bonsai where the adalogger dispenser boards are stuck in a constant read mode at the read rate so you get `(read_rate)*(TTL_pulse_duration)` number of pellets being recorded. Solution is to reset Bonsai until the inputs behave again. After more tinkering, it looks like it might be a result of a faulty ground wire somewhere in the Feather board Arduino FIRMATA DAQ circuit. Touching the cables more moving things causes the TX light to change, suggesting a loose connection. When malfunctioning, the TX light remains on. When functioning normal, the TX only turns on briefly when there is some kind of activity.

**No pellet dispensing**

If it isn’t jammed, open “test_seros” workflow. When running, press “A,S,D,F” to activate dispense mode for each dispenser. If this still doesn’t work, you might have a fried stepper motor board. Double check all connections before replacing board. 

**Bonsai is not counting pellets**

Double check all the connections and try all above troubleshooting, including powering down/unplugging all boards, Bonsai, and computer. When running “test_servos” or any of the behavior workflows, the normal state of the green LED on the Adafruit datalogger boards should be rapid flashing green. When a pellet is removed from the dispenser, it should briefly turn red, dispense, then go back to fast blinking  green. Any other behavior suggests either 1) a connection has become undone, 2) friend Feather Adalogger board, 3) fried stepper motor board, 4) fried stepper motor that rotates the dispenser disk below the pellet hopper (NOTE: stepper motor is the motor that rotates the pellet dispensing disk below the hopper, NOT the servo controlling the external arm.)
	
	

