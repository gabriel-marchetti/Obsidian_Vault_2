C# se trata de uma linguagem pré-compilada que roda através de uma máquina virtual. 

Em C++ você projeta um código fonte, de modo que chamamos o compilador de cada linguagem para converter código fonte em código binário. Cada plataforma possui seu próprio compilador para se adequar ao sistema operacional.

Em linguagens interpretadas usamos o próprio interpretador que recebe como entrada o código fonte e gera um executável. Note que cada plataforma irá possuir seu próprio interpretador. 

**A Abordagem do C#:**
![[Pasted image 20250616100704.png | center]]
Nessa abordagem precisamos apenas nos preocupar em implementar a VM(Virtual Machine). Essa implementação é representada através do CLR(Common Language Runtime).