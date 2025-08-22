# Line and Line Segments:
$x_1, x_2 \in \mathbb{R}^n$, então:
$$y=\theta \cdot x_1 + (1-\theta)\cdot x_2$$
Define uma reta ou um segmento de reta. O segmento de reta é quando variamos $0 \leq \theta \leq 1$.
Uma outra interpretação desse mesmo conceito de reta é através de:
$$
y = x_2 + \theta(x_1 -x_2)
$$
Onde:
$x_2:$ é um ponto base.
$(x_1-x_2)$: é uma direção.

# Affine Sets:
Um conjunto $C \subseteq R^n$ é afim se dados dois pontos em $C$ temos que a linha desses dois pontos está totalmente contida em $C$. Portanto:
$$x_1,x_2\in C \subseteq\mathbb{R}^n \wedge \theta \in \mathbb{R} \implies \theta \cdot x_1 + (1-\theta) \cdot x_2 \in C$$
Portanto, podemos definir 

**Affine Combination:** 
$$\theta_1 \cdot x_1 + \theta_2 \cdot x_2 + \cdots + \theta_n \cdot x_n, \text{ sujeito a } \theta_1 +\theta_2+\cdots+\theta_n=1$$
**Exercício:** Provar que se $C$ é um conjunto afim, então $C$ contém qualquer combinação afim de seus elementos.

**Relação entre conjuntos afim e espaços vetoriais:** 
$$V = C - x_0 = \{ x-x_0 | x\in C\} \iff V +x_0 = C$$
É possível mostrar que isso forma um espaço vetorial.
**Exercício:** Provar que $V$ define um espaço vetorial. (Para isso basta mostrar que se há dois vetores em $V$, então a combinação linear deles pertence a $V$).

A dimensão de affine set é atrelado à dimensão do subespaço vetorial associado. Portanto, a dimensão do Nullspace(A) é a dimensão do affine set.

**Perguntas:**
- Como mostrar que todo conjunto afim pode ser expresso como um sistema de equações lineares.
- O Subespaço vetorial associado a $C$ é o Nullspace($A$), onde $A$ é a matriz no sistema de equações lineares.

**Affine Hull:**
$$aff(A)=\{\theta_1 \cdot x_1 + \cdots +\theta_n \cdot x_n | x_1,\cdots,x_n \in C \wedge \theta_1 + \cdots+ \theta_n=1\}$$
The affine hull of some set is the smallest affine set that contains C. i.e., $S \text{ affine } \wedge C \subseteq S \implies aff(C) \subseteq S$.

## Affine Dimension and relative interior.
**Affine Dimension:** Dimension of the Affine Hull. (Associado ao espaço vetorial).
Esse conceito é útil em **convex analysis** e **optimization**. 

Se $C \subseteq \mathbb{R}^n$ e a dimensão de $C$ é menor que $n$. Então $aff(C) \neq \mathbb{R}^n$. 
$$relint(C) = \{ x \in C \;|\; B(x,r) \cap aff(C) \subseteq C \}$$
**Pergunta:**
- Eu não entendi como no exemplo 2.2 ele chegou no relative interior.
- O que é um closure de um conjunto?


# Convex Sets.
Um conjunto é convexo se o segmento de linha está completamente dentro do conjunto.
$x_1, x_2 \in C$, então:
$$y=\theta \cdot x_1 + (1-\theta)\cdot x_2 \;\wedge\; 0 \leq \theta \leq 1$$
![[Pasted image 20250819173438.png|center]]
**Combinação Convexa:** 
$$\theta_1 \cdot x_1 + \theta_2 \cdot x_2 + \cdots + \theta_n \cdot x_n, \text{ SUJEITO A: } \theta_1 +\theta_2+\cdots+\theta_n=1 \;\wedge\; \theta_i \geq 0$$
**Exercício:** Mostrar que um conjunto é convexo se, e somente se, contém todas as combinações convexas dos seus pontos.

**Convex Hull:**
$$
conv(C) = \text{Set of all convex combination of a set.}
$$
O mesmo segue de conjuntos afim.
O Convex Hull é o conjunto convexo de menor dimensão que contém o próprio conjunto. Portanto, $B \text{ convexo} \;\wedge\; C \subseteq B \implies conv(C) \subseteq B$.
![[Pasted image 20250819174051.png|center]]
# Cones:
Um conjunto $C$ é um cone se:
$$x \in C \;\wedge\; \theta \geq 0 \implies \theta x \in C$$
**Cone convexo:** é um cone e é convexo. Portanto, dado que $x_1, x_2 \in C$, então $\theta_1 \cdot x_1 + \theta_2 \cdot x_2 \in C, \theta_1 \geq0 \;\wedge\; \theta_2 \geq 0$. Aqui a definição de convexo não exatamente bem enquadrada, pois os $\theta$'s deveriam somar um, só que esse caso está englobado dentro do caso mostrado. Segue uma imagem do cone convexo.
![[Pasted image 20250819174723.png|center]]
**Conic Combination:**
$$\theta_1 \cdot x_1 + \theta_2 \cdot x_2 + \cdots + \theta_n \cdot x_n, \text{ SUJEITO A: } \theta_i \geq 0$$
**Exercício:** Mostre que $C$ é um cone convexo se, e somente se, todas as combinações cônicas de $C$ estão em $C$.

**Conic Hull:** Dado um conjunto $C$, então basta fazer a combinação cônica de todos os elementos de $C$. Também é verdade que a Conic Hull é o menor conjunto cônico que contém a si próprio.

# Hyperplanes

Hyperplanes são definidos por:
$$H = \{ x | a^T x = b\}$$
**Exercício:** Mostrar que um Hyperplane é um Affine Set.

# Halfspaces

$$H = \{ x | a^T x \leq b\}$$

**Exercício:** Mostrar que um Halfspace é convexo, mas não é afim.

# Norm Cone:
Não entendi muito bem a definição disso e o exemplo:
![[Pasted image 20250820110628.png|center]]
# Polyhedra:
OBS: Não entendi muito bem a definição de Affine Indenpendent.



