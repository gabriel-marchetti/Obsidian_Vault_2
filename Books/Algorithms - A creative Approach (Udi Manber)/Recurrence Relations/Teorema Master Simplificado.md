Dada uma relação de recorrência $T(n) = a \cdot T(\frac{n}{b}) + c \cdot n^{k}$ onde a e b são constantes inteiras com $a \geq 1$ e $b \geq 2$ e $c, k$ também são constantes positivas. Temos:

$$
T(n) = 
\begin{cases}
O(n^{log_{b}^{a}}), \text{ se } a > b^{k} \\ \\
O(n^{k} \cdot \log(n)), \text{ se } a = b^{k} \\ \\
O(n^{k}), \text{ se } a < b^{k}
\end{cases}
$$
Para demonstrar isso podemos fazer a seguinte argumentação:

Suponha $n = b^{m}$ sem perda de generalidade.
$$
T(b^{m}) = a \cdot T(b^{m-1}) + c \cdot b^{mk}
$$
$$
T(b^{m}) = a \left[ a \cdot T(b^{m-2}) + c \cdot b^{k(m-1)}  \right] + c \cdot b^{mk}
$$
$$
T(b^{m}) = a^{2} \cdot T(b^{m-2}) + ac\cdot b^{k(m-1)} + c \cdot b^{mk}
$$
Se tentarmos expandir mais uma vez, teremos:
$$
T(b^{m}) = a^{2} \left[ a \cdot T(b^{m-3}) + c \cdot b^{k(m-2)} \right] + ac\cdot b^{k(m-1)} + c \cdot b^{mk}
$$
$$
T(b^{m}) = a^{3} \cdot T(b^{m-3}) + a^2c \cdot b^{k(m-2)} + ac\cdot b^{k(m-1)} + c \cdot b^{mk}
$$
Podemos expandir para:
$$
T(b^{m}) = a^{m} \cdot T(b^{m-m}) + a^{m-1} \cdot c \cdot b^{k} + \cdots + a^2 \cdot c \cdot b^{k(m-2)} + a\cdot c\cdot b^{k(m-1)} + c \cdot b^{mk}
$$
Considerando que $T(1) = c$ pois caso seja um outro valor constante, haverá uma diferença apenas de uma constante. Teremos:
$$
\begin{align}
T(b^{m}) & = c \sum_{j=0}^{m} a^{m-j} \cdot b^{kj} \\ \\
T(b^{m}) & = c \cdot a^m \cdot \sum_{j=0}^{m} \left[ \frac{b^k}{a} \right]^{j}
\end{align}
$$
Veja que para o seguinte problema temos três condições:
- $\displaystyle \frac{b^{k}}{a} < 1$

Se essa condição ocorre, então $\displaystyle \sum_{j=0}^{m} \left[ \frac{b^{k}}{a} \right]^{j}$ converge a uma constante seja $\displaystyle \sum_{j=0}^{m} \left[ \frac{b^{k}}{a} \right]^{j} = \alpha$.
$$
T(b^{m}) = c \cdot \alpha \cdot a^{m} \implies T(b^{m}) \in O(a^{m})
$$
Como $n = b^{m} \implies \log_{b} n = m$
$$
\displaystyle T(n) \in O(a^{\log_{b}n}) \implies T(n) \in T(n^{\log_{b} a})
$$
- $\displaystyle \frac{b^{k}}{a} = 1$

Então teremos que:
$$
\begin{align}
T(b^{m}) &= c \cdot a^{m} \cdot \sum_{j=0}^{m} \left[ \frac{b^{k}}{a} \right]^j \\[5pt]
T(b^{m}) &= c \cdot a^{m} \cdot \sum_{j=0}^{m} \left[ 1 \right] \\[10pt]
T(b^{m}) &= c \cdot a^{m} \cdot (m+1) \\[10pt]
T(b^{m}) &= c \cdot a^{m} \cdot m + c \cdot a^{m}
\end{align}
$$
Note que $T(b^{m}) \in O(a^{m} \cdot m)$
Logo $T(n) \in O(n^{\log_{b}a} \cdot \log_{b} n)$, mas note que $\frac{b^{k}}{a} = 1 \implies b^{k} =a \implies \log_{b} b^{k} = \log_{b} a \implies k = \log_{b} a$
Portanto, $T(n) \in O(n^{k} \cdot \log n)$
- $\displaystyle \frac{b^{k}}{a} > 1$

$$
\displaystyle \sum_{j=0}^{m} \left[ \frac{b^{k}}{a} \right]^j 
= \frac{ 1 - \left[ \frac{b^{k}}{a} \right]^{m+1} }{1 - \frac{b^k}{a}}
= \frac{ \frac{a^{m+1} - b^{k(m+1)}}{a^{m+1}} }{ \frac{a - b^{k}}{a} }
= \frac{ a \cdot \left[ a^{m+1} - b^{k(m+1)} \right] }{ (a -b^k) \cdot a^{m+1} }
= \frac{a}{a-b^k} \cdot \frac{a^{m+1} - b^{km} \cdot b^k}{a^{m+1}}
= \frac{a}{a-b^k} \cdot \left[ 1 - \frac{b^k \cdot b^{km}}{a \cdot a^m} \right]
$$
Note que por $a, b, k$ se tratarem de constantes, temos:
$$
\displaystyle \sum_{j=0}^{m} \left[ \frac{b^{k}}{a} \right]^j 
= \alpha - \beta \left[ \frac{b^k}{a} \right]^m
$$
Logo:
$$
T(b^{m}) = c \cdot a^{m} \cdot \left( \alpha - \beta \left[ \frac{b^k}{a} \right]^m \right )
$$
Usando $n = b^{m}$
$$
T(n) 
= c \cdot n^{\log_{b} a} \cdot \left( \alpha - \beta \left[ \frac{b^k}{a} \right]^{\log_{b} n} \right ) 
= c \cdot n^{\log_{b} a} \cdot \left( \alpha - \beta \left[ \frac{n^k}{n^{\log_b a}} \right] \right )
= c \cdot \alpha \cdot n^{\log_{b} a} - c \cdot \beta \cdot n^{k}
$$
Como $k > \log_{b} a$ temos que $T(n) \in O(n^k)$

Desse modo fica demonstrado o [[Teorema Master Simplificado]].

## Visualização:

Note que a recorrência $T(n) = a \cdot T(\frac{n}{b}) + c \cdot n^{k}$

Representa o seguinte problema de divisão e conquista:
![[Teorema_Master_Simplificado.drawio.png]]
Note que a altura dessa árvore será $\log_{b} n + 1$. Dividindo esse problema em duas partes: A divisão e a conquista podemos entender como:
Se a parte da conquista for a parte que é computacionalmente mais cara, então teremos que os nós que possuem $\displaystyle c \cdot \left( \frac{n}{b^j} \right)^{k}$ irão "pesar" computacionalmente. Desse modo o termo de maior ordem que é $n^{k}$, portanto, temos que $T(n) \in O(n^{k})$. Isso ocorre justamente quando reconstituir os subproblemas é mais caro, ou seja, $b^{k} > a \implies k > \log_{b} a$. 
Se a parte de divisão e conquista forem proporcionalmente iguais em termos de complexidade. Então cada linha tem sua relevância, logo, teremos que a parte de divisão e resolução são relevantes para a complexidade do problema, isto é, se $b^k = a$, então $T(n) \in O(n^k \log n)$. 
Caso a parte de divisão seja a mais relevante, então temos que $b^{k} < a$, então $T(n) \in O(n^{\log_{b} a})$.

