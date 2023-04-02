
# Button-controlled LED activation 

If the user presses the button twice, the LED is activated. If the user presses the button three times, the LED is deactivated.

Input GPIO PIN : PA0 (Connected to B1 user Button)

Output GPIO PIN : PC6

GPIO Mode : External interrupt mode with falling edge trigger detection

File containing all interrupt service routine : stm32f00xx_it.c

Function used : void HAL_GPIO_EXTI_Callback 

My code is present in location : 

    'LED With Interrupt/EXTI_2on_3off/Core/Src/gpio.c'

Code : 
    /* USER CODE BEGIN 2 */

    static uint8_t press_count = 0;

    static GPIO_PinState last_button_state = GPIO_PIN_RESET;

    static GPIO_PinState led_state = GPIO_PIN_RESET;

    void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)

    {
	
    if(GPIO_Pin == B1_Pin)
    {
        press_count++;

        if(led_state == GPIO_PIN_RESET && press_count == 2)
        {
            led_state = GPIO_PIN_SET;
            HAL_GPIO_WritePin(GPIOC, GPIO_PIN_6, led_state);
            press_count = 0;
        }
        else if(led_state == GPIO_PIN_SET && press_count == 3)
        {
            led_state = GPIO_PIN_RESET;
            HAL_GPIO_WritePin(GPIOC, GPIO_PIN_6, led_state);
            press_count = 0;
        }

        last_button_state = HAL_GPIO_ReadPin(B1_GPIO_Port, B1_Pin);
    }
    }



    /* USER CODE END 2 */








## Logic

I first declared 3 variables : 

    press_count : is used to keep track of the number of times the B1 button connected to GPIO pin PA0 has been pressed.

    last_button_state is used to store the last state of the B1 button.

    led_state is used to store the state of the red LED light connected to GPIO pin PC6.

The function first increments the press_count variable whenever the B1 button is pressed.

It then checks the value of the led_state variable and the press_count variable to determine whether to activate or deactivate the LED.

If led_state is GPIO_PIN_RESET (i.e., the LED is currently off) and press_count is 2, the program sets the led_state variable to GPIO_PIN_SET, activates the LED by writing the led_state variable to GPIO pin PC6 and resets the press_count variable to 0.

If led_state is GPIO_PIN_SET (i.e., the LED is currently on) and press_count is 3, the program sets the led_state variable to GPIO_PIN_RESET, deactivates the LED by writing the led_state variable to GPIO pin PC6 and resets the press_count variable to 0.
