# Introdução:

Template pergunta para Gemini corrigir:
Você é um professor de Sistemas Operacionais universitário e deve avaliar minhas respostas. Nesse quesito se prenda ao que a questão pede e seja rigoroso.

#### Exercício 1)
**Pergunta**: Cite quais são as principais funções de um Sistema Operacional.
**Resposta**: As principais funções de um Sistema Operacional envolvem gerenciamento de recursos eficiente, conveniência para utilização do usuário e facilidade de uso.

**Gerenciamento de recursos**: Diversos componentes de um computador podem ser entendidos como recursos (senão todos). A utilização de uma CPU é entendida como um recurso, a utilização de memória é entendida como recurso ou o armazenamento persistente através de um HDD também pode sem entendido como recurso. A questão é: existem métodos eficientes e não eficientes para a utilização. Assim, delegamos a responsabilidade dessas questões para o Sistema Operacional.
**Conveniência de utilização**: Isso envolve o escopo do Sistema Operacional. Por exemplo, um Celular precisa ser feito para aguentar horas em utilização sem uma fonte de alimentação, desse modo o Sistema Operacional deve ser feito pensando nessas questões. Enquanto, um sistema desktop para utilização residencial pode contar com funcionalidades que utilizem mais processamento. Pense nos sistemas Windows que não são utilizados em sistemas móveis, enquanto o uso na cena residencial é bem expressiva.
**Facilidade de uso**: Isso é bem óbvio, afinal todos preferem utilizar um sistema fácil de ser utilizado do que um sistema mais complicado.
$${\color{red} \text{Insatisfatório}}$$
**Pontos a melhorar sobre essa resposta:**
- Abordagem de modo superficial de um sistema operacional. 
- **Conveniência de utilização** e **Facilidade de uso** não estão muito no campo de função, entram mais no campo de design e marketing.
- Faltou comentar sobre atividades como **Gerenciamento de Processos**, **Gerenciamento de Memória Principal**, **Gerenciamento de Arquivos**, **Gerenciamento de Dispositivos I/O**, **Segurança e Proteção** e **Interface de usuário**.

**Resposta**:
As principais funcionalidades de um sistema Operacional envolvem **Gerenciamento de Processos**, **Gerenciamento de Memória Principal**, **Gerenciamento de Memória Persistente**, **Gerenciamento de Dispositivos de I/O**, **Segurança e Proteção** e **Garantia de uma interface para utilização dos recursos do sistema**.
$$\color{green} Satisfatório$$

OBS:
- **Gerenciamento de Processos**: O Sistema Operacional é responsável por criar, escalonar, sincronizar e encerrar processos. Além de gerenciar o tempo de CPU para cada processo.
- **Gerenciamento de Memória Principal**: O Sistema Operacional deve ser encarregado de alocar e desalocar posições de memória, além de garantir que nenhum processo invada a região de memória de outro processo.
- **Gerenciamento de Arquivos**: O Sistema Operacional deve garantir uma interface para gerenciamento de arquivos, criação de arquivos e destruição de arquivos.
- **Gerenciamento de Dispositivos I/O**: O SO abstrai a camada de gerenciamento de dispositivos de entrada e saída através de *Drivers*.
- **Segurança e Proteção**: Controle sobre os processos e seus respectivos escopos de atuação. Além disso, os dispositivos conectados ao computador devem ter como intermediário o SO.


#### Exercício 2)
**Pergunta**: Uma Chamada de Sistema é um dos pontos de entrada para que o Sistema Operacional atenda a uma requisição da aplicação de usuário. Explique o papel de uma Troca de Contexto para possibilitar isso.

