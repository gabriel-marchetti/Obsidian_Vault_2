---
tags:
  - redes-de-computadores
---
# Introduction and Transport-Layer Service:

## Services provided by Transport Layer:
- Multiplexing and Demultiplexing
- Reliable Data Transfer
- Flow Control
- Congestion Control
## Protocols Offered:
- UDP
- TCP

**Logical communication** between applications, i.e., abstract the way the applications are connected.

## Transport vs Network Layer service and protocols:
A analogia que é feita aqui é o o "Network-Layer" é como um serviço postal.
Desse modo, o **Network-Layer** se preocupa em fazer a comunicação entre diferentes **hosts**.
Enquanto, o **Transport-Layer** se preocupa em fazer comunicação entre diferentes **processos**.

**TCP** (Transmission Control Protocol):
- Reliable, in-order delivery.
- Congestion Control.
- Flow Control.
- Connection Setup.
**UDP** (User Datagram Protocol):
- unreliable, unordered delivery.
- best-effort delivery.

**Services Not Available**:
- Delay Guarantees.
- Bandwidth Guarantees.

# Transport Layer Multiplexing and Demultiplexing:
**Demultiplexing**: Considere que diversos datagramas estão chegando dentro de um host, o processo aqui é justamente organizar isso.

**Multiplexing**: Processo contrário.

![[Pasted image 20260425180225.png]]
Os Headers são importantes para inserir informações para esse processo.
**How demultiplexing works**: o host utiliza de endereços IP e número de porta para direcionar o segmento para o socket apropriado.

Note que aqui há alguns conceitos, temos o **host-local** port number, que é a porta criada localmente. 

## Demultiplexing UDP:
Connectionless demultiplexing
Para criar um Datagrama UDP precisamos especificar um IP de destino, assim como uma porta.

![[Pasted image 20260425181129.png]]
## Demultiplexing TCP:
Connection-oriented multiplexing
Aqui haverá uma tupla com as informações (source IP address, source port number, dest IP address, dest port number), no processo de demultiplexação o recebedor irá utilizar essas quatro informações para definir um socket apropriado.
![[Pasted image 20260425181724.png]]
Veja que cada uma das requisições criou um socket diferente dentro do servidor HTTP.

## Connectionless Transport: UDP:
**UDP** (User Datagram Protocol) - sender send services and believes it will reach receiver.
**Connectionless** - no handshake is needed between UDP sender and receiver.
Cada segmento será tratado de maneira independente.

A utilização do UDP é decorrente do fato de:
- Há menor atraso, uma vez que não é necessário a conexão.
- É um protocolo mais simples.
- O header é menos informativo, portanto possui menos tamanho.
- Não se interessa com congestionamento.

Você consegue fazer com que o UDP seja confiável dentro da camada de aplicação.
As etapas que ocorrem são a seguinte:
1) Um host pode mandar uma mensagem através do UDP, para isso haverá a abertura de um socket.
2) Após isso a mensagem é passada para a camada de transporte, onde há anexo do segmento UDP.
3) Esse segmento é passado para a camada de Network e irá anexar um datagrama, ou é anexado um IP.

A estrutura de um segmento UDP.

![[Pasted image 20260426114953.png]]

### UDP Checksum:
Detect errors or flipped bits.
Há o envio de dois números e a soma desses dois números. Note que o segmento UDP é tratado como uma sequência de 16 bits, portanto, há envio de dois elementos dessa sequência e o checksum.
![[Pasted image 20260426115442.png]]
Notamos que esse mecanismo de verificação de erro não é robusto. Mudanças nos bits pode resultar na mesma checksum.

# Principles of Reliable Data Transfer:
## Reliable Data Transfer:
**Objetivo**: Tentar entender como criar mecanismos que garantem a transmissão de mensagens em um meio não tão confiável.
Pense que qualquer um dos processos não consegue entender o estado que está o outro processo sem envio de uma mensagem. Ideia da cortina entre eles.

