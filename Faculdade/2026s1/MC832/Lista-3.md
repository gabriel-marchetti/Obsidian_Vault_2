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

8) Quais problemas um protocolo de transferência confiável precisa resolver quando opera sobre um serviço não confiável? Comente perda, corrupção, duplicação, reordenação e temporização.

**Resposta**: Essa questão está diretamente relacionada com as versões de rdt (reliable data transfer). Em primeiro lugar, podemos comentar sobre a perda de a corrupção de pacotes, esse mecanismo pode ser parcialmente evitado através de mecanismos de checksum, o fato de ser parcialmente evitado é que uma corrupção de dados específica pode ocasionar na falha da detecção pelo checksum. Sobre a perda de pacotes há uma comunicação através de ACKs ou NACKs onde cada pacote recebido é mandada uma mensagem positiva ou negativa, além disso mecanismos de duplicação e reordenação podem ser feito através de numeração dos pacotes que poderá facilitar para o recebedor de saber quais pacotes são duplicados e em qual ordem eles devem chegar. Por fim, o mecanismo de temporização é utilizando para resolver casos em que um canal de comunicação é afetado durante a comunicação, veja que eles são importantes para retransmissão da mensagem caso algo inesperado aconteça.

OBS: podemos falar sobre o modelo "Stop-and-Wait" em que um pacote é enviado e espera o ACK para mandar outro pacote.

9) Explique a função dos ACKs, dos números de sequência e dos temporizadores em protocolos de transferência confiável.

**Resposta**: Os ACKs, números de sequência e temporizadores são mecanismos para tornar canais de comunicação não confiáveis em mecanismos mais confiáveis para comunicação. Em primeiro lugar, vamos comentar sobre os ACKs, eles funcionam através do mecanismo de "Stop-and-Wait" em que o envio de um próximo pacote do sender só é realizado após o recebimento de um ACK do receiver, veja que isso garante que o canal de comunicação seja mais transparente para ambas entidades da rede. Agora podem existir problemas de que um pacote é enviado por um percurso mais rápido do que o anterior, desse modo podemos utilizar os números de sequência em que um número é atribuído para cada pacote e a mensagem de ACK é seguida de um número do pacote, veja que isso mantém a comunicação entre as entidades mais coordenadas. Por fim, temos os temporizadores, veja que se um pacote se perde pelo caminho da rede, então o receiver nunca irá mandar o ACK para esse pacote que geraria um stall da comunicação entre sender e receiver, portanto, o mecanismo de temporização serve para garantir a retransmissão do pacote caso isso ocorra.

OBS: o número de sequência é mais utilizado para detecção de duplicatas.

10) O que significa dizer que um protocolo confiável é pipelined? Explique por que essa ideia pode melhorar o desempenho em comparação com um envio estritamente sequencial.

**Resposta**: Dizer que um protocolo confiável é pipelined significa dizer que ele possui um mecanismo para envio simultâneo de diversos pacotes. Para avaliar a melhora do desempenho vamos primeiro ver o gargalo do envio estritamente sequencial, uma ação que ocorre geralmente é que há um processamento por um host seguido da transmissão da mensagem para um outro host que irá mandar a mensagem de ACK, veja que esse mecanismo sugere que para cada pacote enviado haverá um atraso de RTT. Desse modo, os mecanismos de pipeline tentam tirar proveito dessa questão, em que diversos pacotes são enviados nesse meio tempo, desse modo há um claro aumento de performance, pois estamos reaproveitando o tempo.

OBS:
Podemos utilizar a fórmula de utilização do sender para comprovar isso.
No mecanismo sequencial "stop-and-wait", temos que:
$$
U_{\texttt{sender}} = \frac{L/R}{RTT + L/R}
$$
Se utilizarmos o modo de pipeline, temos que:
$$
U_{\texttt{sender}} = \frac{N * L/R}{RTT + L/R}
$$
11) Compare Go-Back-N e Selective Repeat. Aponte diferenças na forma de reconhecer dados, armazenar pacotes e retransmitir em caso de perda.

**Resposta**: o Go-back-N possui ACK cumulativo, ou seja, uma mensagem de ACK deve ser interpretada como "recebi todos os pacotes até o índice x", enquanto dentro do Selective Repeat temos que cada ACK é individual. Além disso, temos que o receptor não precisa de buffer para o Go-back-N, uma vez que ele atua de uma forma sequencial, isto é, ele espera uma ordem de chegada de pacotes, enquanto o Selective Repeat precisa de um buffer no receptor para que ele consiga tratar os pacotes no modo fora de ordem. Por fim, também temos que a retransmissão de mensagens dentro do Go-Back-N é mais intensa, uma vez que ele precisa enviar diversos pacotes duplicados, enquanto o Selective Repeat reenvia apenas pacotes que ainda não foram processados.

12) Em termos de simplicidade e eficiência, quais são os principais trade-offs entre Go-Back-N e Selective Repeat?

**Resposta**: Veja que o modo Selective Repeat é mais eficiente de um modo geral, pois ele tem tratamento individual de pacotes, isto é, há um temporizador para cada pacote, reconhecimento de ACKs para cada pacote e por ai vai, portanto, ele é mais eficiente, pois não tende a reenviar muitos pacotes repetidos, contudo isso vem com um custo de processamento individual de cada pacotes, por exemplo os temporizadores individuais, assim como há necessidade do receptor também precisar de um buffer específico para tratar individualmente os pacotes.