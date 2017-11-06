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

