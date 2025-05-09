Queremos calcular a sequência:

$$
<0, 1, 1, 2, 3, 5, 8, 13, 21, 34, \cdots > 
$$
Uma abordagem seria:

```C++
#include <bits/stdc++.h>
using namespace std;

int fib(int n)
{
    if(n <= 1)
    {
        return n;
    }

    return fib(n - 1) + fib(n - 2);
}

int main()
{
    int n = 10;
    cout << fib(n) << endl;

    return 0;
}
```
Mas vamos olhar para a pilha do programa para essa solução:

![[Pasted image 20250404155341.png]]

Note que a complexidade do Problema se torna exponencial, podemos majorar por $O(2^n)$ assumindo que cada chamada invoca duas novas avaliações.

Vamos apenas colorir os subproblemas repetidos no diagrama apresentado:
![[Pasted image 20250404155559.png]]
Note que os subproblemas são chamados diversas vezes
$F_{5}$ é chamado 1 vez
$F_{4}$ é chamado 1 vez
$F_{3}$ é chamado 2 vezes
$F_{2}$ é chamado 3 vezes
$F_{1}$ é chamado 5 vezes
$F_{0}$ é chamado 3 vezes
Para avaliar $F_{5}$ tivemos que fazer $1 + 1 + 2 + 3 + 5 + 3 = 16$ somas.
Isso já deve ser um indicativo que devemos utilizar algum tipo de DP para resolver esse problema. Características apresentadas nesse problema
-> Várias chamadas para mesmo subproblema.
-> Fórmula de Recorrência.
Então deve haver uma DP que resolva...

```C++
#include <bits/stdc++.h>
#define MAX_N 10010

using namespace std;

u_int64_t fib_table[MAX_N];

void compute_fib_table()
{
    fib_table[0] = 0;
    fib_table[1] = 1;
    for(int i{2}; i < MAX_N; i++)
    {
        fib_table[i] = fib_table[i-1] + fib_table[i-2];
    }
}

u_int64_t fib( u_int64_t n )
{
    if( n > MAX_N )
    {
        cout << "Fora de Alcance" << endl;
        return 0;
    }

    return fib_table[n];
}

int main()
{
    u_int64_t n;
    compute_fib_table();

    cout << "Digite n para Fib(n): ";
    cin >> n;
    cout << fib(n) << endl;

    return 0;
}
```
O código fornecido resolve o problema de calcular o n-ésimo Fibonacci em tempo $O(n)$ note que isso é MUITO vantajoso se comparado com o algoritmo anterior. Note, entretanto, que esse algoritmo irá utilizar $O(n)$ complexidade espacial.

Um algoritmo ainda mais otimizado que o anterior no sentido de complexidade espacial é:

```C++
#include <bits/stdc++.h>
using namespace std;

u_int64_t fibo(u_int64_t n)
{
    u_int64_t antepenultimate{0}, penultimate{0}, current{0};

    antepenultimate = 0;
    penultimate = 1;
    current = 1;

    for(int i{2}; i <= n; i++)
    {
        current = penultimate + antepenultimate;
        antepenultimate = penultimate;
        penultimate = current;
    }

    return current;
}

int main()
{
    u_int64_t n{0};
    cout << "Digite n para Fib(n): ";
    cin >> n;
    cout << fibo(n) << endl;

    return 0;
}
```
Note que aqui utilizamos O(1) em complexidade espacial.
