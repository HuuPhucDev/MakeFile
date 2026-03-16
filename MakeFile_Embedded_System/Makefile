GCC_DIR := C:/GNU_Toolchain/GCC_NEW
CC = $(GCC_DIR)/bin/arm-none-eabi-gcc
LD_FILE := Linker/stm_ls.ld
INC_DIR := Driver/GPIO/inc

##Include files
INC_DIRS += Driver/GPIO/inc Driver/UART/inc
INC_FILES += $(foreach INC_DIRS,$(INC_DIRS),$(wildcard $(INC_DIRS)/*))

##Source files
SRC_DIRS += Driver/GPIO/src
SRC_FILES += $(foreach SRC_DIRS,$(SRC_DIRS),$(wildcard $(SRC_DIRS)/*))

CC_INC = $(foreach INC_DIRS,$(INC_DIRS),-I$(INC_DIRS))

CHIP=cortex-m4

CCFLAGS= -c -mcpu=$(CHIP) -mthumb -std=gnu11 -O0 -I$(INC_DIR)
LDFLAGS= -nostdlib -T $(LD_FILE) -Wl,-Map=Output/GPIO.map

build : Output/GPIO.hex

Output/main.o : User/src/main.c
	$(CC) $(CCFLAGS) -o $@ $^

Output/GPIO.o : Driver/GPIO/src/GPIO.c
	$(CC) $(CCFLAGS) -o $@ $^

Output/stm32_startup.o : Startup/stm32_startup.c
	$(CC) $(CCFLAGS)  -o $@ $^

Output/GPIO.elf : Output/main.o Output/GPIO.o Output/stm32_startup.o
	$(CC) $(LDFLAGS) -o $@ $^

Output/GPIO.hex : Output/GPIO.elf
	$(GCC_DIR)/arm-none-eabi/bin/objcopy.exe -O ihex "$^" "$@"

run : 
	./Tool/ST-LINKUtility/ST-LINK_CLI.exe -ME
	./Tool/ST-LINKUtility/ST-LINK_CLI.exe -p "Output/GPIO.hex" 0x08000000
	./Tool/ST-LINKUtility/ST-LINK_CLI.exe -rst
 
clean : 
	rm -rf ./Output/*

print-%:
	@echo $($(subst print-,,$@))