**Resposta**: 
Para facilitar o pensamento imagine que estamos trabalhando com um sistema *single-core*, pois algo análogo acontecerá em sistemas *multi-core*. Um processador possui seus registradores que a partir daí conseguimos fazer operações sobre dados. Veja que, nesse contexto, apenas um processo consegue ser manipulado por vez. Desse modo, quando desejamos fazer a concorrência de programas devemos guardar um contexto sobre cada interrupção de processo. De modo que, será possível retornar para o contexto do programa. Veja que uma chamada de sistema irá realizar uma I/O, desse modo podemos utilizar o tempo de ociosidade da CPU para manipular outro processo, veja que armazenar o contexto e, portanto, realizar uma troca de contexto para outro processo é uma atividade que possibilita a concorrência de programas.
$$\color{orange} \text{Mediano. Existem pontos a melhorar}. $$
Primeiramente, devemos entender que uma **Chamada de Sistema** se trata de uma requisição de um processo em modo usuário realizando um pedido para uma atividade que deve ser realizada em modo **kernel**. Para facilitar esse entendimento, vamos pensar em um sistema **single-core**, nele apenas um processo consegue ser realizado por vez. Desse modo, se o processo A está utilizando os recursos do processador, então nenhum outro processo consegue utilizar. Assim, o processo A chega em um ponto da aplicação em que uma atividade em modo **kernel** deve ser realizada, isto pode ser a realização de uma I/O, um pedido de memória e entre outras coisas. Entretanto, ninguém consegue operar sobre o Hardware sem interferência do Sistema Operacional, ou seja, sem a chamada de sistema. Desse modo, devemos passar o controle da CPU para o Sistema Operacional, entretanto, em alguma hora desejamos retornar para a execução do processo A. Veja que é necessário guardar o estado desse processo, isso é, devemos guardar o Program Counter e os registros para voltar ao estado do programa. 
Assim chegamos ao ponto principal da pergunta, o papel da Troca de Contexto. Tal conceito é entendido como a troca do estado de um processo para a realização de outro processo. Note que no exemplo comentado, desejamos passar o controle do processo A para o Sistema Operacional, realizar a requisição do processo A, e depois retornar para o Sistema Operacional. Ou seja, estamos no estado do processo A, realizamos uma troca de contexto para o Sistema Operacional, realizamos a execução da requisição e depois realizamos outra troca de contexto para o processo A. Portanto, a troca de contexto é essencial para a Concorrência de programas.
$$\color{green} \text{Satisfatório}$$

OBS:
- Um erro que eu estava cometendo era pensar que a chamada de sistema realiza um I/O só que é bem mais abrangente. Uma requisição de sistema pode alocar memória para um processo, realizar a requisição de um I/o, criar um processo ou até mesmo obter a hora do sistema.
- Outra questão importante dessa questão é a importância de entender que a **Troca de Contexto** é uma solução para um problema. O problema em sí é a **Chamada de Sistema**.
- A **Chamada de Sistema** é um intermediário para um processo em modo usuário realizar operações em modo kernel.
- **Process Control Block(PCB)**: Estrutura de Dados que possibilita que um estado seja armazenado pelo SO.
#### Exercício 3)
**Pergunta:** Dê exemplos de atividades que podem ser executadas em modo de execução de usuário ou devem ser executadas em modo núcleo (modo kernel ou modo máquina). O que há de diferente entre os dois modos que determinadas atividades podem estar em um, enquanto outras devem estar em outro?

**Resposta**: 
Primeiramente, vamos destacar a diferença entre atividades que podem ser executadas em modo usuário ou devem ser executadas em modo *kernel*. Desse modo, vou destacar as atividades que o sistema consegue realizar em modo *kernel*. Atividades como **Gerenciamento de Processos**, **Gerenciamento de Memória Principal**, **Gerenciamento de Arquivos** e **Gerenciamento de Dispositivos I/O** são as principais atividades que diferenciam o modo usuário para o modo *kernel*. 
Nesse sentido, um programa de usuário não pode criar um outro processo em uma chamada de sistema. Assim como, mesmo em um comando $\texttt{malloc}$ ,que pode ser executado em um código feito pelo usuário, precisa de uma chamada do sistema operacional para oferecimento da memória. Desse modo, atividades como operações aritméticas e lógicas podem ser executadas através de um código de usuário, enquanto o modo *kernel* possui mais privilégios.
Os dois modos existem para abstrair atividades que devem ser gerenciadas pelo SO, imagine que um programa de usuário utiliza os meios computacionais para atingir um objetivo sem interesses computacionais, como o gerenciamento de contas bancárias, nesse sentido deveremos utilizar a criação de processos paras gerenciar as operações bancárias, o gerenciamento de memória para armazenar valores que serão computador ou até mesmo o gerenciamento de I/O para lidar com a entrada dos usuários do banco. Assim, fica clara a importância de uma interface bem definida pelo OS que deixe o mais simples possível para que aplicações diversas utilizem o sistema computacional. Além disso, algumas questões de Segurança podem ser destacadas para delegar responsabilidades para o SO, como o problema de compartilhamento de memória entre processos e a sincronização de processos.
$$\color{cyan} \texttt{Parcialmente Satisfatório}$$

