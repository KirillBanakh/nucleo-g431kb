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
    ${CMAKE_CURRENT_LIST_DIR}/Project/Core/main.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/Device/Source/system_stm32g4xx.c
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/Device/startup_stm32g431xx.s)

set(EXECUTABLE ${PROJECT_NAME}.elf)

add_executable(${EXECUTABLE} ${CORE_FILES})

target_compile_definitions(${EXECUTABLE} PRIVATE
    -DSTM32F431xx
)

target_include_directories(${EXECUTABLE} PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/CMSIS
    ${CMAKE_CURRENT_LIST_DIR}/Project/Drivers/Device/Include
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
    -T${CMAKE_SOURCE_DIR}/Project/Drivers/Device/stm32g431kbt6_flash.ld
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