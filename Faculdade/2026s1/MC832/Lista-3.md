---
tags:
  - redes-de-computadores
---
1) Qual é o papel da camada de transporte em uma arquitetura em camadas? Explique como ela se relaciona com a camada de rede e por que não basta apenas a entrega entre hosts

**Resposta**: O papel da camada de transporte é servir de intermediário entre a camada de aplicação e a camada de rede. Seu papel é ser uma API entre os sockets abertos entre transporte e camada de aplicação e preparar os segmentos para conseguir se comunicar com a rede. Dentro dessa camada diversas ações podem ser feita, como verificação dos pacotes enviados através de checksums ou até mesmo criar arquiteturas para mandar dados de forma confiáveis através de protocolos como o TCP. Veja que ela se relaciona com a camada de rede, pois ele prepara os pacotes para eles conseguirem transitar dentro da rede, ou seja, pode anexar IPs e Portas dentro do segmento que são atributos essenciais para a comunicação em rede. Portanto, precisamos perceber que a questão não é envio sobre hosts e sim envio sobre processos, de modo que um host pode tanto processos clientes como processos servidores, portanto, na arquitetura da rede não basta pensar em hosts e sim no papel exercido por esse host, ou seja, se ele é sender ou receiver de dados.

OBS:
- A camada de transporte se preocupa com a multiplexação e demultiplexação através de portas, o protocolo de IP é responsabilidade da camada de rede.

2) O que significa dizer que a camada de transporte oferece comunicação processo a processo? Relacione sua resposta com portas e com a entrega dos dados à aplicação correta.

**Resposta**: Dizer que a camada de transporte oferece comunicação processo a processo significa dizer que um mesmo host pode abrir diversos processos, que podem ser tanto sender como receiver de mensagens, de modo que essas mensagens sejam encaminhadas para o socket específico do processo. Pense que temos duas aplicações, como abas dentro de um navegador, que se comunicam com o mesmo servidor, note que cada aba irá fazer suas requisições HTTP para alcançar um servidor, então a maneira dessas mensagens não serem confundidas entre as abas podemos utilizar as portas dos sockets.

3) Explique os conceitos de multiplexação e demultiplexação na camada de transporte. Por que esses mecanismos são necessários em um host que executa várias aplicações ao mesmo tempo?

**Resposta**: Podemos pensar em processos, em vez de pensar em aplicações. Pense que um host pode abrir diversas requisições de cliente para um servidor HTTP, contudo, cada aplicação pode pedir informações diversas e distintas, portanto, há de haver um mecanismo de controlar o recebimento das mensagens para o processo A ou para o processo B. Dentro do cliente, existem diversas portas e no momento de transmissão a rede não faz sentido elas serem expostas, uma vez que essa informação só será utilizada no destino, portanto, há o processo de multiplexação, onde as informações de porta são encapsuladas pelos protocolos de rede. Contudo, no momento que essa informação chegar no servidor HTTP elas precisam atingir a porta correta, desse modo, há o processo de demultiplexação, em que os pacotes que chegam são direcionados para a porta correta. Portanto, podemos perceber quão importante são os mecanismos de multiplexação e demultiplexação para comunicação entre diferentes processos dentro da rede.

4) Suponha que você precisa projetar uma aplicação remota que deseja responder o mais rápido possível ao usuário. Você usaria TCP ou UDP? Discuta em que contexto cada escolha faria mais sentido, considerando confiabilidade, controle de congestionamento e requisitos da aplicação.

**Resposta**: Veja que não existe bala de prata quanto à questão de escolher um protocolo, ou seja, não há protocolo que resolva todos os problemas. Veja que por se tratar de velocidade, o protocolo UDP tem menor latência de envio da mensagem, uma vez que não há o processamento do handshake, reduzindo em 1 RTT (Round Trip Time) para chegar transmissão  do dado. Contudo, essa resposta é simplista se considerarmos que pode haver perda de pacotes, pois não há controle de fluxo, comunicação para reconhecimento do recebimento da mensagem e mecanismos para garantir a comunicação. Portanto, a questão é que aplicações que admitem uma quantidade de erro de transmissão e precisam ser rápidas podem usar o UDP, dado que a reconstrução da imagem não precisa de todos bits perfeitamente, mas precisa de latência baixa entre dados, como em serviços de streaming. Contudo, se houver uma grande perda de pacotes isso poderá tornar a aplicação inutilizável e a utilização da transmissão TCP teria uma "entrega" mais rápida para essa atividade, uma vez que o UDP erraria várias vezes e precisaria retransmitir várias vezes através da camada de aplicação.

5) O que caracteriza um protocolo sem conexão, como o UDP? Explique quais garantias ele não oferece e por que, ainda assim, ele continua sendo útil em várias aplicações.

**Resposta**: Um protocolo sem comunicação é caracterizado pelo recebimento do segmento pelo *receiver* não ser seguido de uma mensagem de reconhecimento desse recebimento. Desse modo, o protocolo UDP não garante controle de congestionamento, controle do fluxo de envio das mensagens e retransmissão dos dados corrompidos. Veja que ele continua sendo útil para aplicações que necessitam de uma rápida taxa de transmissão, mas que admitem uma quantidade de erros, como serviços de streaming e de jogos online.

6) Quais são as principais vantagens de usar UDP em vez de TCP?

**Resposta**: As principais vantagens de usar UDP em vez de TCP são a velocidade de transmissão e se tratar de um protocolo mais simples. Em primeiro lugar, pelo fato não haver mecanismos para controle de transferência de dados confiável a mensagem é transmitida de maneira mais rápida, assim como por ser um protocolo mais simples é mais fácil de entender e consequentemente carrega menos dados, portanto, causa menos gárgalo dentro da rede. Também podemos comentar que pelo fato do TCP ter controle de congestionamento da rede, ele não utiliza a banda disponível, enquanto aplicações UDP não se preocupam com isso.

7) Qual é a função do checksum no UDP?

**Resposta**: A função do checksum dentro do UDP é garantir que os dados transmitidos sejam verificados para sistemas que possuem falhas por inversão de bits, podemos argumentar que esse mecanismo não é robusto, pois pode dar uma falsa validação de um dado que está corrompido. 

8) 