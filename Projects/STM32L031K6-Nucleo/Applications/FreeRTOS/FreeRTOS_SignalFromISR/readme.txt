/**
  @page FreeRTOS_SignalFromISR FreeRTOS Signal from ISR example
 
  @verbatim
  ******************** (C) COPYRIGHT 2016 STMicroelectronics *******************
  * @file    FreeRTOS/FreeRTOS_SignalFromISR/readme.txt
  * @author  MCD Application Team
  * @version V1.7.0
  * @date    31-May-2016
  * @brief   Description of the FreeRTOS Signal from ISR example.
  ******************************************************************************
  *
  * Licensed under MCD-ST Liberty SW License Agreement V2, (the "License");
  * You may not use this file except in compliance with the License.
  * You may obtain a copy of the License at:
  *
  *        http://www.st.com/software_license_agreement_liberty_v2
  *
  * Unless required by applicable law or agreed to in writing, software 
  * distributed under the License is distributed on an "AS IS" BASIS, 
  * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  * See the License for the specific language governing permissions and
  * limitations under the License.
  *
  ******************************************************************************
  @endverbatim

@par Application Description

This application shows how to use thread signalling from an interrupt using CMSIS RTOS API.

This example creates a threads that calls osSignalWait to wait for a signal to set bit1 and bit2 then toggles LED3.

SysTick_Handler calls the function "Toggle_Leds" 
Toggle_Leds calls osSignalSet to send a signal = bit1 to Thread2 if a static counter is > 400 and < 1000
and calls osSignalSet to send a signal = bit1 | bit2 to Thread2 if a static counter is >= 1000
  
As a result, the behaviour is as follows:
LED3 toggle every 1000ms  


@note Care must be taken when using HAL_Delay(), this function provides accurate delay (in milliseconds)
      based on variable incremented in SysTick ISR. This implies that if HAL_Delay() is called from
      a peripheral ISR process, then the SysTick interrupt must have higher priority (numerically lower)
      than the peripheral interrupt. Otherwise the caller ISR process will be blocked.
      To change the SysTick interrupt priority you have to use HAL_NVIC_SetPriority() function.
      
@note The application need to ensure that the SysTick time base is always set to 1 millisecond
      to have correct HAL operation.

@note The FreeRTOS heap size configTOTAL_HEAP_SIZE defined in FreeRTOSConfig.h is set according 
      to the OS resources memory requirements of the application with +10% margin and rounded to 
	  the upper Kbyte boundary.

For more details about FreeRTOS implementation on STM32Cube, please refer to UM1722 "Developing Applications 
on STM32Cube with RTOS".


@par Directory contents
    - FreeRTOS/FreeRTOS_SignalFromISR/Src/main.c                Main program
    - FreeRTOS/FreeRTOS_SignalFromISR/Src/stm32l0xx_it.c        Interrupt handlers
    - FreeRTOS/FreeRTOS_SignalFromISR/Src/system_stm32l0xx.c    STM32L0xx system clock configuration file
    - FreeRTOS/FreeRTOS_SignalFromISR/Inc/main.h                Main program header file
    - FreeRTOS/FreeRTOS_SignalFromISR/Inc/stm32l0xx_hal_conf.h  HAL Library Configuration file
    - FreeRTOS/FreeRTOS_SignalFromISR/Inc/stm32l0xx_it.h        Interrupt handlers header file
    - FreeRTOS/FreeRTOS_SignalFromISR/Inc/FreeRTOSConfig.h      FreeRTOS Configuration file


@par Hardware and Software environment

  - This example runs on STM32L031xx devices.
    
  - This example has been tested with STM32L031-Nucleo board and can be
    easily tailored to any other supported device and development board.
    

@par How to use it ?

In order to make the program work, you must do the following :
 - Open your preferred toolchain 
 - Rebuild all files and load your image into target memory
 - Run the example
  
 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
