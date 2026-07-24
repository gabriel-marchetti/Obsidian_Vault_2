---
tags:
  - Arduino
---
Dentro do vídeo ele utiliza a própria IDE oferecida pelo Arduino. Mas eu quero usar o próprio VSCODE para alterar meu código, portanto, eu vou utilizar a extensão PlatformIO.

Dentro dessa primeira aula tivemos acesso ao circuito de fazer o LED piscar e suas combinações diversas.

```c++
#include <Arduino.h>

#define LED_RED_1 13
#define LED_RED_2 12

#define DELAY 250

void setup() {
  pinMode(LED_RED_1, OUTPUT);
  pinMode(LED_RED_2, OUTPUT);
}

void loop() {
  digitalWrite(LED_RED_1, HIGH);
  digitalWrite(LED_RED_2, LOW);
  delay(DELAY);
  digitalWrite(LED_RED_1, LOW);
  digitalWrite(LED_RED_2, HIGH);
  delay(DELAY);
}

```
Esse código é utilizado para fazer com que um LED seja acionado, ao mesmo tempo em que o outro LED é desacionado e vice-versa.