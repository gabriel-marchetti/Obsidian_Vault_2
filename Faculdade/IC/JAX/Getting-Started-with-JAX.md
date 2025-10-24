Link: https://docs.jax.dev/en/latest/notebooks/thinking_in_jax.html

# Objetivos com a leitura:
[] Descobrir como utilizar o ambiente para rodar dentro de uma GPU para maior desempenho.
[] Descobrir como utilizar a função JIT do JAX.
[] Avaliar como funciona a questão de diferenciação automática.
[] Descobrir como criar funções que podem ser automaticamente vetorizadas.


# JAX vs NUMPY
- JAX Arrays podem muitas vezes ser usados para substituir Numpy Arrays.
- Jax Arrays são sempre imutáveis, não é o mesmo dentro do Numpy.

Pelo fato de serem imutáveis, algo que é esperado por um Numpy array como:
```python
x = np.arange(10)
x[0] = 10 

## Output ##
[10  1  2  3  4  5  6  7  8  9]
```
Não pode ser feito.
Contudo, uma interface mais orientada-a-objetos é implementada e podemos fazer essa mesma alteração através de:
```python
y = x.at[0].set(10)
```
OBS: Aqui há a cópia do conteúdo de x.

# JAX arrays:
- Create arrays using JAX API.
- JAX arrays have an attribute called $\texttt{devices}$ which indicates where it is stored.
- JAX arrays can be shared between multiple $\texttt{devices}$.

Existem duas coisas interessantes aqui. Um objeto do tipo jax.Array possui dois atributos diferenciados: $\texttt{devices}$ e $\texttt{sharding}$ que indicam em qual dispositivo o vetor está armazenado. Mais detalhes sobre isso em [[JAX-Introduction-to-parallel-programming]].
```python
x = jnp.arange(10)
isinstance(x, jax.Array) # True
x.devices()
x.sharding
```
# JIT Compilation with jax.jit:
```python
import numpy as np
import jax.numpy as jnp
from jax import jit

def norm(X : jax.Array) -> jax.Array:
	X = X - X.mean(0)
	return X / X.std(0)
	
norm_compiled = jit(norm)

# Para verificar se está correto podemos rodar:
np.random.seed(1701)
X = jnp.array(np.random.rand(10000, 10))
np.allclose(norm(X), norm_compiled(X), atol=1e-6)

# Para fazer benchmark com IPython:
%timeit norm(X).block_until_ready()
%timeit norm_compiled(X).block_until_ready()
```
**OBS**:
  Para o processo de $\texttt{jit}$ funcionar todas as entradas precisam ser de "static shape".
  Esse erro fica explícito em:
```python
def get_negatives(x : jax.Array) -> jax.Array:
	return x[x < 0]

x = jnp.array(np.random.randn(10))
get_negatives(x)

jit(get_negatives)(x)
```
Isso irá gerar um erro, porque os vetores precisam ter estrutura conhecida em tempo de compilação.

# Taking derivatives with jax.grad:

A questão aqui é que podemos usar diferenciação automática dentro do JAX. Para isso podemos fazer:

```python
from jax import grad

def sum_logistic(x):
	return jnp.sum(1.0 / (1.0 + jnp.exp(-x)))
	
x = jnp.arange(3.)
derivative_fn = grad(sum_logistic)
print(derivative_fn(x))
```
Assim como, podemos compor tanto o $\texttt{jax.grad}$ junto do $\texttt{jax.jit}$:
```python
print(jit(grad(jit(grad(sum_logistic)))(1.0))
```
Também existe a função $\texttt{jax.jacobian}$ para computar o Jacobiano da função:
```python
from jax import jacobian
x = jnp.arange(3.)
print(jacobian(jnp.exp)(x))
```
Parece haver um mundo de transformações contempladas dentro do JAX:
- $\texttt{jax.vjp, jax.jvp, jax.linearize}$.
- composition of above functions $\texttt{jax.jacfwd, jax.jacrev}$. 

**OBS**: O que é Forward-Jacobian e Reverse-Jacobian?

# Auto-vectorization with jax.vmap:

$\texttt{jax.vmap}$ significa "Vectorizing Map". O objetivo agora será transformar uma operação de multiplicação entre **matriz x vetor** para uma multiplicação entre **matriz x matriz**. 
Aqui ele entra em bastante detalhe sobre [[Batches]].

