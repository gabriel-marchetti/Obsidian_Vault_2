What good in learning C++?
- When developing native code to run into some odd system.
- Develop fast programs


## How the C++ Compiler Works:
No contexto de gerar um código em C++ há duas grandes etapas que são seguidas: Compilação(Compilation) e Encadeamento(Linking).
Vamos focar na parte de Compilação. 
Qual o processo principal dessa etapa? Transformar arquivos de texto (geralmente com a extensão .cpp) em arquivos intermediários chamados de arquivos objetos(no Visual Studio eles tem a extensão .obj) 
Dentro da compilação também existem etapas:
1) Pré-Processamento.
2) Tokenizing e Parsing (Geração da AST - Abstract Syntax Tree).
3) Gera o código em si, transforma em operações e constantes dentro da arquitetura.

Os arquivos em C++ nada mais são do que conteúdos de possível código, diferente do Java que os arquivos e pastas tem significado para o Compilador. Desse modo, podemos dizer que os arquivos em C++ são meio "genéricos". Então, arquivos não tem um significado formal dentro da linguagem.

#### Pré-Processamento:
A primeira etapa da compilação de um arquivo c++ é a fase de pré-processamento. Nessa etapa, geralmente o compilador lida com as diretivas 
```c++
#define
#include
#if 
#ifdef 
#pragma 
```
Existem algumas coisas interessantes que podem ser feitas para geração de códigos dentro do visual studio. Por exemplo, se clicarmos com o botão direito na solução e irmos em propriedades podemos acessar em Output Files -> Assembler Output para o programa gere código em assembly e se virmos o resultado de uma operação como:
```cpp
int multiply()
{
	return 5 * 2;
}
```
Algumas otimizações podem ser feitas no código assembly, por exemplo, podemos fazer o constant folding e substituir a multiplicação de duas constantes pelo resultado.  

## FlashCards
Quais são as etapas que seguem a geração de um código em C++?
?
A primeira etapa é a de compilação e logo depois a fase de encadeamento.

