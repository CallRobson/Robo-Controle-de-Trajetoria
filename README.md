1. INTRODUÇÃO

A robótica móvel é uma área que desperta a curiosidade de muitos e que tem evoluído bastante nos últimos anos para o desenvolvimento de sistemas de controle de robôs.
O projeto propõe um controle de trajetória de um carro robô usando PID, onde o robô irá sempre seguir reto na direção inicial.
As etapas da construção do veículo estão esquematizadas em três sistemas e consequentemente seus subsistemas, tais como sistema mecânico (estrutura), sistema elétrico e o sistema eletrônico de controle (controle de velocidade, aceleração e posição, motores e bateria).  
No sistema mecânico, a estrutura pode ser comprada onde é composta de chassi e pneus.
A etapa que faz referência a parte elétrica e eletrônica do sistema, serão abordados os motores DC, o sensor de velocidade/aceleração (MPU5060), a ponte H, bateria e o controlador Arduino UNO.

2. EMBASAMENTO TEÓRICO/PRÁTICO

2.1 MODELAGEM DO SISTEMA

O motor de corrente contínua é representado por 3 equações:

●	Equação da armadura 

<p align="center">
  
<a href="https://imgur.com/jUPqjAR"><img src="https://i.imgur.com/jUPqjAR.jpg" title="source: imgur.com" /></a>
  
  
onde "e" a força eletromotriz, "Va" é a tensão de armadura e "Ra e "La" são a resistência e a indutância da armadura, respectivamente.

●	Equação da força eletromotriz

<a href="https://imgur.com/KYwKq7K"><img src="https://i.imgur.com/KYwKq7K.jpg" title="source: imgur.com" /></a>

onde "0m" é o ângulo mecânico e "Ke" é uma constante.

●	Equação do torque gerado

<a href="https://imgur.com/Qr87SVQ"><img src="https://i.imgur.com/Qr87SVQ.jpg" title="source: imgur.com" /></a>

onde "Tm" é o torque mecânico gerado pelo motor e "Kt" uma constante.

Segunda lei de Newton para o movimento de rotação

<a href="https://imgur.com/rBwo2wQ"><img src="https://i.imgur.com/rBwo2wQ.jpg" title="source: imgur.com" /></a>

onde "Jm" é a inércia do conjunto motor-carga, "b" representa um coeficiente de atrito e "d" representa a variação de direção que constitui a perturbação.
O ângulo mecânico é escolhido como variável de saída, ou seja, "y = 0m" . Então as equações da força eletromotriz e do torque gerado são reescritas como:

<a href="https://imgur.com/H4Hhxb9"><img src="https://i.imgur.com/H4Hhxb9.jpg" title="source: imgur.com" /></a>

<a href="https://imgur.com/Rlnz2DM"><img src="https://i.imgur.com/Rlnz2DM.jpg" title="source: imgur.com" /></a>

Fazendo a Transformada de Laplace das quatro equações, tem-se:

 
<p align="center"><b>(1)</b>
<p align="center"><a href="https://imgur.com/TFnhZnh"><img src="https://i.imgur.com/TFnhZnh.jpg" title="source: imgur.com" /></a>
  
<p align="center"><b>(2)</b>
<p align="center"><a href="https://imgur.com/kmisbky"><img src="https://i.imgur.com/kmisbky.jpg" title="source: imgur.com" /></a>
<p align="center"><a href="https://imgur.com/J9flRiF"><img src="https://i.imgur.com/J9flRiF.jpg" title="source: imgur.com" /></a>

<p align="center"><b>(3)</b>
<p align="center"><a href="https://imgur.com/E7CSuRj"><img src="https://i.imgur.com/E7CSuRj.jpg" title="source: imgur.com" /></a>
 
 Isolando o valor de "Ia(S)" na Equação 1, usando a Equação 2 e substituindo na Equação 3, obtém-se:
 
<p align="center"><a href="https://imgur.com/hqkPNwb"><img src="https://i.imgur.com/hqkPNwb.jpg" title="source: imgur.com" /></a>
  
  2.2 DIAGRAMA DE BLOCOS

O projeto do sistema de controle é fundamental para minimizar os efeitos dos distúrbios sobre a variável de processo que, no caso, é o ângulo.

<p align="center"><a href="https://imgur.com/T6YvzYw"><img src="https://i.imgur.com/T6YvzYw.jpg" title="source: imgur.com" /></a>
  
  2.3 FLUXOGRAMA
  
  <p align="center"><a href="https://imgur.com/rak1bFH"><img src="https://i.imgur.com/rak1bFH.jpg" title="source: imgur.com" /></a>
  
  3. IMPLEMENTAÇÃO

