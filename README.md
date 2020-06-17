Projeto de Cronômetro.

O que usei para desenvolver o projeto:

IDE: STM32CubeIDE 1.2.0
Placa: BluePill (STM32F103C8T6)
Display: OLED 0.91″ 128×32 I2C White 

Instrumento de medição: HANTEK6022BE


Iniciando (16/06/2020).

Neste dia inicie o projeto tentando usar o display OLED junta da placa BluePill. Usei este site https://controllerstech.com/oled-display-using-i2c-stm32/ como referência.

Apos os testes, criei um código simples de um cronômetro, que basicamente usa a tecnica de superloop (que evita travamentos no código), baseando-se na função "HAL_GetTick()", para o controle do cronômetro. A seguir coloquei o código referenciado anteriormente.

if(HAL_GetTick()-now > tempobase){
		  now = HAL_GetTick();
		  ms++;
	  }

    if(ms>999{ //valor 10
        s++;
        ms=0;
        HAL_GPIO_TogglePin(GPIOC, GPIO_PIN_13);
    }
    if(s>59){
        m++;
        s=0;
    }
    if(m>59){
        m=0;
    }
}

Depois tentei implementar o display OLED, para a exibição do tempo, neste momento me deparei com a primeira dificuldade do projeto, que foi a taxa de altualização do display. No primeiro momento, com minha ingenuidade tentei atuzalizar o display a cada ms, o display até que exibiu os valores de 0 a 1000, contudo demora muito mais de 1 segundo, pra elucidar o nivel da minha loucura eu queria que o display tivesse-se uma taxa de atualização de "1000 FPS". 
Por curiosidade, fiz algumas pesquisas pra saber qual seria a maxima taxa de atualização, e encontrei um cara que tinha conseguido com um display similar a façanha atingindo 150 FPS (o link onde encontrei isso https://hackaday.com/2018/05/08/push-it-to-the-limit-ssd1306-at-150-fps/).

Visto meu erro, descidi usar modestos 50ms ou 20 FPS para a taxa de atualização e apenas exibir os decimos de segundo.