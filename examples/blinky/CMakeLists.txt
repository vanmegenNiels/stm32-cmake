cmake_minimum_required(VERSION 3.13)
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_CURRENT_SOURCE_DIR}/../../cmake/stm32_gcc.cmake)

project(stm32-blinky C ASM)
set(CMAKE_INCLUDE_CURRENT_DIR TRUE)

find_package(CMSIS COMPONENTS STM32L0 STM32F1 STM32F4 REQUIRED)
find_package(HAL COMPONENTS STM32L0 STM32F1 STM32F4 RCC GPIO CORTEX REQUIRED)
# Find all drivers:
#find_package(HAL COMPONENTS STM32L0 STM32F1 STM32F4 REQUIRED)
# Find drivers for all families:
#find_package(HAL COMPONENTS RCC GPIO CORTEX REQUIRED)
# Find LL driver:
#find_package(HAL COMPONENTS LL_GPIO REQUIRED)
# Find everything:
#find_package(HAL REQUIRED)

# STM32F4-Discovery
add_executable(stm32-blinky-f4 blinky.c stm32f4xx_hal_conf.h)
target_link_libraries(stm32-blinky-f4 
    HAL::STM32::F4::RCC
    HAL::STM32::F4::GPIO
    HAL::STM32::F4::CORTEX
    CMSIS::STM32::F407VG
    STM32::NoSys 
)

# STM32VL-Discovery
add_executable(stm32-blinky-f1 blinky.c stm32f1xx_hal_conf.h)
target_link_libraries(stm32-blinky-f1 
    HAL::STM32::F1::RCC
    HAL::STM32::F1::GPIO
    HAL::STM32::F1::CORTEX
    CMSIS::STM32::F100RB
    STM32::NoSys
)

# STM32L0538-Discovery
add_executable(stm32-blinky-l0 blinky.c stm32l0xx_hal_conf.h)
target_link_libraries(stm32-blinky-l0
    HAL::STM32::L0::RCC
    HAL::STM32::L0::GPIO
    HAL::STM32::L0::CORTEX
    CMSIS::STM32::L053C8
    STM32::NoSys
)
