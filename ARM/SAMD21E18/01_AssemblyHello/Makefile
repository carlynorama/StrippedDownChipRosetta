###############################################################################
# Makefile for a simple SAMD21 Assembly project
###############################################################################

## General Flags
TARGET ?= hello#set if not defined 
LINKER_FILE ?= $(TARGET).ld
MACH = cortex-m0

TOOL_BASE = arm-none-eabi-
CC = $(TOOL_BASE)gcc

## Options common to compile, link and assembly rules
COMMON = -mcpu=$(MACH)
COMMON += -mthumb

## Compile options common for all C compilation units.
CFLAGS = $(COMMON)
CFLAGS += -Wall
CFLAGS += -g
CFLAGS += -Os


## Linker flags
LDFLAGS = $(COMMON)
LDFLAGS += --specs=nosys.specs -nostdlib -lgcc

## Objects that must be built in order to link
OBJECTS = $(TARGET).o 

## Objects explicitly added by the user
LINKONLYOBJECTS = 

# Programming support using avrdude. Settings and variables.
PROGRAMMER = openocd
PROGRAMMER_FLAGS = -f program_and_serve.cfg

## Build
all: $(TARGET).elf

## Compile
%.o : %.S
	$(CC) -x assembler-with-cpp -c $(CFLAGS) $<

##Link
%.elf: $(OBJECTS)
	 $(CC) $(LDFLAGS) $(OBJECTS) $(LINKONLYOBJECTS)  -T./$(LINKER_FILE) -o $(TARGET).elf


# Program the device. 
#.PHONY: program 
program: $(TARGET).elf
	$(PROGRAMMER) $(PROGRAMMER_FLAGS)

# Print the disassembly. 
#.PHONY: disamb
disamb: $(TARGET).elf
	arm-none-eabi-objdump --disassemble $<

## Clean target
#.PHONY: clean
clean:
	-rm -rf $(OBJECTS) $(TARGET).elf $(TARGET).hex $(TARGET).lss $(TARGET).map 

