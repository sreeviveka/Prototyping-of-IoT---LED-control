
# EXP NO: 1 - LED CONTROL USING ARDUINO #
## Name: V.S SREE VIVEKA ##
## Reg. no: 2305001031
# Aim #
To design and implement an LED control system using an Arduino microcontroller and a push button, and to verify its operation through simulation using Proteus.

# Components Required #
Arduino Uno
Led
Resistance 10K ohms, 220 ohms
Push button
Bread board
Jumber wire

# Procedure: #
1. Open Proteus Design Suite and create a new project.
2. Click Pick Devices (P) and add the following components:
   * Arduino UNO
   * Push Button
   * LED (Red)
   * Resistor (220 Ω for LED)
   * Resistor (10 kΩ for pull-down/pull-up, if required)
   * Ground (GND) and Power (VCC)
3. Place all the components on the workspace.
4. Connect the components as follows:
   * Connect the LED anode to Arduino Digital Pin through a 220 Ω resistor.
   * Connect the LED cathode to GND.
   * Connect one terminal of the push button to Arduino Digital Pin.
   * Connect the other terminal of the push button to +5 V.
   * Connect a 10 kΩ resistor between input Pin and GND (pull-down resistor).
5. Save the circuit.
6. Open the Arduino IDE and write the program to read the push button state and control the LED.
7. Verify and compile the program.
8. Upload the program to the Arduino board and generate the HEX file by selecting Sketch → Export Compiled Binary.
9. Return to Proteus and double-click the Arduino UNO.
10. Browse and load the generated HEX file into the Program File field.
11. Click the Run (Play) button to start the simulation.
12. Press and release the push button during the simulation.
13. Observe the LED behavior:
    * **Button Pressed:** LED turns **ON**.
    * **Button Released:** LED turns **OFF**.
14. Verify that the LED responds correctly to every button press and record the simulation results.

## Theory ##

An **Arduino UNO** is a microcontroller development board based on the **ATmega328P** microcontroller. It provides digital input/output pins that can be programmed to interface with external devices such as sensors, switches, and LEDs. In this experiment, a **push button** is used as a digital input device, while an **LED** serves as a digital output device.

<img width="1327" height="887" alt="image" src="https://github.com/user-attachments/assets/635af591-11ba-424c-abd3-09cc75cbd1ea" />

A **push button** is a momentary switch that changes its state when pressed. The Arduino continuously reads the logic level of the input pin connected to the push button. Depending on the button state, the microcontroller executes the corresponding instruction to control the LED.


An **LED (Light Emitting Diode)** emits light when sufficient current flows through it in the forward direction. A **220 Ω current-limiting resistor** is connected in series with the LED to protect it from excessive current. A **10 kΩ pull-down resistor** is connected to the push button input to ensure that the input pin remains at a stable LOW state when the button is not pressed, thereby preventing false triggering. Alternatively, the Arduino's internal pull-up resistor can be used.

<img width="573" height="324" alt="image" src="https://github.com/user-attachments/assets/4f1a0f78-5365-4cb4-a258-db2be9bc4b9a" />

The Arduino program repeatedly executes the `loop()` function, where it reads the push button status using the `digitalRead()` function. If the button is pressed (HIGH), the Arduino sets the LED pin HIGH using the `digitalWrite()` function, causing the LED to glow. When the button is released (LOW), the LED is turned OFF.

Proteus Design Suite provides a virtual environment for simulating the Arduino circuit without physical hardware. The compiled Arduino program (HEX file) is loaded into the Arduino model in Proteus, allowing the circuit operation to be verified before hardware implementation. This simulation helps in identifying design and programming errors, reducing development time and cost.

## Working ##

1. When the simulation starts, the Arduino UNO initializes the input and output pins.
2. The push button is configured as a digital input, and the LED is configured as a digital output.
3. The Arduino continuously monitors the state of the push button inside the `loop()` function.
4. When the push button is **not pressed**, the input pin remains **LOW** (or HIGH when using the internal pull-up configuration), and the Arduino keeps the LED **OFF**.
5. When the push button is **pressed**, the input pin changes its logic state, which is detected by the Arduino.
6. The Arduino executes the corresponding instruction and sets the LED output pin to **HIGH**, causing the LED to **glow**.
7. When the push button is **released**, the input pin returns to its original state, and the Arduino turns the LED **OFF**.
8. This process repeats continuously, enabling real-time control of the LED using the push button.
9. The entire operation is verified through **Proteus simulation**, where the LED's ON/OFF behavior can be observed corresponding to the push button action.


<img width="838" height="377" alt="image" src="https://github.com/user-attachments/assets/65106004-3757-4906-8450-9e9fd7d4a551" />

## Applications ##
Interactive Light Display

Educational Game for Children

Home Automation

Security System Indicator

Emergency Signaling System

Weighing Machines



## Program  ##
```
#include "main.h"
void SystemClock_Config(void);
static void MX_GPIO_Init(void);
int main(void)
{
  HAL_Init();
  SystemClock_Config();
  MX_GPIO_Init();
  while (1)
  {
     HAL_GPIO_WritePin(GPIOA,GPIO_PIN_0,GPIO_PIN_SET);
	   HAL_Delay(4000);
	   HAL_GPIO_WritePin(GPIOA,GPIO_PIN_0,GPIO_PIN_RESET);
	   HAL_Delay(4000);
  }

}

void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};
  __HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE2);

  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_MSI;
  RCC_OscInitStruct.MSIState = RCC_MSI_ON;
  RCC_OscInitStruct.MSICalibrationValue = RCC_MSICALIBRATION_DEFAULT;
  RCC_OscInitStruct.MSIClockRange = RCC_MSIRANGE_6;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)
  {
    Error_Handler();
  }

  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK3|RCC_CLOCKTYPE_HCLK
                              |RCC_CLOCKTYPE_SYSCLK|RCC_CLOCKTYPE_PCLK1
                              |RCC_CLOCKTYPE_PCLK2;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_MSI;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;
  RCC_ClkInitStruct.AHBCLK3Divider = RCC_SYSCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0) != HAL_OK)
  {
    Error_Handler();
  }
}

static void MX_GPIO_Init(void)
{
  GPIO_InitTypeDef GPIO_InitStruct = {0};
  __HAL_RCC_GPIOA_CLK_ENABLE();

  HAL_GPIO_WritePin(GPIOA, GPIO_PIN_0, GPIO_PIN_RESET);

  GPIO_InitStruct.Pin = GPIO_PIN_0;
  GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

}

void Error_Handler(void)
{

  __disable_irq();
  while (1)
  {

  }

}

#ifdef  USE_FULL_ASSERT

void assert_failed(uint8_t *file, uint32_t line)
{

}
#endif 
```

## Output  ##
## LIGHT ON
<img width="899" height="1599" alt="WhatsApp Image 2026-08-14 at 9 34 48 AM" src="https://github.com/user-attachments/assets/17b5f10b-6d96-40a0-9c6f-b5eeb768a2c5" />

## LIGHT OFF
<img width="899" height="1599" alt="WhatsApp Image 2026-08-14 at 9 34 48 AM (1)" src="https://github.com/user-attachments/assets/22ed91c9-e2d5-4a6d-aae2-c25262f8cf7a" />

## Result ##
Designing and implementing an LED control system using an Arduino microcontroller and a push button, and to verify its operation through simulation using Proteus is executed and results are verified.

