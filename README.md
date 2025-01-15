# STM32-SERVO-MOTOR-CONTROL
This is a simple code you can use to control an SG90 Servo Motor using an STM32 microcontroller.
The full tutorial is available on YouTube: 
    //Set the timer frequency to 50Hz
    
    /* USER CODE BEGIN 0 */
    // Function to set servo angle
    void Set_Servo_Angle(TIM_HandleTypeDef *htim, uint32_t channel, uint8_t angle)
    {
        // Map angle (0-180) to pulse width (210-1050 counts)
        //210 for 0.5ms (0 degrees) and 1050 for 2.5ms (180 degrees)
        uint32_t pulse_length = 210 + (angle * (1050 - 210) / 180);
        __HAL_TIM_SET_COMPARE(htim, channel, pulse_length);
    }
    /* USER CODE END 0 */
  
  
    /* USER CODE BEGIN 2 */
    // Start the PWM signal generation
    HAL_TIM_PWM_Start(&htim2, TIM_CHANNEL_1);
    /* USER CODE END 2 */
  
    /* Infinite loop */
    /* USER CODE BEGIN WHILE */
    while (1)
    {
      /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
	  // Sweep servo from 0 to 180 degrees
	          for (uint8_t angle = 0; angle <= 180; angle += 10)
	          {
	              Set_Servo_Angle(&htim2, TIM_CHANNEL_1, angle);
	              HAL_Delay(100);
	          }

	          // Sweep back from 180 to 0 degrees
	          for (uint8_t angle = 180; angle > 0; angle -= 10)
	          {
	              Set_Servo_Angle(&htim2, TIM_CHANNEL_1, angle);
	              HAL_Delay(100);
	          }

      }
      /* USER CODE END 3 */
    }
