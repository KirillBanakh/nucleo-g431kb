cmake_minimum_required(VERSION 3.20)

set(CMAKE_TOOLCHAIN_FILE ${CMAKE_CURRENT_LIST_DIR}/gcc-toolchain.cmake)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED TRUE)
set(CMAKE_C_EXTENSIONS ON)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)
set(CMAKE_CXX_EXTENSIONS ON)

project(nucleo-g431kb)

enable_language(ASM C CXX)

set(CORE_FILES
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/Device/Source/system_stm32g4xx.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/Device/startup_stm32g431xx.s)

set(APPLICATION_FILES
    ${CMAKE_CURRENT_LIST_DIR}/Project/Core/main.c)

set(STM32_HAL_LL_G4
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_adc_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_adc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_comp.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_cordic.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_cortex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_crc_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_crc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_cryp_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_cryp.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_dac_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_dac.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_dma_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_dma.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_exti.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_fdcan.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_flash_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_flash_ramfunc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_flash.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_fmac.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_gpio.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_hrtim.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_i2c_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_i2c.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_i2s.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_irda.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_iwdg.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_lptim.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_nand.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_nor.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_opamp_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_opamp.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_pcd_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_pcd.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_pwr_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_pwr.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_qspi.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_rcc_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_rcc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_rng.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_rtc_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_rtc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_sai_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_sai.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_smartcard_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_smartcard.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_smbus_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_smbus.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_spi_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_spi.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_sram.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_tim_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_tim.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_uart_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_uart.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_usart_ex.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_usart.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal_wwdg.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_hal.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_adc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_comp.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_cordic.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_crc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_crs.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_dac.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_dma.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_exti.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_fmac.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_fmc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_gpio.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_hrtim.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_i2c.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_lptim.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_lpuart.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_opamp.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_pwr.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_rcc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_rng.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_rtc.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_spi.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_tim.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_ucpd.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_usart.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_usb.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Src/stm32g4xx_ll_utils.c

    ${CMAKE_CURRENT_LIST_DIR}/Project/Core/HAL/stm32g4xx_hal_msp.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Core/HAL/stm32g4xx_hal_timebase_tim.c)

set(AZURE_RTOS_FILES
    ${CMAKE_CURRENT_LIST_DIR}/Project/Core/AzureRTOS/cortexm4_vectors.S
    ${CMAKE_CURRENT_LIST_DIR}/Project/Core/AzureRTOS/tx_initialize_low_level.S
)



set(EXECUTABLE ${PROJECT_NAME}.elf)

add_executable(${EXECUTABLE} ${APPLICATION_FILES} ${CORE_FILES} ${STM32_HAL_LL_G4} ${AZURE_RTOS_FILES})

include(${CMAKE_CURRENT_LIST_DIR}/Project/AzureRTOS/threadx/common/CMakeLists.txt)
include(${CMAKE_CURRENT_LIST_DIR}/Project/AzureRTOS/threadx/ports/cortex_m4/gnu/CMakeLists.txt)

target_compile_definitions(${EXECUTABLE} PRIVATE
    -DSTM32F431xx
    )

target_include_directories(${EXECUTABLE} PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/Project/Core
    ${CMAKE_CURRENT_LIST_DIR}/Project/Core/HAL
    ${CMAKE_CURRENT_LIST_DIR}/Project/Core/AzureRTOS
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/CMSIS
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/Device/Include
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Inc
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/stm32g4xx_hal_driver/Legacy
    ${CMAKE_CURRENT_LIST_DIR}/Project/AzureRTOS/threadx/common/inc
    ${CMAKE_CURRENT_LIST_DIR}/Project/AzureRTOS/threadx/ports/cortex_m4/gnu/inc
    )

target_compile_options(${EXECUTABLE} PRIVATE
    -mcpu=cortex-m4
    -mthumb
    -mfpu=fpv4-sp-d16
    -mfloat-abi=hard
    -fmessage-length=0
    -fdata-sections
    -ffunction-sections
    -ffreestanding
    -specs=nosys.specs
    -specs=nano.specs
    -Wall
    $<$<CONFIG:Debug>:-Og>
    )

target_link_options(${EXECUTABLE} PRIVATE
    "SHELL: -T ${CMAKE_SOURCE_DIR}/Project/Drivers/Device/stm32g431kbt6_flash.ld"
    "SHELL: -T ${CMAKE_SOURCE_DIR}/Project/Core/AzureRTOS/sample_threadx.ld"
    -mcpu=cortex-m4
    -mthumb
    -mfpu=fpv4-sp-d16
    -mfloat-abi=hard
    -specs=nano.specs
    -specs=nosys.specs ${CMAKE_SOURCE_DIR}/Project/Drivers/Device/Source/syscalls.c
    -lc
    -lm
    -lnosys
    -Wl,-Map=${PROJECT_NAME}.map,--cref
    -Wl,--gc-sections
    )

add_custom_command(TARGET ${EXECUTABLE} POST_BUILD
    COMMAND arm-none-eabi-objcopy -O ihex ${EXECUTABLE} ${PROJECT_NAME}.hex
    COMMAND arm-none-eabi-objcopy -O binary ${EXECUTABLE} ${PROJECT_NAME}.bin)

add_custom_command(TARGET ${EXECUTABLE} POST_BUILD
    COMMAND arm-none-eabi-size ${EXECUTABLE} -G)