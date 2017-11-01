# USBaspV2-stuff
USBaspV2 stuff for full windows use

HW: https://de.aliexpress.com/item/USBasp-USBISP-3-3V-5V-AVR-Programmer-USB-ATMEGA8-L/2036883289.html
and https://de.aliexpress.com/item/USB-Nano-V3-0-ATmega328-16M-5V-Micro-controller-CH340G-board-For-Arduino/32647826505.html as arduino Programmer

complete tutorial:
http://www.rogerclark.net/updating-firmware-on-usbasp-bought-from-ebay/

My USBasp was a ATmega8A and works with ATmega8 firmware

short tutorial:

Prepare Arduino:
Program an Arduino as an ISP.
This is a fairly simple process.
Plug in your Arduino.
From the Examples (on the File menu). Select “Arduino ISP”
Select “Upload” and confirm that the new firmware has been uploaded.Note down the Com port that the Arduino board is connected via i.e from the Tools->Serial port menu

Prepare USBasp: 
disconnect USBasp form PC
set JP2 and set to 5V

Connect USBasp to Arduino:
Arduino    USBASP
5V ———– 2 (VCC)
GND ——– 10 (GND)
D13 ———— 7 (SCK)
D12  ———-  9 (MISO)
D11 ———-   1 (MOSI)
D10 ———    5 (RESET)


Check your config:
Check that avrdude can connect to the USBasp In the windows command window, type

COM3 is my COM port of the arduino
avrdude -c avrisp -P COM3 -b 19200 -p m8 -v

If everything is connected correctly you should see a load of information about the USBasp board that you are about to program, like this

Using Port                    : COM3
Using Programmer              : avrisp
Overriding Baud Rate          : 19200
AVR Part                      : ATMEGA8
Chip Erase delay              : 10000 us
PAGEL                         : PD7
BS2                           : PC2
RESET disposition             : dedicated
RETRY pulse                   : SCK
serial program mode           : yes
parallel program mode         : yes
Timeout                       : 200
StabDelay                     : 100
CmdexeDelay                   : 25
SyncLoops                     : 32
ByteDelay                     : 0
PollIndex                     : 3
PollValue                     : 0x53
Memory Detail                 :

Block Poll               Page                       Polled
Memory Type Mode Delay Size  Indx Paged  Size   Size #Pages MinW  MaxW   ReadBack
———– —- —– —– —- —— —— —- —— —– —– ———
eeprom         4    20   128    0 no        512    4      0  9000  9000 0xff 0xff
flash         33    10    64    0 yes      8192   64    128  4500  4500 0xff 0x00
lfuse          0     0     0    0 no          1    0      0  2000  2000 0x00 0x00
hfuse          0     0     0    0 no          1    0      0  2000  2000 0x00 0x00
lock           0     0     0    0 no          1    0      0  2000  2000 0x00 0x00
calibration    0     0     0    0 no          4    0      0     0     0 0x00 0x00
signature      0     0     0    0 no          3    0      0     0     0 0x00 0x00

Programmer Type : STK500
Description     : Atmel AVR ISP
Hardware Version: 2
Firmware Version: 1.18
Topcard         : Unknown
Vtarget         : 0.0 V
Varef           : 0.0 V
Oscillator      : Off
SCK period      : 0.1 us

avrdude: AVR device initialized and ready to accept instructions

BACKUP:
avrdude -c avrisp -P COM3 -b 19200 -p m8 -U flash:r:original_firmware.bin:r

FLASH:
avrdude -c avrisp -P COM3 -b 19200 -p m8 -U flash:w:usbasp.atmega8.2011-05-28.hex

FUSES:
avrdude -c avrisp -P COM3 -b 19200 -p m8 -B 200 -U hfuse:w:0xC9:m -U lfuse:w:0xEF:m
