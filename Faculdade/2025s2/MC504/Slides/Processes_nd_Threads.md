# Questões levantadas pelas questões sobre processos e threads:
[] Quais informações o SO armazena sobre a execução de cada processo?
[] Quais informações são compartilhadas entre processos quando criamos diversas Threads?
[] Quais informações são replicadas e armazenadas individualmente em cada Thread?
[] Quais informações são armazenadas em cada uma das situações descritas acima?
[] Fazer o esboço de um código C que realiza a tarefa de iniciar um novo programa no shell.
[] É viável e aconselhável a implementação do shell através de threads?
[] Implementação de uma rotina de multiplicação de matrizes através de Threads.
# Slides Professor:
Tópicos abordados:
- Conceito de Processo.
- Escalonamento de Processos.
- Operações sobre Processos.
- Interprocess Communication.
- IPC in Shared-Memory Systems.
- IPC in Message-Passing Systems.
- Exemplos de sistemas IPC.
- Comunicação em sistemas client-server.

# Conceito de Processo:
Um processo é uma unidade de computação que executa de maneira sequencial. É composto por:
- **Text Section** : Parte onde o código está localizado.
- **Program Counter** : Apontador para a instrução que será executada.
- **Stack** : Contém dados temporários.
- **Heap** : Contém memória dinamicamente alocada em tempo de execução.
- **Data Section** : Contém variáveis globais.

O contexto geral que temos é que um programa está armazenada em algum dispositivo de **Armazenamento de Arquivos**. Assim, quando acionamos algum mecanismo de execução de arquivo ,como a execução de algum script no shell ou através do click do mouse, então a entidade passa a ser um **processo**. Nesse sentido, ela está alocada em memória e possui as estruturas apresentadas acima. 
Pense que essa relação pode ser de um para muitos, pois um programa pode originar diversos processos. Pense em um programa de consulta de banco de dados com diversos usuários.
![[Pasted image 20250916163346.png|center]]
Desse modo, podemos gerar um esquema de conversão de um código C para uma estrutura como a apresentada acima.
![[Pasted image 20250916163538.png|center]]
Além disso, processos ficam oscilando entre 5 estados diferentes que são apresentados em:
![[Pasted image 20250916163613.png|center]]
#### Process Control Block (PCB).
São informações armazenadas pelo SO para gerenciar os processos.
![[Pasted image 20250916163706.png|center]]
Devemos nos atentar que essa estrutura deve ser altera quando introduzirmos **Threads**, pois a adição de diversas **Threads** pode implicar em mais de um **Program Counter** por programa.
Dentro de alguma versão da implementação do *kernel* do **Linux** havia a seguinte implementação para um processo através da estrutura $\texttt{task\_struct}$ o nome **task** é justamente utilizado para mesclar com o conceito de **Threads**. Nesse sentido, veja que o processo de escalonamento agora se torna o gerenciamento de unidades de execução.
```C
pid t_pid;                   /* process identifier */
long state;                  /* state of the process */
unsigned int time_slice      /* scheduling information */
struct task_struct *parent;  /* this process’s parent */
struct list_head children;   /* this process’s children */
struct files_struct *files;  /* list of open files */
struct mm_struct *mm;        /* address space of this process */
```
#### Process Scheduling.
O escalonador de processos deve selecionar os processos de modo a maximizar o tempo de utilização da CPU. Desse modo, ele deve armazenar duas filas para armazenar os processos *Ready* e *Waiting*.
![[Pasted image 20250916165032.png|center]]
Uma **representação** do escalonador de processos pode ser feita através de:
![[Pasted image 20250916165325.png|center]]
Um SO altera entre processos constantemente. Nesse caso, ocorrerá uma troca de contexto.
![[Pasted image 20250917101752.png|center]]
Quando há uma troca de contexto requisitada pela **CPU** devemos **Armazenar o Processo em execução**, isto é, guardar seus dados através em um **PCB**. **Troco o contexto para outro processo**, isto é, carrego o **PCB** de outro processo na **CPU**.
Entretanto, esse processo não é interessante no contexto do usuário, isto é, só introduzimos overhead.
Além disso, quanto mais complexa é a representação de um contexto dentro de uma **CPU**, mais tempo demoramos para realizar essa troca de contexto. Portanto, essa unidade deve ser implementadas o mais simples possível.

