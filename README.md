# Obboto-WLED-Mod
A guide on installing WLED to the Obboto Sphere.

This guide shows how to install WLED and a correct LEDmap to the obboto sphere.
Pay close attention to the written instructions and supplied photos.


Disclaimer !
This mod REQUIRES soldering to the main PCB and flashing new firmware to the ESP32 microcontroller located on the board.
This mod also requires additional hardware to flash the ESP32 microcontroller as this is for now not possible through the SD card slot.
Please Backup the factory firmware beforehand as listed in this guide.
Continue at your own risk.

Requirements:
Obboto Sphere
Basic Tools
Soldering Iron + supplies
Breadboard Pins 2.54mm / 0.1"
Breadboard Wires female-female
ESPprog flashing board: (https://docs.espressif.com/projects/esp-iot-solution/en/latest/hw-reference/ESP-Prog_guide.html)
ESP32Tool software: (https://github.com/Jason2866/esp32tool)


Step 1 Dissassembly

To access the main PCB we have to dissassemble our Obboto,
To open the device locate the 4 rubber feet on the bottom of the device and remove them carefully, if done right the glue should stick to the feet so these can be used again after reassembly.

(Insert pic 1)

Now remove the 4 screws located under the rubber feet.

You should now be able to twist the base to remove it, after the base is twisted it should easily lift off.
Be carefull there are wires connected to the base.

(Insert Pic 2)

Disconnect the following connectors from the main PCB
POWER
PIR 1
PIR 2
LOGO
SPEAKER
MIC
and the wifi antenna

You should now be able to remove the base entirely from the sphere.

Disconnect the remaining connectors from the PCB and loosen the 4 silver screws holding the PCB in place.

Now remove the PCB form the sphere, this can be a bit finnicky because of the many wires.

You should now have access to the entire PCB.

(Insert Pic 3)

Step 2 Soldering the Debug Header

Locate the Debug header holes on the PCB

Solder 6 of the breadboard pins to the empty DEBUG header facing up as shown in the following picture.

(Insert Pic 4)

Step 3 Connecting using ESPprog and Making a backup.

Now connect 6 breadboard wires from the Program header of the ESP Prog to the Debug Header.

<img width="522" height="448" alt="image" src="https://github.com/user-attachments/assets/ef5af40e-ab78-4053-a702-1441a38c0b91" />


| ESP-Prog | Obboto Debug |
| -------: | -----------: |
|        1 |            4 |
|        2 |            6 |
|        3 |            3 |
|        4 |            1 |
|        5 |            2 |
|        6 |            5 |


Connect the ESPprog to the computer and open the ESP32Tool software.

Connect the correct COM port (only one should give a successfull connection.

After connection the following should be visible

<img width="1380" height="886" alt="image" src="https://github.com/user-attachments/assets/04b85a9d-2a7e-4a5b-8383-f524d3f750b4" />

The esp has a flash size of 8mb so make sure the size is set to 0x800000

Now click read flash to backup your obboto
Note: This process can take up to 10 minutes, be patient, a green light should flash occasionally on the ESPprog.

Save the bin File in a safe location, this is the entire backup of your specific obboto, if you ever want to go back to the original firmware just connect the board to the software again and select the file to flash it again.

Step 4 Installing WLED

Keep the board connected to the PC and go to https://install.wled.me/

Click install and select the same COM port as used in the ESPtool software.

Click install WLED.

Step 5 Reassembly

Disconnect the ESPprog and remove the Breadboard wires, keep the header installed on the board it doesnt need to be removed.

Reconnect the internal connectors and install the PCB in the sphere.

Reconnect the connectors fron the base. 

You should now be able to power on the Obboto and you should see a few leds light up orange.

Now connect to the WLED wifi AP and setup your home wifi on the obboto.

Step 6 Configuring WLED

We now have WLED installed and running on our obboto.

first we need to limit the brightness of the LEDS to make sure we dont overdrive the supply

Go to:
settings - LED & Hardware - and set the global brightness factor to 20% (can be higher but from my experience this is fine)

Configure the LED outputs as follows

1 Start 0 Length 700 GPIO 15
2 Start 700 Length 700 GPIO 16
3 Start 1400 Length 715 GPIO 17
4 Start 2115 Length 801 GPIO 18
5 Start 2916 Length 6 GPIO 2

The first 4 segments are the LED Panels and the last segments are the Logo LEDS

save this config and your obboto should now light up entvirely in orange.

Now we have to upload the correct LEDMAP file, this file tells WLED how to map all the LEDS in a 2D Matrix to correctly display matrix effects.

Download the LEDmap file from the Releases of this Repo.

In your browser go to "ipofyourobboto/edit" to access the file manager

Click upload file and upload the ledmap.json 

Now restart your obboto.

Your obboto should power up fully orange like before.

Now select one of the 2D matrix effects like "Ballpit" and you should see all the LEDs mapped correctly displaying the effect like in my original post

Now just close up the Obboto and reinstall the rubber feet and the WLED converion is completed.












