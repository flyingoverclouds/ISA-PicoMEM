# ISA PicoMEM Firmware Repository

**How to read the Firmware name:**<br /> 

**PM_MonthDay_D0** : Firmware released the Day/Month at Base Address D0 (*)<br />
**PM_W_xxx_xxx**   : Firmware for the Pico W Only (For ne2000)

If you use an XTIDE or a Disk BIOS, Use the DO (D000) Picomem Firmware and place the XTIDE in C800.<br />
**New:** In the debug sub directory, you can find "Debug" versions firmwares.<br />

**WARNING:** One new firmware may add incompatibility, pease try the previous versions of the firmware.<br />
(*) The Base Addres is the BIOS ROM location in memory, it can be C80000h or D0000h.<br />

## How to update the Firmware ?

The firmware update is done like for any Pi Pico : 

Connect the Board with the MicroUSB to a PC/Laptop and press the BOOTSEL Button on the Pico at the same time:
- A Folder is the automatically opened on the PC, you need to copy the file to this “Virtual Disk”, 
  wait until the folder automatically closes and it is finished.<br />
**WARNING:** For the PicoMEM 1.1 ONLY (Corrected on the 1.11): 
- The PicoMEM must be plugged into a PC so that the programming work. 
  Power on the PC (The Retro one) and press the button at the same time.

## Firmwares Revision History : 

- + Added Wifi connection status detection and Display (BIOS Menu, Left Ctrl+Alt+F1)
    It can display if the wifi.txt file is missing, wrong SSID, Password, Signal strength...
- ! Fixed some Wifi connection problem with connection retry. (every 5s)
- + Configuration file (config.txt) support added : The BIOS Base Address can be changed in this file. 
    It can also force to start the Setup when the Optional ROM start (For Book8088 Support) can't be used in some systems (Like IBM5150)
- + RAM/ROM emulation speed increased : The PicoMEM now work on the Book8088 at 8MHz, with out of standard ISA (250 vs 500ns MEMR Timing)
    This speed increase will surely allow for more compatible system.
- + You can now plug an I2S DAC on the board and enjoy Adlib emulation. It is preliminary and need fix, but it is working quite well.
- ! Display bug in the image selection display
- ! Corrected the "Extention" Typo :P
- - Removed Boot HDD Number from the BIOS, will de obsolete.

### PM_W_Apr21_xx:
- **WARNING:** As Timing changes has been done, I would like as many feedback as possible, **Go to the previous firmware in case of problem.**
- + RAM/ROM Emulation is faster : Now Work on the Commodore PC10 and maybe more.<br />
    On one PC10, it needed to be put in 8 or 10MHz mode to work.
- + Added the Number of Floppy drive and Disk Drive display in the BIOS
- ! Changed the POST Code : PicoMEM BIOS Port is 81h, PC BIOS Still 80h

### PM_W_Apr14_xx:
- + Added USB Joystick suport (XBOX and PS4 Compatibles) Only one joystick for the moment, no driver needed. Need to be enabled in the BIOS
- + PMEMM EMS Driver is now available for 4Mb of EMS.
- ! Fixed the Boot on Sega Teradrive
- ! Small fix on the POST Code (Don't miss Code anymore)

### PM_W_Apr2_xx:
- + Added support of multi page Images selection : Up to 32 Images, 2 pages.
- + Added the Floppy image SWAP under DOS : **Press Left Ctrl+Shift+F2** to select another A: Floppy image.<br />
    This is working only in text mode.
- + Post Code values added in the BIOS Initialisation phase. (Visible only with the QwiiC external screen)
- + Changed the "PicoMEM Init" text : Display a . for every Init phase.
- ! Corrected a display bug : the image selection windows did not clear completely.

### PM_Apr2_D0:
- Not Wifi Version of the above firmware.

### PM_W_Mar11_xx:
- ! The Floppy disk bug was still present : Corrected and tested.

### PM_W_Mar10_xx:
- + The ne2000 IO Port can be changed and ne2000 can be disabled.
- ! It is now possible to BOOT DOS With RAM emulated with PSRAM.
- ! Disk Write supported with RAM Emulated from PSRAM.
- + Function to create new HDD Images added in the Disk BIOS Menu.
- ! Corrected a bug that made the Computer Floppy drive not usable.
- + The Computer configuration detection is now moved to the BootStrap Code :
-   > Should increase the compatibility with Memory and Disk Boards using ROM.
- These changes should allow the usager of DOS in High RAM (Emulated); Boot to DOS 6.22 With 736Kb of RAM ...

### PM_W_Feb11_C8_Test (and D0):
- Added the POST Code function : Port 80h code will be displayed if a 4 Digit Qwiic display is connected :
<br /> https://www.sparkfun.com/products/16916
- Some internal optimisation  

### PM_W_Jan21_xx:

- Version only for the Pico W Boards
- + Added support for PM2000 (NE2000 PicoMEM Version detecting I/O and Port  

### PM_W_Jan21_C8_Test (and D0): 
Merge of the latest BIOS and ISA Code.
This Firmware work only with a Pico W Board, use the PM_Dec28 Otherwise

ne2000 emulation via Wifi presend, but "for test only" :
- Create a wifi.txt file with the SSID in the first line and the Password in the 2nd line
- use ne2000.com 8Bit (command line : ne2000 0x60 0x3 0x300)
- The PicoMEM can't tell if the connection fail and does not try to re connect.
- The Wifi Access point need to be relatively close to increase the chance of connection success. 
The IRQ Can be changed in the BIOS Menu (Default is IRQ 3)

Other changes :
- Memory read Access speed increased
- Added Boot HDD Number selection in the BIOS (Not Active)

### PM_Dec28: 5150 Support is Back
- ! Corrected the 5150 Support, If someone can test it more to be sure….
- + Added BIOS Menu option to select uSD and PSRAM Speed, but not implemented in the Pico
- + Speed of I/O and Memory access increased globally, so may be worth trying on other machines

### PM_Nov26: 
- + Modified the uSD Code. This now use the native and unmodified FasFS SPI Code.
    Faster and compatible with much more uSD. uSD Clocked at 24MHz.

### PM_Nov11: WARNING : Does not work anymore on 5150, Use the Oct 13 code for it.
- + USB Mouse added
- ! Floppy disk B: Working

### PM_Oct13: WARNING : Not reliable on 5150
- Other BIOS Display corrected (5150, Other) Settings always On, Segment number.
- Start always during the BOOT Menu
- Disk Drive B: not working (Correction in progress)

### PM_Sept26: Last version Ok for 5150
- ! Correct (Again) a new bug from previous version : Floppy image selection
- Remove the IRQ Stop during Int13h if PSRAM is not used to emulate memory : 
   The Disktest result will be more “Correct” (No Timer IRQ Missed)

### PM_Sept25:
- ! Corrected a bug in the image selection (Added by previous version)
- ! Corrected a Display bug with some 5150 BIOS Version

### PM_Sept23:
- + Added EMS emulation display at boot time
- + Add Video RAM Segment exclusion from the emulation
