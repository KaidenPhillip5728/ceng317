# Hardware report/Build instructions
Your target audience is a Computer Engineering Technology student from a different college who would like to recreate your project. Guidelines for next semester's CENG 355 Report are available.[^1]
[^1]: Technology Report Guidelines. OACETT, Revised September 2022. Available at: https://www.oacett.org/getmedia/5ad707d7-f472-4b24-a7fe-f34e270b0c41/2022_TR_Guidelines_-_Updated_Version_-_Sept_2022.pdf
## Table of Contents
[1.0 Introduction](#10-introduce-the-broadcom-development-platform-and-exisiting-functionality)   
[2.0 Body](#20-added-functionality)   
[2.1 Sensor/Effector purchase](#21-sensor-effector-purchase)   
[2.2 PCB design and soldering](#22-pcb-design-and-soldering)   
[2.3 Case design and assembly](#23-case-design-and-assembly)   
[2.4 Firmware development and use](#24-firmware-development-and-use)   
[3.0 Testing and Results](#30-testing-and-results)   
[4.0 References](#40-references)  

## 1.0 Introduce the Broadcom development platform and existing functionality   

The board is run on Raspberry Pi 4 using the Raspberry Pi operating system. The Raspberry Pi was purchased through Humber which included an LED senshat, with temperature, humidity, and pressure, sensors. However, the senshat is not needed for the RFID reader to work.   

## 2.0 Added functionality   

On top of the Raspberry Pi, I’ve added a PCB and soldered a qwiic connector to connect the RFID sensor. I've also soldered an LED, transistor and two resistors to test the functionality of the PCB before hooking up the sensors. The RFID sensor adds the ability to read 125kHz RFID cards. The SparkFun RFID Starter Kit comes with the board which connects to the pi, the RFID magnet, RFID cards for testing and a cable. You can buy them in the kit or purchase them separately. Depending on the frequency of the cards you will need to buy the corresponding magnet.

### 2.1 Sensor/Effector purchase   

I purchased the SparkFun RFID Starter Kit on sparkfund but it got lost in the mail so I got a refund and bought a new one. Everything purchased can be found on the bill of materials. [[BOM](https://github.com/PrototypeZone/hardware-project-KaidenPhillip5728/blob/main/hardware/bom.md)]

### 2.2 PCB design and soldering   

The PCB was designed in KiCad but was given to us as a template where we just needed to connect the traces ([link](https://github.com/PrototypeZone/ceng317/tree/main/hardware/pcb)). We were given the board with the qwiic connecter soldered for us but we had to solder the LED resistors and transistor. For me, the most difficult piece of solder was the transistor. Make sure to leave enough room to solder the transistor but low enough to fit the senshat.   

### 2.3 Case design and assembly   

The case was designed using Humber’s laser-cutting lab where the pdf was designed by the professor ([link](https://github.com/PrototypeZone/ceng317/tree/main/hardware/lasercutting)) but edited by us to include a mount for our sensor and modify the hole for our screws. I assembled the case using clear tape. I also mounted the board the board using 4 M2.5 X .4 screws, 4 16MM standoffs, and a stacking header(items found in the BOM). The senshat was reattached but on top of the PCB with its own screws, standoffs and stacking header.  

### 2.4 Firmware development and use   

The firmware was created based on the sparkfund hook-up guide. The code was pulled straight from the website’s zip folder. The code is supposed to get the number of the card when it is scanned; However, I couldn’t it get running on the Pi this semester because it could not pick up the i2c bus. [SparkFun Qwiic RFID-IDXXLA Hookup Guide - SparkFun Learn](https://learn.sparkfun.com/tutorials/sparkfun-qwiic-rfid-idxxla-hookup-guide)
 

## 3.0 Testing and Results   

Since we made the pcb from scratch we first tested the connection using a flashing LED. During the testing, the transistor was malfunctioning however with more solder it worked. Next, we connected our sensor and discovered the I2C with the pi’s i2cconnect command. I tried many different ways to test the i2c bus but they all came up blank. I hypothesize that the pi cannot read past i2c 0x77 where my device is past that range at 0x7D qwicc connected or 0x7C jumper (a wired connection). During the break, I will have to connect it to my Arduino UNO and reprogram the i2c range to an address readable to the pi. Lastly, if your pi can pick up the address you may need to cut the int trace on the sensor board or give it a 3.3-5v jumper.  

## 4.0 References   

Sparkfund hookup guide
[SparkFun Qwiic RFID-IDXXLA Hookup Guide - SparkFun Learn](https://learn.sparkfun.com/tutorials/sparkfun-qwiic-rfid-idxxla-hookup-guide)

Rfid Arduino GitHub
[https://github.com/sparkfun/SparkFun_Qwiic_RFID_Arduino_Library](https://github.com/PrototypeZone/hardware-project-KaidenPhillip5728/tree/main/hardware)https://github.com/PrototypeZone/hardware-project-KaidenPhillip5728/tree/main/hardware 
