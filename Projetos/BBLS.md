# BamBu Light Status (BBLS)

# Visão Geral da Solução:
- A Bambu Lab A1 tem funcionalidade de conexão com o WiFi. 
- Utilizar rede local (LAN) para adquirir status da impressora através do protocolo MQTT.
- Microcontrolador (Como ESP32) se conecta à rede WiFi que a impressora está conectada.
- O Microcontrolador lê os sinais enviados pela impressora.
- Com base na mensagem podemos interpretar os sinais.

# Princípios Básicos necessários para a solução.
## Princípios Eletrônicos.
**O que é um LED e como ele funciona?** 
- Polaridade do LED.
**O que é um Resistor e como ele funciona?**
- Necessidade da utilização de um resistor para evitar que o LED queime.
- Qual a resistência necessária para esse função? ($220 \ohm \text{ ou } 330 \ohm$).
**O que é um Protoboard?**
- Por que ele será necessário para criação das conexões?

**OBS:**
- Buscar material de como ascender um LED através de um Arduíno ou de uma ESP.

## Programação básica de microcontroladores.
- Linguagem básica em C/C++.
- Qual Stack é utilizada para programação de microcontroladores?
- Ferramentas para depuração de código de microcontroladores?

## Comunicação em Rede (MQTT).
- O que é o protocolo MQTT.
- Pesquisar materiais como "Comunicação MQTT com ESP32/Arduino".

# Passo-a-Passo para solução do Problema.
Na impressora:
1) Habilitar modo LAN dentro da impressora para habilitar comunicação local entre dispositivos.
2) Encontrar o IP e Access Code da impressora.
O Circuito:
3) Conectar cada LED a um GPIO da ESP32.
4) 

