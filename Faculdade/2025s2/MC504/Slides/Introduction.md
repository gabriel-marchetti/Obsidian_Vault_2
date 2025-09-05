# Objetivos
[] Descrever a organização geral de sistemas computacionais e apresentar a função de interrupções.
[] Descrever os componentes presentes em um sistema moderno de computadores, multiprocessadores.
[] Ilustrar a transição entre o contexto de *Kernel* e *Usuário*.
[] Discutir como sistemas operacionais são utilizados em diversos contextos.

# O que é um Sistema Operacional:
Um sistema operacional é uma ferramenta desenvolvida para facilitar o uso do *Hardware* de um computador. De modo que, o usuário não precise se preocupar diretamente com atividades que o sistema operacional se encarregue de cumprir. Portanto, o Sistema Operacional atua como intermediário entre *Computer-User* e *Computer-Hardware*.
Dentre as principais atividades que um Sistema Operacional realiza são:
- Execução dos programas de usuário, de modo que a resolução de problemas computacionais pelo usuário sejam mais facilmente desenvolvida.
- Tornar Sistemas Computacionais mais convenientes de serem utilizados.
- Utilizar o *Hardware* de um Computador de modo eficiente, sem tornar o processo mais complexo ao usuário.

# Computer Systems Structure:
Um Sistema Computacional pode ser dividido em **Quatro** grandes partes:
- *Hardware*:
	O *Hardware* consiste justamente dos componentes básicos de um computador.
	Dentro desse contexto podemos incluir *CPU*, *Memory*, *I/O Devices*. Veja que essas ferramentas proporcionam tanto a funcionalidade, quanto implementação de diversas atividades realizadas por um computador.
- *Operating System*:
	O Sistema Operacional é quem deve orquestrar o funcionamento do *Hardware* para diversos usuários e aplicações.
- *Application programs*:
	Uma aplicação define como os recursos fornecidos pelo sistema computacional devem ser utilizados para realizar uma tarefa.
	*Exemplos*: *Word Processor, Compilers, Web Browsers, ...*
- *Users*:
	Podem ser tanto Pessoas, quanto máquinas ou outros computadores.
OBS: Aqui podemos entender como baixo nível vs alto nível.
![[Pasted image 20250903110053.png|center]]
A imagem tenta justamente mostrar como os níveis, idealmente ou conceitualmente, se comunicam.

Desse modo, veja que as principais atividades que um Sistema Operacional deve se preocupar são *Conveniência*, *Ease-of-Use* e *Good Performance*. Pense que essas são as questões aparentes na interface que o usuário vê sobre o computador. Pense que uma pessoa pode optar por utilizar *Windows*, em vez de *Linux*, pois o primeiro sistema tende a ser mais focado para usuários de diversos conhecimentos.
Por conta disso, podemos entender que o foco principal do Sistema Operacional é **Gerenciamento de Recursos**.
A questão aqui é entender o contexto de aplicação:
- Um Sistema Computacional Residencial apresenta certos recursos que um Sistema Computacional Mobile não apresenta. Então, cada contexto apresenta certas convenções que influenciam o *Design* do Sistema Operacional.
Contudo, podemos perceber que mesmo que diversos Sistemas Computacionais apresentem um escopo de aplicações determinado. Alguns sistemas devem apresentar certa flexibilidade conforme a utilização. Na verdade, se pensarmos historicamente, Sistemas Computacionais eram principalmente utilizadas com finalidades militares. Contudo, com o avanço da tecnologia podemos perceber o aumento de contexto em que sistemas computacionais começaram a ser úteis, desse modo Sistemas Operacionais começaram a ser pensados de modo a abranger diversos usuários.
# Kernel de um OS:
Apesar da certa diversidade de Sistemas Computacionais. Há um conceito que permeia todos os sistemas e chamamos isso de **Kernel**;
	**Kernel**: São as partes do sistema que sempre devem rodar para orquestrar uma mínima funcionalidade do sistema.
Se um programa não está contido no **Kernel**, então é um *System Program* ou *Application Program*.
Hoje existe uma região de programas chamadas de **Middleware** que consistem em programas que podem ser substanciais em certas aplicações, principalmente de desenvolvedores, como: *Databases*, *Multimedia*, *Graphics*.

