
# Activation and Deactivation of LED

Input GPIO PIN : PA0 (Connected to B1 user Button)

Output GPIO PIN : PC6

GPIO Mode : External interrupt mode with falling edge trigger detection

File containing all interrupt service routine : stm32f00xx_it.c

Function used : void HAL_GPIO_EXTI_Callback 

My code is present in location : 

'LED With Interrupt/EXTI_2on_3off/Core/Src/gpio.c'

Code : 

/* USER CODE BEGIN 2 */

void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)
{

	if(GPIO_Pin == B1_Pin)
	{
		static bool prev_val;
		if(prev_val == false )
		{
			HAL_GPIO_WritePin(GPIOC, GPIO_PIN_6, SET);
			prev_val = true;
		}
		else
		{
			HAL_GPIO_WritePin(GPIOC, GPIO_PIN_6, RESET);
			prev_val = false;
		}
	}

}

/* USER CODE END 2 */

Explanation : 







## Logic

The function checks if the interrupt was triggered by the B1 button connected to GPIO pin PA0 by comparing the GPIO_Pin parameter to the B1_Pin .

If the button was pressed (i.e., the interrupt was triggered), the program toggles the state of LED GPIO pin PC6 by using prev_val to keep track of the previous state of the LED.

If prev_val is false (i.e., the LED is currently off), the program sets the LED state to ON. 

It then sets prev_val to true to indicate that the LED is now on.

If prev_val is true (i.e., the LED is currently on), the program sets the LED state to off. 

It then sets prev_val to false to indicate that the LED is now off.