**OBS:**
- Faltou comentar a distinção fundamental da diferença entre o modo *kernel* e o modo *usuário*. Não basta falar que o modo *kernel* possui mais privilégios. Poderia adicionar a questão do *Mode Bit* que distingue fisicamente os dois modos, além disso poderia comentar que a chamada de sistema muda esse bit.
- Também existe um campo de instruções privilegiadas. Instruções que só podem ser executadas quando o *Mode Bit* está ativado. Caso o programa tente executar uma instrução privilegiada estando em modo *usuário* haverá uma exceção do tipo *trap*.
- Atividades como: Executar lógica de aplicativo (navegador ou editor de texto), fazer cálculos em planilha, executar lógica de um jogo é feita através de instruções em modo *usuário*.


#### Exercício 4)
**Pergunta:** 
um sistema tem uma cpu com apenas um core. nesse sistema, queremos executar três processos, p0, p1 e p2, com tempos de execução em modo usuário de 5 ms, 10 ms e 20 ms. na média, cada processo executa uma chamada de sistema a cada 1 ms. o escalonador do sistema operacional atua a cada 10 μs. o tempo médio de uma troca de contexto é de 1 μs. o tempo de tratamento de uma chamada de sistema específica é desprezível. quanto é o tempo relógio total para execução dos três processos nesse sistema? mostre como você chegou até a resposta.

**Resposta**:
A) Uma chamada de sistema ocorre a cada 1 ms.
B) O escalonador de processo é chamado a cada 10 $\micro$s
C) A troca de contexto demora 1 $\micro$s.

Note que o tempo total de execução dos processos é de $P_0 + P_1 + P_2 = 5 \, ms + 10 \, ms + 20 \, ms = 35 \, ms$.
Além disso, temos que a cada 10 $\micro$s há duas trocas de contexto, pois há a troca de contexto processo -> OS -> processo.
Ainda mains, temos que uma chamada de sistema ocorre a cada 1 ms, portanto, temos que também haverá uma troca de contexto processo -> OS -> processo com tempo de tratamento desprezível.

Assim:
$$
\begin{align}
T_T & = 35\,ms +\frac{35\,ms}{10\,\micro s} \cdot 2\,\micro s + \frac{35\,ms}{1\,ms} \cdot 2 \micro s \\
 & = 42,07 \,ms
\end{align}
$$
#### Exercício 5)
**Pergunta**: 
Um processo é uma abstração interna do Sistema Operacional que encapsula diversas informações sobre um programa em execução. Dê exemplos de informações que o Sistema Operacional guarda sobre cada processo em execução.

**Resposta**:
Uma forma de encapsular a abstração de processo é através de uma unidade de computação, ou até mesmo através do nome de *task*, que engloba tanto processos como threads. Existem cinco componente básicas que formam uma unidade de computação (podemos encaixar processo aqui também) **Program Counter**, **Text Section**, **Stack**, **Heap**, **Data Section**. O **Program Counter** armazena a posição de memória da próxima instrução a ser processada. A **Text Section** armazena o código de execução de um programa. A **Stack** é a pilha de programa. **Heap** para operação dinâmica de memória. **Data Section** para armazenamento de variáveis em escopo elevado.
Além disso, o SO utiliza um **PCB**(Program-Control Block) que armazena diversas características do processo e é utilizada, principalmente, para realização da troca de contexto entre processos ou threads. Nesse sentido, elementos como **status do processo**, **Program Counter**, **Estado dos registradores** e **Arquivos abertos** são armazenados pelo PCB.
$$\color{cyan} \texttt{Parcialmente Satisfatório}$$
OBS:
- A **Text Section**, **Data Section**, **Heap** e **Stack** fazem parte do espaço de endereçamento virtual de um processo. O Sistema operacional não armazena diretamente essas informações, isso é o que o programa armazena para posteriormente ser executado. Nesse sentido, o SO administra essas partes quando o programa deve ser executado em memória.
- Não há distinção clara sobre o que **É UM PROCESSO** e o que o **SO SABE SOBRE O PROCESSO**. Devido a essa mesclagem de conceitos a questão se torna confusa.
- Desse modo, para melhoria da questão devemos adicionar que o **PCB** é uma estrutura utilizada para encapsular o conceito de processo em uma unidade de computação. Para isso devemos considerar a **Identificação de um Processo**, **Contexto de Hardware**, **Estado do Processo**, **Informações de Gerenciamento de Memória**, **Informações de Contabilização de utilização de recursos**, **Informações sobre o estado de I/O**.
**Identificação de um processo**:
	**PID (Process ID)**: número de identificação do processo.
	**PPID (Parent Process ID)**: número de identificação do processo pai.
	**UID (User ID)**: número de identificação do usuário do processo.
**Contexto de Hardware**:
	**Program Counter (PC)**.
	**Registradores da CPU**.
**Estado do Processo**:
	Novo, Pronto, Em execução, esperando e terminado.
