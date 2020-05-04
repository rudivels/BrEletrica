# Iniciando o projeto de CANBUS para o BRElétrico
Rudivels @Abril 2020

Pasta local  
`/Users/rudi/src/Breletrico/`



# 1. Apresentação 
O Gurgel BR800 foi projetado pelo Gurgel Motores na década de setenta com uma proposta inovadora de ser um veículo leve, pequeno, acessível, ou seja, o primeiro carro popular brasileiro. Estes caractersíticas tornam-o apropriadao para ser convertido para tração elétrica. Entretanto, a proposta de transformação do BR800 não se resumo somente a trocar a máquina de tração, mas tem como proposta desenvolver tecnologias para a eletrificação do setor de transportes. Neste sentido os princípios que nortearam a transforção são:

- O carro será usado como laboratório com acesso fácil a todos os novos componentes;
- Instalação de instrumentação em todos os pontos de interesse para ter o máximo de dados;
- Tecnologia livre: código fonte aberta e também hardware não proprietário;

A primeira conversão foi realizado com o BR800 instalada no dinamômetro trocando o motor de combustão por motor elétrico [1]. Em seguido um banco de baterias foi instalada e o sistema de arrefecimento do motor e seu controlador. Este sistema de arrefecimento foi desenhada de tal forma que facilite o acesso aos componentes e sua instrumentação [2]. O banco de baterias também foi organizado em módulos para faciliar o acesso e manuseio [3]. 

A segunda etapa da conversão é o redesenho de toda parte elétrica convencional do carro, como por exemplo, farois, luzes e demais assessórias num barramento usando tecnologia de rede local automotiva mais moderna. O BR800 foi desenvolido na década de oitenta e naquela época o sistema elétrico do veículo era realizado com relés e interruptores. Dessa forma é necessária desenhar um novo arranjo da instalação elétrica do carro, levando em conta a necessidade de instrumentação e monitoramento, segurança, e eficiência energética. 

A estratégia será de organizar a parte elétrica em diversos subsistemas inteligentes que conversarão entre si por meio de uma rede de comunicação. Essa rede de comunicação será baseada na tecnologia *Control Area Network (CAN)*, e a seguir serão descritos os diversos subsistemas e sua funcionalidade. 

# 2. Subsistemas

Os veículos modernos usam diversos subsistemas específicos para controlar as diversas funcionalidades do carro e estes subsistemas comunicam uns com os outros usando o barramento de comunicação. Os principais subsistemas são:

- Subsistema de tração e freio;
- Subsistema de armazenamento de energia;
- Subsistema de instrumentação e sinalização;
- Subsistema de portas, vidros e demais assessórios.

Há dois barramentos de comunicação no veículo. O primeiro é um barramento *Control Area Network (CAN)* de alto velocidade que estabelece a comunicação entre os subsistemas críticos como tração e armazenamento. A comunicação entre os demais subsistemas é realizado por um barramento CAN de baixa velocidade. O subsistema de instrumentação também funcionará como ponte entre os dois barramentos.

O diagrama de blocos abaixo mostra os componentes e os dois barramentos CAN.

![Diagrama](./blob/master/Diagrama_blocos_BBB_Modbus_Can.jpg)

Assim o subsistema de tração do veículo, composto pelo motor elétrico e o seu controlador recebe os comandos de velocidade e direção do condutor e disponibiliza todos os dados como rotação do motor, tensão e corrente do motor, temperatura do controlador etc, no barramento CAN de alta velocidade.

Da mesma forma o sistema de armazenamento de energia composto pelas baterias, o *Battery Management System (BMS)*, também disponibiliza os dados pelo barramento CAN de alta velocidade. 

O subsistema de sinalização, luzes e monitoramento de temperatura e velocidade estão interligados no barramento CAN de baixa velocidade.

O computador de bordo funcionará como ponte entre as duas barramentos e também apresentará os dados do funcionamento do veículo por meio de uma interface interativa.


[Subsistemas no barramento CAN de baixa velocidade](./Modulos_arduino_can/MOD_ARDUINO_README.md)

[Subsistemas no barramento CAN de alta velocidade](./Beagleboard_can/BBB_CAN_README.md)

[Sistema de gerenciamento de energia](./rasp_can/RASP_CAN_README.md)

# Bibliografia
 

1) Vieira MVB, Els RH van, Khalil SB. Avaliação de um veículo a combustão interna convertido para tração elétrica. Congr. iniciação científica Univ. Brasília, 2015, p. 1–9. 
[link para artigo](http://fga.unb.br/rudi.van/galeria/artigo-marcus-vieira-pibic-relatorio-final-envio-2015-08-08-00.pdf). 

2) Els PPD van, Veiga IVA, Freitas RCM de, Els RH van, Viana DM. Conversão de BR800 e dimensionamento do sistema de arrefecimento. Congr. do 13 salão Latino-Americano Veículos Híbridos-Elétricos, São Paulo-SP: 2017.
[link para artigo](http://fga.unb.br/rudi.van/galeria/pedro-paulo-dunice-van-els.pdf)

3) Freitas RCM de, Veiga IVA, Miranda ARS de, Pedro Paulo Dunice van Els, Els RH van, Viana DM. Plataforma de ensaio para conversão de veículos elétricos com motor de imã permanente sem escovas e banco de baterias. Congr. do 13 salão Latino-Americano Veículos Híbridos-Elétricos, São Paulo-SP: 2017.
[link para artigo](http://fga.unb.br/rudi.van/galeria/renata-cunha-moraes-freitas2.pdf)

4) Ribeiro A do N, Meneghin P, Els RH van. Developing technology for a Brazilian hybrid electric mini car. 2nd Lat. Am. Conf. Sustain. Dev. Energy, Water Environ. Syst., 2020, p. 1–10. 
[link artigo](http://fga.unb.br/rudi.van/galeria/arrigo-alex-lasdewes20-fp-161.pdf)

