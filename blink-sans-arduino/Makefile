TARGET       = blink
MCU          = atmega328p
F_CPU        = 16000000
ARDUINO_PORT = /dev/ttyACM0
AVRDUDE_ARD_BAUDRATE = 115200

CC=avr-gcc
CFLAGS=-Os -DF_CPU=$(F_CPU)UL -mmcu=$(MCU)

top: $(TARGET).hex


%.elf: %.o
	$(CC) -o $@ $^

%.hex: %.elf
	avr-objcopy -O ihex -R .eeprom $^ $@

clean:
	rm -f $(TARGET) *.o *.elf *.hex

upload: $(TARGET).hex
	avrdude -F -V -c arduino \
	-p ATMEGA328P -P $(ARDUINO_PORT) -b $(AVRDUDE_ARD_BAUDRATE) \
	-U flash:w:$(TARGET).hex