3.1 PONTE H

3.1.1 O que é ponte H?

É um circuito composto por um arranjo de 4 transistores, é capaz de acionar simultaneamente dois motores DC controlando não apenas seus sentidos, como também suas velocidades. 
Seu funcionamento dá-se pelo chaveamento de componentes eletrônicos usualmente utilizando do método de PWM para determinar além da polaridade, o módulo da tensão em um dado ponto de um circuito.
As pontes H em possuem este nome devido ao formato que é montado o circuito, semelhante a letra H. O circuito utiliza quatro chaves (S1, S2, S3 e S4) que são acionadas de forma alternada, ou seja, (S1-S3) ou (S2-S4), veja as figuras abaixo. Dependendo da configuração entre as chaves teremos a corrente percorrendo o motor hora por um sentido, hora por outro.

<p align="center"><a href="https://imgur.com/pJtPexn"><img src="https://i.imgur.com/pJtPexn.jpg" title="source: imgur.com" /></a>
  
Quando nenhum par de chaves está acionado, o motor está desligado (a). Quando o par S1-S3 é acionado a corrente percorre S1-S3 fazendo com que o motor gire em um sentido (b). Já quando o par S2-S4 é acionado a corrente percorre por outro caminho fazendo com que o motor gire no sentido contrário (c).

3.1.2 Drive Motor Ponte H - L298N

<p align="center"><a href="https://imgur.com/RUM4UlW"><img src="https://i.imgur.com/RUM4UlW.jpg" title="source: imgur.com" /></a>

Este Driver Ponte H é baseado no chip L298N, construído para controlar cargas indutivas como relés, solenoides, motores DC e motores de passo, permitindo o controle não só do sentido de rotação do motor, como também da sua velocidade, utilizando os pinos PWM do Arduino.

3.1.2.1 Especificações:

– Tensão de Operação: 4~35v

– Chip: ST L298N

– Controle de 2 motores DC ou 1 motor de passo

– Corrente de Operação máxima: 2A por canal ou 4A max

– Tensão lógica: 5v

– Corrente lógica: 0~36mA

– Limites de Temperatura: -20 a +135°C

– Potência Máxima: 25W

– Dimensões: 43 x 43 x 27mm

– Peso: 30g

3.1.2.2 Funcionamento:

<p align="center"><a href="https://imgur.com/yF2jMEz"><img src="https://i.imgur.com/yF2jMEz.jpg" title="source: imgur.com" /></a>

(Motor A) e (Motor B) se referem aos conectores para ligação de 2 motores DC ou 1 motor de passo.

➢	OUT1 - Terminal positivo do Motor 1 DC ou A+ do motor de passo

➢	OUT2 - Terminal negativo do Motor 1 DC ou A- do motor de passo

➢	OUT3 - Terminal positivo do Motor 2 DC ou B+ do motor de passo

➢	OUT4 - Terminal negativo do Motor 2 DC ou B- do motor de passo

(Ativa MA) e (Ativa MB) – são os pinos responsáveis pelo controle PWM dos motores A e B. Se estiver com jumper, não haverá controle de velocidade, pois os pinos estarão ligados aos 5v. Se estiver sem o jumper, esses pinos podem ser utilizados em conjunto com os pinos PWM do Arduino

(Ativa 5v) e (5v) – Este Driver Ponte H L298N possui um regulador de tensão integrado. Quando o driver está operando entre 6-35V, este regulador disponibiliza uma saída regulada de +5v no pino (5v) para um uso externo (com jumper), podendo alimentar por exemplo outro componente eletrônico. Portanto não alimente este pino (5v) com +5v do Arduino se estiver controlando um motor de 6-35v e jumper conectado, isto danificará a placa. O pino (5v) somente se tornará uma entrada caso esteja controlando um motor de 4-5v (sem jumper), assim poderá usar a saída +5v do Arduino.

(6-35v) e (GND) – Aqui será conectado a fonte de alimentação externa quando o driver estiver controlando um motor que opere entre 6-35v. Por exemplo se estiver usando um motor DC 12v, basta conectar a fonte externa de 12v neste pino e (GND).

(Entrada) – Este barramento é composto por IN1, IN2, IN3 e IN4. Sendo estes pinos responsáveis pela rotação do Motor A (IN1 e IN2) e Motor B (IN3 e IN4).

A tabela abaixo mostra a ordem de ativação do Motor A através dos pinos IN1 e IN2. O mesmo esquema pode ser aplicado aos pinos IN3 e IN4, que controlam o Motor B.

