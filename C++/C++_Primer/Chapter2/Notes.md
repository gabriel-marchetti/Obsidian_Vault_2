Aqui o livro comenta sobre questões mais interessantes sobre a linguagem.
Veja que devido ao ambiente de customização diverso do C++ toda operação pode se tornar confusa:
```
i = i + j
```
Veja, por exemplo, a operação mostrada acima, nela não podemos ter certeza do que a operação faz sem saber os tipos de $i$ e $j$. Como vimos no [[1_note]] em Sales_item tinhamos que a operação '+' juntava informações.
![[Pasted image 20250610163515.png | center]]
## Signed and Unsigned
Dentro dessa classe estamos nos referindo a números em que o sinal não faz sentido, como em problemas de contagem, ou que seja necessário, como em um esquema de fluxo de caixa de uma empresa. Para os tipos básicos como $\texttt{short, int, long, long long}$ todos POSSUEM SINAL. Se quisermos omitir o sinal podemos fazer $\texttt{unsigned short, unsigned int, unsigned long, unsigned long long}$. Contudo, para o tipo de 1 byte o $\texttt{char}$ temos que o padrão é esse ser sem sinal e se quisermos usar o com sinal utilizamos o $\texttt{signed char}$.

**AVISO:** Se precisarmos utilizar um pequeno inteiro através de um $\text{char}$ então devemos SEMPRE especificar o tipo, se é signed ou unsigned. Isso ocorre, porque algumas máquinas utilizam o signed como padrão e outras utilizam o unsigned.

## Type Conversions:
Alguns data types admitem conversão automática para um tipo adequado.
```cpp
bool b = 42; // b is true
int  i = b;  // i holds 1
i = 3.14     // i holds 3
double pi = i // pi holds 3.0
unsigned char c = -1 // c holds 255 (-1 mod 256).
signed char c2 = 256 // c2 is undefined.
```
OBS: Usar o compound initialization evita esse problema.

Fazer contra com unsigned e int's pode se tornar muito confuso, pois a operação padrão do C++ é converter todos os tipos signed para unsigned e realizar a operação. 

## Literals:
Podemos escrever inteiros através da base Octal, Decimal e Hexadecimal.
```cpp
20   // Para a base decimal.
024  // Para a base octal.
0x14 // Para a base hexadecimal.
```
