################################################################################
# Automatically-generated file. Do not edit!
################################################################################

-include ../makefile.init

RM := rm -rf

# All of the sources participating in the build are defined here
-include sources.mk
-include Drivers/STM32F1xx_HAL_Driver/Src/subdir.mk
-include Core/Startup/subdir.mk
-include Core/Src/subdir.mk
-include subdir.mk
-include objects.mk

ifneq ($(MAKECMDGOALS),clean)
ifneq ($(strip $(C_DEPS)),)
-include $(C_DEPS)
endif
endif

-include ../makefile.defs

# Add inputs and outputs from these tool invocations to the build variables 
EXECUTABLES += \
Receptor\ NRF.elf \

SIZE_OUTPUT += \
default.size.stdout \

OBJDUMP_LIST += \
Receptor\ NRF.list \

OBJCOPY_BIN += \
Receptor\ NRF.bin \


# All Target
all: Receptor\ NRF.elf secondary-outputs

# Tool invocations
Receptor\ NRF.elf: $(OBJS) $(USER_OBJS) C:\Users\cesar\STM32CubeIDE\workspace_1.2.0\Projeto-stm32\Receptor\ NRF\STM32F103C8TX_FLASH.ld
	arm-none-eabi-gcc -o "Receptor NRF.elf" @"objects.list" $(USER_OBJS) $(LIBS) -mcpu=cortex-m3 -T"C:\Users\cesar\STM32CubeIDE\workspace_1.2.0\Projeto-stm32\Receptor NRF\STM32F103C8TX_FLASH.ld" --specs=nosys.specs -Wl,-Map="Receptor NRF.map" -Wl,--gc-sections -static --specs=nano.specs -mfloat-abi=soft -mthumb -Wl,--start-group -lc -lm -Wl,--end-group
	@echo 'Finished building target: $@'
	@echo ' '

default.size.stdout: $(EXECUTABLES)
	arm-none-eabi-size  $(EXECUTABLES)
	@echo 'Finished building: $@'
	@echo ' '

Receptor\ NRF.list: $(EXECUTABLES)
	arm-none-eabi-objdump -h -S $(EXECUTABLES) > "Receptor NRF.list"
	@echo 'Finished building: $@'
	@echo ' '

Receptor\ NRF.bin: $(EXECUTABLES)
	arm-none-eabi-objcopy  -O binary $(EXECUTABLES) "Receptor NRF.bin"
	@echo 'Finished building: $@'
	@echo ' '

# Other Targets
clean:
	-$(RM) *
	-@echo ' '

secondary-outputs: $(SIZE_OUTPUT) $(OBJDUMP_LIST) $(OBJCOPY_BIN)

.PHONY: all clean dependents
.SECONDARY:

-include ../makefile.targets
