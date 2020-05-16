# Barramento CAN de Alta Velocidade
Rudivels @Abril 2020

Pasta local  
`/Users/rudi/src/BrEletrica/Barramento_Alta_Can/`

  
# 1. Apresentação 

No BRElétrico o barramento CAN de alta velocidade liga seguintes componentes:

- Controlador do Motor (PM BLDC Guandong); 
- Battery Management System (EK-YT-21-BMS);
- Módulo de gerenciamento de energia;
- Computador de Bordo.

A seguir as especificidades de cada módulo será apresentado.


# 2. Módulo de gerenciamento de energia
Este módulo terá a função de monitorar e gerenciar todo fluxo de energia no veículo elétrico. A partir dos dados transmitidas no barramento CAN este módulo pode registrar o consumo do sistema de tração. O módulo também vai de monitorar e controlar o carregamento das baterias de 12v e 24v. O circuito de 12Volts alimenta todos os sistemas elétricas convencionais no veículo como luzes, buzina, instrumentação e tem como armazenador (por enquanto) uma bateria automotiva chumbo ácido convencional. A previsão é de mudar essa bateria para uma tecnologia mais adequado.
 
Além deste circuito de 12Volts o BRElétrica precisa de um circuito de 24Volts para alimentar o rele de força para ligar o circuto de potência em 200Vdc da bateria de tração ao Controlador do motor de tração. Não se conseguiu resultados satisfatórios e estáveis com reles de 12Vdc, e por isso optou-se em instalar um circuito separado. Num futuro todos os circuitos de potência secundário de um carro elétrico podem ser alimentado por este circuito (por exemplo sistema de arrefecimento do motor e condiciomanento do ar). 

Este módulo tem a função de recarregar as baterias de 12 e 24Volts a partir da rede elétrica convencional. Além disso por meio de um conversor CC-CC esté módulo pode comandar a carga das baterias secundárias a partir do banco de bateria de tração. 
Uma outra opção será de carrgar as baterias secundárias a partir de um  painel de energia solar fotovolaitico no teto do veículo.

O módulo monitorá o consumo das baterias e por meio do barramento CAN informará todos os dados para os demais sistemas e o computador de bordo. Devido a complexidade do módulo ele será implementado num minicomputador compacto Raspberry. A documentação deste módulo está no [repositório](../rasp_can/RASP_CAN_README.md)


# 3. Controlador do motor (PM BLDC Guandong)

Descrição do controlador do motor.

Instrument: the CAN bus communication specification

|-----------|-------------|---------|
| BYTE1 | voltage low byte	  |0.1V/bit offset：-10000 range：0 V～500V |

|------|------|------|------|------|-----|------|------|
|reserved|Ready for|reserved|reserved|stop|brake|backward|forward|


| BIT7 | BIT6 | BIT5 |	BIT4 |	BIT3 |	BIT2 | BIT1 | BIT0 |
|------|------|------|------|------|-----|------|------|

```


# 4. Battery Management System BMS (EK-YT-21-BMS)

Descrição do BMS.

Com o osciloscópio mediu-se o sinal no barramento CAN e descobriu-se que a velocidade de comunicação do barramento era de 250khz. 
Funcionamento do Modulo concentrador de comunicação.
Sistema composto por 4 modulos de 16 celular LIFEPO4, ligado por meio de uma barramento próprio, passando alimentação e sinais para o modulo concentrador. Este modulo concentrador tem duas portas CAN. Uma porta para  o Battery Charger e outro avulso. 

Foi feito o teste no 14/05/2020 com Arduino e Can sheild da sparkfun. 
Ligou somente um modulo de batterias (tensão +-40 volts) e o display do BMS. 
Sem ligar o sparkfun o barramento mostra uma atividade muito intensa no osciloscópio. Assim que coloca o sparkfun, no barramento aparece somente vem um pacote de dados a cada 2 segundos.

Usou programa 
`CAN Read Demo for the SparkFun CAN Bus Shield.`
Da biblioteca de CAN do Arduino Shield. Somente configurou o programa para 250khz e a porta serial 57200 bps. 


Quando liga o concentrador somente com um modulo e o display e o Arduino CAN Shield.  

Primeiro teste arduino 

```
CAN Read - Testing receival of CAN Bus message
CAN Init ok
ID: 601, Data: 89 99 00 0F 01 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 01 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 01 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 01 00 00 00 

```

Quarta teste

```
CAN Read - Testing receival of CAN Bus message
CAN Init ok
ID: 601, Data: 89 99 00 0F 00 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 00 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 00 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 00 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 00 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 00 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 01 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 01 00 00 00 
ID: 33C, Data: 80 00 00 00 00 00 00 00 
ID: 601, Data: 89 99 00 0F 01 00 00 00 
```


Vamos agora testar com o programa <https://github.com/kahiroka/slcanuino>
que permite usar o candump e outras ferramentas na próxima tentativa de depuração do barramento.




# Bibliografia
 

4) Ribeiro A do N, Meneghin P, Els RH van. Developing technology for a Brazilian hybrid electric mini car. 2nd Lat. Am. Conf. Sustain. Dev. Energy, Water Environ. Syst., 2020, p. 1–10. 
[link artigo](http://fga.unb.br/rudi.van/galeria/arrigo-alex-lasdewes20-fp-161.pdf)

[Volta](../README.md)