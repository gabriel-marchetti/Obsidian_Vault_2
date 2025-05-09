Assim como qualquer probabilidade, a probabilidade condicional se refere a uma probabilidade de um evento ocorrer com o adicional da informação de que outro evento tenha ocorrido. Defina dois eventos $A$ e $B$ de modo que:
$$
Pr(A |B) = Pr_{B} (A) = \frac{Pr(A\cap B)}{Pr(B)}
$$
Veja que essa definição pode ser oralmente entendida como: Dado que o evento B ocorre, qual a probabilidade de A ocorrer. Note que a fórmula matemática grita esse sentido, uma vez que B ocorre, então a única alternativa é se o evento pertencer a $A \cap B$.

Note que a partir daqui surge uma outra definição: Dois eventos A e B são independentes se a probabilidade absoluta é igual à probabilidade condicional, isto é:
$$
Pr(A|B) = Pr(A)
$$
Note que podemos articular que se o evento A tem mesma probabilidade que A dado que B ocorre, então B não teve nenhum papel em diminuir o espaço amostral. Veja que sempre que trabalhamos com probabilidades condicionais estamos tentando reduzir o espaço amostral.

> [!theorem] Independência de variáveis em probabilidades condicionais.
> $$
> Pr(A|B) = Pr(A)
> $$

DESENVOLVIMENTO DE RACIOCÍNIO:
Lembre que uma definição de independência é $Pr(A\cap B) = Pr(A) \cdot Pr(B)$. Portanto, queremos dizer que:
$$
Pr(A|B) = Pr(A) \implies Pr(A\cap B) = Pr(A) \cdot Pr(B)
$$
Só que esse resultado sai de imediato se considerarmos a definição de probabilidade condicional:
$$
Pr(A|B) = \frac{Pr(AB)}{Pr(B)} \xRightarrow{Pr(A|B) = Pr(A)} Pr(A) = \frac{Pr(AB)}{Pr(B)} \implies Pr(B) \cdot Pr(A) = Pr(AB)
$$
---
Note também que nem sempre é verdade que $Pr(A|B) = Pr(B|A)$, pois:
$$
Pr(A|B) = \frac{Pr(AB)}{Pr(B)} \qquad \text{e} \qquad Pr(B|A) = \frac{Pr(AB)}{Pr(A)}
$$
Se $Pr(A) = Pr(B)$, então teremos essa igualdade.

#### Exemplo: Testes Clínicos.
Sabemos que testes clínicos de uma doença podem resultar em condições falsas. Por exemplo, uma checagem de COVID gerar um teste positivo mesmo para uma pessoa que não esteja doente. Portanto, saber a eficácia dos exames é essencial.
Por exemplo, defina os eventos:
$A_{p}$: p obteve resultado positivo no exame.
$D_{p}$: p está com a doença D.

$Pr(A_p|D_p)$ é a probabilidade da pessoa obter um exame positivo dado que está com a doença.
$Pr(D_p|A_p)$ é a probabilidade da pessoa estar doente dado que o exame deu positivo.

Note que temos os seguintes casos:
![[Pasted image 20250421160958.png]]
$$
Pr(A_p|D_p) = \frac{Pr(D_p|A_p) \cdot Pr(A_p)}{Pr(D_p)}
$$
Note que $Pr(A_p|D_p)$ é uma probabilidade que é desejável que seja próxima de um. Afinal, é desejável que todos os casos que tenham doença sejam diagnosticados como positivos. 

### Falácias:

1 - Assumir que $Pr(A|B) \approx Pr(B|A)$.

Pelo teorema de Bayes, temos que:
$$
Pr(A|B) = Pr(B|A) \cdot \frac{Pr(A)}{Pr(B)} \implies \frac{Pr(A|B)}{Pr(B|A)} = \frac{Pr(A)}{Pr(B)}
$$
Portanto, só ocorre $Pr(A|B) \approx Pr(B|A)$, se $Pr(A) \approx Pr(B)$.

2 - Viés da Seleção.
Suponhamos que uma Sequela (S) pode ocorrer de uma Doença (D). Um médico, pode concluir que se várias pessoas buscam sua consulta para buscar uma solução para um problema e elas apresentam a condição $S_D$: Sequela causada por D, então ele indaga que $Pr(S_D)$ é alta. Mas ele está apenas observando o caso em que $Pr(S_D|\text{Foi no médico consultar o problema)}$.
