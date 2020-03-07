Command Line:
/x/tools/ide/arduino-1.8.10/hardware/tools/avr/bin/avrdude -C/x/tools/ide/arduino-1.8.10/hardware/tools/avr/etc/avrdude.conf -v -patmega1284p -cstk500v1 -P/dev/ttyACM0 -b19200 -e -Ulock:w:0x3F:m -Uefuse:w:0xFD:m -Uhfuse:w:0xDE:m -Ulfuse:w:0xD6:m 
/x/tools/ide/arduino-1.8.10/hardware/tools/avr/bin/avrdude -C/x/tools/ide/arduino-1.8.10/hardware/tools/avr/etc/avrdude.conf -v -patmega1284p -cstk500v1 -P/dev/ttyACM0 -b19200 -Uflash:w:/home/thr/Arduino/hardware/anet/avr/bootloaders/atmega/optiboot_atmega1284p.hex:i -Ulock:w:0x0F:m 