rdt (reliable data transfer protocol):
- define states for rdt.
rdt 1.0 - reliable transfer over a reliable channel.
- separate FSM for sender and receiver.
![[Pasted image 20260426121241.png]]
rdt 2.0 - channel with bit errors:
- Checksum to detect bit errors.
- How to recover from errors? 
- ACKs (Acknowledgements) - receiver replies sender with an Ok message.
- NACKs (Negative Acknowledgements) - receiver tells sender that there were errors in the message.
- sender retransmits packet on the NACKs reply for the server
- O que irá acontecer é que para cada pacote enviado haverá a espera da resposta do servidor. (STOP-AND-WAIT).
![[Pasted image 20260426121952.png]]

rdt 2.0 has a fatal flaw: O que acontece se um ACK ou um NACK for corrompido?
Para lidar com pacotes duplicados podemos adicionar um número de sequência para cada pacote. O recebedor descarta pacotes duplicados.

rdt 2.1 - Adiciona os números na sequência de cada pacote para lidar com falsos ACKs ou NACKs.

rdt 3.0 - Canais podem corromper ou até mesmo perder mensagens.
- Mecanismo: o sender irá começar um temporizador para retransmitir o ACK ou a mensagem de caso haja problema.
- ![[Pasted image 20260426123738.png]]
 ![[Pasted image 20260426124019.png]]
 Para computar a utilização do sender podemos fazer:
 ![[Pasted image 20260426124256.png]]
 Para conseguir aumentar a eficiência da utilização do sender, podemos utilizar o pipeline.
 ![[Pasted image 20260426124411.png]]
 Para conseguir fazer isso podemos utilizar o 
 **Go-Back-N**: 
 1) sender manda até N unACKed packets
 ![[Pasted image 20260426124633.png]]
 ![[Pasted image 20260426124721.png]]
 **Selective Repeat**: Receiver individually ACKed received packets.

## Connection Oriented Transport 
Em contraste ao UDP que é orientado por mensagens, o TCP é orientado por byte streams.
- Cummulative ACKs.
- Pipelining.
- Connection-Oriented.
- Flow Controlled.

$$
\texttt{Estimated RTT} = (1-\alpha) \cdot \texttt{Estimated RTT} + \alpha \cdot \texttt{SampleRTT}
$$
- Usar apenas o $\texttt{SampleRTT}$ varia muito. 
$$
\texttt{Timeout Interval} = \texttt{Estimated RTT} + 4 \cdot \texttt{Deviation RTT}
$$

**TCP sender**:
1) Creates segment with seq #
2) Start timer for oldest unACKed 

**TCP fast retransmit**: If receive 3 ACKs for same data, then resend segment with smallest seq #.
## TCP Reliability, Flow Control, Congestion Control:
**Flow Control**: Receiver controls sender, so sender won't overflow receiver buffer.
Receiver manda quanto de memória livre ele possui no campo rwnd do Header TCP.

### TCP connection management:
- handshake protocol - 2-way handshake and 3-way handshake.
![[Pasted image 20260428145042.png]]
**Closing a TCP connection**.

# Principles of Congestion Control:
Manifestações de congestionamento podem ser percebidas através de **long delays** e **packet loss**. 

Mesmo considerando o caso ideal de um buffer infinito podemos perceber que há um delay muito grande 
![[Pasted image 20260428151420.png]]
Nesse caso aqui haverá uma decadência da curva, porque agora temos o problema de perda de pacotes em buffers cheios. Isto é, o envio de um pacote não corresponde ao recebimento de um pacote. Veja que esse problema é agravado caso consideremos problema de retransmissão de duplicatas.
![[Pasted image 20260428151731.png]]

**End-End Congestion Control**:
- Diminui a quantidade de dados enviados para um receiver à medida que percebe que pacotes estão sendo perdidos.

**Network-Assisted Congestion Control**:
- Roteadores providenciam fedback sobre o fluxo de dados dentro da rede.