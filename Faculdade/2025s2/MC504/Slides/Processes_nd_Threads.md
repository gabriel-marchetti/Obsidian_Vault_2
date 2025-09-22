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

O contexto geral que temos é que um programa está armazenada em algum dispositivo de **Armazenamento de Arquivos**. Assim, quando acionamos algum mecanismo de execução de arquivo ,como a execução de algum script no shell ou através do click do mouse, a entidade passará a ser um **processo**. Nesse sentido, ela está alocada em memória e possui as estruturas apresentadas acima. 
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

- Uma regra que pode ser utilizada por SO's é a seguinte: Processos **Parent** só podem ser finalizados se **NÃO** existirem processos **Child**. Essa regra gera o efeito de **Cascading** entre processos. 

# Interprocess Communication.
**Processos** podem ser **Cooperativos** ou **Independentes**. Mas além disso, existem diversas razões para a **Cooperação** entre **Processos**. Elas podem ser **Compartilhamento de informações**, **Computation Speedup**, **Modularity**, **Convenience**. As políticas de **IPC** são **Shared Memory** e **Message Passing**.
![[Pasted image 20250920175226.png|center]]
Um novo paradigma é introduzido aqui: **Producer-Consumer Problem**.
**Unbounded-Buffer**. -> Processos produtores não precisam aguardar a alocação no buffer. Consumidores apenas aguardam quando não há mensagem.
**Bounded-Buffer**. -> Processos produtores e consumidores podem aguardar na alocação/consumo dos dados.

**PROBLEMA**: A questão aqui é que essas questões são orquestradas pelos usuários, então o SO não consegue garantir sincronização.
```C
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/shm.h>
#include <sys/stat.h>
#include <sys/mman.h>
#include <unistd.h>
#include <sys/wait.h>
#include <time.h>

#define BUFFER_SIZE 16
const char *SHM_NAME = "/prodcons_shm";

typedef struct
{
    int id;
} item;

typedef struct 
{
    item buffer[BUFFER_SIZE];
    int in;
    int out;
} SharMem;

int main()
{
    pid_t pid;
    int shm_fd;
    SharMem *sh_data;

    shm_fd = shm_open(SHM_NAME, O_CREAT | O_RDWR, 0666);
    if(shm_fd == -1)
    {
        perror("shm_open");
        return 1;
    }

    if(ftruncate(shm_fd, sizeof(SharMem)) == -1)
    {
        perror("ftruncate");
        return 1;
    }

    sh_data = mmap(0, sizeof(SharMem), PROT_READ | PROT_WRITE, MAP_SHARED, shm_fd, 0);
    if(sh_data == MAP_FAILED)
    {
        perror("mmap");
        return 1;
    }

    sh_data->in = 0;
    sh_data->out = 0;

    pid = fork();
    if(pid < 0)
    {
        perror("fork");
        munmap(sh_data, sizeof(SharMem));
        shm_unlink(SHM_NAME);
        return 1;
    }
    else if(pid > 0)
    {
        printf("[PRODUTOR] Processo Pai (PID: %d) Iniciado\n", getpid());
        srand(time(NULL));

        for(int i=0; i < 20; i++)
        {
            item next_prod;
            next_prod.id = rand() % 1000;

            while((sh_data->in + 1) % BUFFER_SIZE == sh_data->out)
            {
                // Busy-Waiting.
            }

            sh_data->buffer[sh_data->in] = next_prod;
            sh_data->in = (sh_data->in + 1) % BUFFER_SIZE;
            printf("[PRODUTOR] Processo Pai Produziu Item: #%d. Buffer: %d/%d\n", next_prod.id, sh_data->in, sh_data->out);
            usleep(500000);
        }

        wait(NULL);
        printf("[PRODUTOR] Finalizando...\n");

        munmap(sh_data, sizeof(SharMem));
        shm_unlink(SHM_NAME);
        printf("[PRODUTOR] Memória Limpada...\n");
    }
    else
    {
        printf("[CONSUMIDOR] Processo Filho (PID %d) Iniciado\n", getpid());

        for(int i=0; i < 20; i++)
        {
            item next_cons;
            while(sh_data->in == sh_data->out)
            {
                // Busy-Waiting.
            }

            next_cons = sh_data->buffer[sh_data->out];
            sh_data->out = (sh_data->out + 1) % BUFFER_SIZE;

            printf("[CONSUMIDOR] Consumiu Item #%d. Buffer: %d/%d\n", next_cons.id, sh_data->in, sh_data->out);
            usleep(750000);
        }

        printf("[CONSUMIDOR] Finalizado...\n");
        munmap(sh_data, sizeof(SharMem));
    }

    return 0;
}
```
O trecho de código é utilizado para criar um processo **Consumidor** e outro processo **Produtor** através de uma fila de espera e **Busy-Waiting**. 
**OBS:** Adicionar descrição passo-a-passo do processo.
Contudo, aqui criamos uma **Condição de Corrida** como mostrado no seguinte trecho da saída no terminal.
```
[PRODUTOR] Processo Pai (PID: 6291) Iniciado
[CONSUMIDOR] Processo Filho (PID 6292) Iniciado
[CONSUMIDOR] Consumiu Item #511. Buffer: 1/1
[PRODUTOR] Processo Pai Produziu Item: #511. Buffer: 1/0
[PRODUTOR] Processo Pai Produziu Item: #757. Buffer: 2/1
```
Veja que o item 511 foi primeiro consumido e depois produzido. Isso acontece por conta de uma condição de corrida do print. Contudo, nesse método estamos desperdiçando uma posição de memória que nunca será utilizada para justamente garantir a sobreposição dos ponteiros.

**Outro método**:
Podemos fazer esse controle através de uma **Counter** que conta a quantidade de processos na produzidos e os consumidos.
Para isso podemos encapsular a variável counter dentro do campo de **Shared Data**.

```C
typedef struct
{
    int id;
} item;

typedef struct 
{
    item buffer[BUFFER_SIZE];
    int in;
    int out;
    int counter;
} SharMem;
```
E o controle é feito através desse **Counter**. Contudo aqui ainda pode ocorrer uma **Condição de Corrida**.

# Interprocess Communication - Message Passing.