### Operations on Processes.
#### Process Creation:
A requisição de criação de um processo é feita através de outro processo. Desse modo, temos uma relação de **Parent Process** e **Child Process**, assim como há a criação de uma **Tree of Processes**.
Para diferenciar entre processos utilizamos **PID** (process id's).
![[Pasted image 20250917103852.png|center]]

**Compartilhamento de Recursos**:
- Compartilhamento completo dos processos de **Parent Process** e **Child Process**.
- **Child Process** compartilha parte dos recursos do **Parent Process**.
- **Child** e **Parent** não compartilham recursos.
**Opções de execução:**
- **Parent** e **Child** executam de modo concorrente.
- **Parent** espera o término da atividade de **Child**.
**Espaço de endereçamento**:
- **Child Process** duplica o espaço do **Parent Process**.
- **Child Process** carrega o próprio programa.

**UNIX:**
- $\texttt{fork()}$
- $\texttt{exec()}$
- $\texttt{wait()}$
![[Pasted image 20250917103837.png|center]]
Segue um trecho de código que apresenta conceitualmente como funciona esse processo:
```C
#include <sys/types.h>
#include <sys/wait.h>
#include <stdio.h>
#include <unistd.h>

int main()
{
    pid_t pid;
    pid = fork();

    if(pid < 0)
    {
        fprintf(stderr, "Fork Failed");
        return 1;
    }
    else if(pid == 0)
    {
        execlp("/bin/ls", "ls", NULL);
    }
    else 
    {
        wait(NULL);
        printf("Child Complete\n");
    }
    
    return 0;
}
```
OBS:
- Nos slides do professor não tinha a inclusão do cabeçalho de wait, isto é, $\texttt{\#include <sys/wait.h>}$
A execução que está ocorrendo aqui é:
1) Pai executa o $\texttt{fork()}$ e faz uma cópia de si mesmo.
2) Filho carrega o código desejado.
3) Pai espera que o filho seja executado.
![[Pasted image 20250917110237.png|center|500x]]
O $\texttt{fork()}$ para o:
**Pai)** retornará o **PID** do processo do filho.
**Filho)** retornará 0 caso a função seja bem sucedida.
#### Process Termination:
Um processo realiza sua última operação e indica ao sistema operacional o final da sua execução através do $\texttt{exit()}$. O processo filho realiza a execução da função $\texttt{exit()}$ e o processo pai irá receber o status do processo filho através da chamada da função $\texttt{wait()}$. Assim, o recursos do processo filho são desalocados do sistema.
Contudo, a chamada da função $\texttt{exit()}$ pelo filho já realiza boa parte da liberação de recursos, entretanto o SO armazena uma **entrada mínima na tabela de processos** do sistema. Essa **entrada mínima** armazena o **PID** do processo filho, **status de terminação** e **algumas métricas de uso de recursos**.
Nesse estado, o filho se torna um **processo zumbi** que está aguardando a chamada da função $\texttt{wait()}$ pelo processo pai.

Processos Pai podem acabar com a execução de um processo filho utilizando a função $\texttt{abort()}$. As razões para isso são:
- O processo filho está utilizando muitos recursos.
- Tarefa delegada para o processo filho não é mais necessária.
- O processo pai executa sua função $\texttt{exit()}$ e precisa que todos os processos filhos acabem para finalizar sua execução. (**cascading termination**).
Conceito de processos orphan e zombie:
**Zombie Process**: Processo invoca a função $\texttt{exit()}$, mas seu pai ainda não invocou a função $\texttt{wait()}$.
**Orphan Process**: Processo invoca a função $\texttt{exit()}$, mas seu pai já está em status de terminated.

