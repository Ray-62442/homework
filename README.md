# 第一次作业
这是电控第一次作业
1.HAL_Delay版闪烁：/* USER CODE BEGIN 3 */
		HAL_Delay(250);
		HAL_GPIO_TogglePin(GPIOC, GPIO_PIN_13);
		
  		}
		  /* USER CODE END 3 */
2.定时器中断版闪烁： /* USER CODE BEGIN 2 */
		HAL_TIM_Base_Start_IT(&htim2);
  		/* USER CODE END 2 */
3.外部中断版闪烁PS需要把上面那段代码注释掉：/* USER CODE BEGIN 4 */
	void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)
	{
		if(htim->Instance == TIM2)
		{
			HAL_GPIO_TogglePin(LED_GPIO_Port, LED_Pin);
		}
	}
	void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)
	{
		static uint32_t last =0;
		uint32_t now=HAL_GetTick();
		if(GPIO_Pin ==GPIO_PIN_0)
		{
			if (now-last <20)
			{
				return;

			}
			else
			{
				last = now ;
				HAL_GPIO_TogglePin(LED_GPIO_Port,LED_Pin);
			}
		}
	}
		
			
/* USER CODE END 4 */
硬件：PA0-51行，GND-36.37行,PB0-44行,LED-20行
视频1.2.3分别对应第123题