# Overview Computer Structure:
![[Pasted image 20250903111522.png|center]]
A questão aqui interessante que eu quero destacar é que a comunicação é feita através de *buffers* locais para cada controlador. Pense que a comunicação entre periféricos e Sistema Computacional é feita através desses *buffers* e o *controller* é quem manda um sinal para a *CPU* que a tarefa foi concluída, assim há a geração de uma **Interrupção**.

Após a geração de uma **Interrupção** o Sistema Operacional precisa decidir a rotina de tratamento de interrupção, a rotina pode ser identificada com auxílio do *Interrupt Vector*. Isso porque um sistema gerenciado através de interrupções precisa guardar a posição para cada instrução que lida com interrupção.
Dentro desse contexto, temos as *trap*'s ou *exception*'s que são interrupções geradas por erros.
Assim, podemos perceber que os Sistemas Operacionais se tratam de ferramentas *Interrupt Driven*.

Contudo, devemos perceber que um Sistema Operacional deve guardar o contexto em que uma aplicação estava antes de gerenciar a interrupção. Desse modo, podemos guardar os registradores e PC(Program Counter) para prosseguir com a execução depois do tratamento da interrupção. Veja que o tratamento da execução não é uma tarefa trivial, a ponto de que devemos utilizar a *CPU* para determinar como o tratamento da interrupção será feita.
![[Pasted image 20250903112534.png|center]]
# I/O Structure:
Existem dois modos que podemos tratar uma requisição I/O:
- A CPU espera a rotina de tratamento da interrupção acabar.
	Um problema que pode ser visto por esse método é que a *CPU* espera sempre o tratamento da exceção.
	Veja que uma vantagem é a de que apenas uma *Interrupção* é tratada por vez.
- A CPU retorna à execução do programa mesmo que a interrupção não tenha sido tratada.
	Aqui temos a aplicação de um **System Call** e **Device-Status Table**.

# Computer Startup:
A inicialização de um programa é feita através de um **Bootstrap program**, que é carregado no momento em que inicializamos o computador. Geralmente o armazenamento desse programa é feito através de uma **ROM** ou **EPROM** que é conhecida como **Firmware**. Veja que o componente principal desse momento é o carregamento do **Kernel** no computador.

# Storage Structure:
A armazenamento de dados de programa e instruções de programas é feita através de uma memória que chamamos de *Main Memory*. Geralmente possui os atributos de ser:
- *Random Access*.
- *Volatile*.
- Geralmente é feita através de um **DRAM** (Dynamic Random Access Memory).
Uma forma de armazenamento conhecida como *Secondary Memory* é feita através de um componente com alta capacidade de armazenamento não volátil.

Veja que podemos adicionar um *tradeoff* entre formar de armazenamento. Existem tipos de memórias mais rápidos, então podemos aplicar estratégias como **Caching**, que consiste em armazenar dados em uma forma mais rápida de armazenamento para execução mais rápida. Contudo, temos que implementar **Device Drivers** para cada componente nova que o sistema irá utilizar/gerenciar. 

# Exercícios de Revisão:
1) Cite quais são as principais funções de um Sistema Operacional.

2) Uma Chamada de Sistema é um dos pontos de entrada para que o Sistema Operacional atenda a uma requisição da aplicação de usuário. Explique o papel de uma Troca de Contexto para possibilitar isso.

3) Dê exemplos de atividades que podem ser executadas em modo de execução de usuário ou devem ser executadas em modo núcleo (modo kernel ou modo máquina). O que há de diferente entre os dois modos que determinadas atividades podem estar em um, enquanto outras devem estar em outro?

4) Um sistema tem uma CPU com apenas um core. Nesse sistema, queremos executar três processos, P0, P1 e P2, com tempos de execução em modo usuário de 5 ms, 10 ms e 20 ms. Na média, cada processo executa uma chamada de sistema a cada 1 ms. O escalonador do Sistema Operacional atua a cada 10 μs. O tempo médio de uma troca de contexto é de 1 μs. O tempo de tratamento de uma chamada de sistema específica é desprezível. Quanto é o tempo relógio total para execução dos três processos nesse sistema? Mostre como você chegou até a resposta.