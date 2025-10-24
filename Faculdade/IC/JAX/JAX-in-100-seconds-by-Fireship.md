Link: https://www.youtube.com/watch?v=_0D5lXDjNpw

- XLA - Accelerated Linear Algebra. A grande diferença do JAX para o NUMPY é a limitação do tipo de dados para um dado **immutable** e **pure** para compilar em código de baixo-nível para aplicações em GPUs e TPUs.
- Autograd - Diferenciar funções do python.
- Just-in-Time - escrever uma função dentro do JAX e utilizar funções do JIT converte para instruções simples e primitivas. Essa representação intermediária é conhecida como **JAXPR** que é avaliada como uma mini linguagem funcional que pode ser paralelizada.

- Existe uma biblioteca chamada **FLAX NNX** para construir **Deep Neural Networks**.