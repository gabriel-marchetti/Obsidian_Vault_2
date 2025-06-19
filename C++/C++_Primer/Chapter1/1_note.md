**Problem of the Chapter:** Simple program for a bookstore.

Keep a file of transactions of our bookstore, one example of such transaction can be:
0-201-70353-X 4 24.99

0-201-70353-X: ISBN (International Standard Book Number).
4: Number of copies sold at that price.
24.99: Price of copies of that book in such price.

Problem Tasks:
- Number of copies sold.
- Total Revenue from one book.
- Average Sales Price.

# Writing a Simple C++ Program.
Every function in C++ has 4 features: **return type, function name, parameter list(possibly empty) and function body.**

Aqui há um comentário interessante sobre datatypes:
	Dentro do C++ um datatype define não só o que essa variável carrega, mas também quais operações é possível fazer com tal datatype.

# A First Look at Input/Output:
O C++ não possui nativamente um mecanismo de Input/Output. Contudo, devido à sua extensa library STL temos a biblioteca iostream que é um conjunto da istream e da ostream. Stream se refere a uma sequência de caracteres lidos sequencialmente gerados ou consumidos.

### Four main objects:
1) cin - standard input
2) cout - standard output
3) cerr - standard error
4) clog - Confirma etapas de execução de um código.

cerr e clog são definidos dentro de ostream, o primeiro faz parte da biblioteca para garantir o aviso de warnings e erros, enquanto o segundo é utilizado para definir etapas de execução do programa. Cada um desses objetos é associado a uma janela dentro do sistema operacional. 

Aqui também há um comentário interessante sobre o std::endl. Ele não só indica uma criação de uma nova linha, como também faz o flush do buffer. Um comentário mais profundo pode ser visto em:
![[Pasted image 20250609090921.png | center]]
Também há uma explicação sobre o operador :: que se refere a um operador de escopo. Desse modo, quando escrevemos std::endl estamos dizendo que a função endl faz parte do escopo de std. 

### Comment Pair Do Not Nest.
Uma coisa útil nesse capítulo é o fato de que os comentários multi-line não podem ser aninhados, pois vejamos o seguinte exemplo:
```cpp
/*
 * Esse comentário vai ter erro
 * /* */
 */
int main()
{
}
```
Veja que o primeiro \*\/ consome como comentário o segundo \/\*. Desse modo, temos um erro que pode não ser detectado pelo compilador e tornando dificil de entender a origem de um erro. 

**BOA PRÁTICA:** Quanto estamos debuggando um código e desejamos comentar um bloco de código, a melhor abordagem é através de comentar através de \/\/ pois assim não teremos problemas de comentários aninhados.

## Reading an Unknown number of inputs:
Suponhamos que desejamos criar um código que lê um número indefinido de entradas e realiza a sua soma. Desse modo, teremos que:
```cpp
#include <iostream>

int main()
{
    int readVal{0}, sum{0};
    while(std::cin >> readVal)
    {
        sum += readVal;
    }

    std::cout << sum << std::endl;
}
```
Aqui há comentários interessantes sobre a estrutura istream. Como o retorno da operação $\texttt{std::cin >> readVal}$ retorna uma estrutura $\texttt{std::cin}$ então quando dermos entradas válidas, nesse caso um inteiro, então a istream retornará TRUE na condição. Caso, entremos com um valor não esperado como um char, a istream "invoca" um erro tornando a sua avaliação FALSE, além disso encontrar um objeto EOF (end of file) também invoca esse erro.
**OBS**: Dentro do WINDOWS um indicador do terminal de end-of-file é CTRL-Z e dentro de sistemas UNIX é o CTRL-D.

## Introducing Classes.
Para fazer o design de uma classe é necessário que façamos três perguntas:
- Qual o nome da classe?
- Onde ela está definida?
- Quais operações ela suporta?

Quando definimos uma classe geralmente é feita uma interface através de um header file .h e invocamos dentro do nosso código as classes desse tipo.