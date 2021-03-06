# Projeto de Cronômetro.

![](https://user-images.githubusercontent.com/37257011/85080524-c8807680-b19f-11ea-9361-20e458c95612.gif)

O que usei para desenvolver o projeto:

- IDE: STM32CubeIDE 1.2.0
- Placa: BluePill (STM32F103C8T6)
- Display: OLED 0.91″ 128×32 I2C White 

- Instrumento de medição: HANTEK6022BE


## Iniciando (16/06/2020).

Neste dia inicie o projeto tentando usar o display OLED junta da placa BluePill. Usei este site https://controllerstech.com/oled-display-using-i2c-stm32/ como referência.

Após os testes, criei um código simples para o cronômetro, basicamente usa a tecnica de superloop (que evita travamentos no código), baseando-se na função "HAL_GetTick()" baseada no timer do microcontrolador. A seguir coloquei como fiz o controle do cronômetro.

```
if(HAL_GetTick()-now > tempobase){
    now = HAL_GetTick();
    ms++;
}

if(ms>9{ //valor 10
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
```

Depois tentei implementar o display OLED, neste momento me deparei com a primeira dificuldade do projeto, a taxa de altualização do display. No primeiro momento, com minha ingenuidade tentei atuzalizar o display a cada ms, o display até que exibiu os valores de 0 a 1000, contudo o funcionamento ficava extremamente lento. Para elucidar o nivel da loucura, usar 1 ms representa uma taxa de atualização de "1000 FPS".

Por curiosidade, fiz algumas pesquisas pra saber qual seria a maxima taxa de atualização, encontrei um cara que tinha conseguido com um display similar a façanha de 150 FPS (o link onde encontrei isso https://hackaday.com/2018/05/08/push-it-to-the-limit-ssd1306-at-150-fps/).

Visto meu erro, descidi usar modestos 50ms ou 20 FPS para a taxa de atualização e apenas exibir os décimos de segundo.

## Problemas com o tempo. (17/06/2020)

Como é possivel verificar na figura 1 tive alguns problemas com a contagem de tempo, neste caso aumentei o tempo de atuzalização do display para 100ms, tal mudança proporcionou resultado satisfatório visto na imagem 2. 

![](https://user-images.githubusercontent.com/37257011/84936029-00a88c00-b0b0-11ea-903e-3d39d6aa6695.png)

##### Imagem 1

![](https://user-images.githubusercontent.com/37257011/84948082-8da81100-b0c1-11ea-9261-96e71a5e5d34.png)

##### Imagem 2

## Sensores. 18/06/2020

Para o controle do cronômetro utilizei botões. Isso causou um problema ao projeto o famoso bounce, que foi resolvido com um "delay" na leitura do input.
O projeto foi dividido em três estados, primeiro (status=0) o cronômetro é zerado, segundo (status=1) inicia a contagem e terceiro (status=2) a contagem é pausada.

## FIM

Este foi o passo a passo / diário do desenvovimento de um cronômetro. Caso alguém tenha alguma dúvidas do projeto ou ideias estarei a disposição.





