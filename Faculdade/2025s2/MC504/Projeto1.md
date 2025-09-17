# Descrição partes do programa:

## main:
```C
int main(int argc, char *argv[]) {
    shellvis();    

    /* Batch Mode */
    if(argc == 2)
    {
        FILE *f = fopen(argv[1], "r");

        if(!f)
        {
            perror("fopen failed in opening file content");
            return 1;
        }

        shellvis(f);
        fclose(f);
    }
    else if(argc > 2)
    {
        fprintf(stderr, "Uso: %s [batchfile]\n", argv[0]);
        return 1;
    }
    else
    {
        shellvis(stdin);
    }

    return 0;
}
```
o $\texttt{perror(...)}$ é utilizado, pois irá indicar que há um erro na chamada do sistema. Podendo ter mais contexto sobre o erro em sí.
Enquanto o erro indicado por $\texttt{fprintf(...)}$ é utilizado, pois o erro está já na camada do próprio código, quando fornecemos diversos argumentos.

# shell_loop:
```C
void shell_loop(FILE *in) {
    char line[MAX_LINE];
    while (1) {
        if (in == stdin) {
            printf("shellvis> ");
            fflush(stdout);
        }
        if (!fgets(line, sizeof(line), in)) {
            if (in == stdin) printf("\n");
            break;
        }
        /* remover newline */
        line[strcspn(line, "\n")] = '\0';
        /* ignorar linhas vazias e comentários (opcional) */
        char *p = line;
        while (*p == ' ' || *p == '\t') p++;
        if (*p == '\0') continue;
        process_line(p);
    }
}
```
1) A ideia de utilizar o $\texttt{fflush}$ vem da ideia de que alguns terminais podem apresentar o problema de aguardar a aparição de um '\n' para imprimir na tela. Desse modo, essa função garante que o buffer de saída seja impresso na tela. 
	A ideia a ser destacada aqui é: utilize o $\texttt{fflush(stdout)}$ quando é desejado mostrar uma mensagem em tela **sem quebra de linha**.
2) A função $\texttt{char *fgets(char *str, int size, FILE *stream)}$. 
	Lê no máximo $\texttt{size - 1}$ caracteres de $\texttt{stream}$ e os insere em $\texttt{str}$.
	A execução é previamente finalizada (antes dos $\texttt{size-1}$) se é encontrado um $\texttt{\\n}$ ou um $\texttt{EOF}$
	O retorno é um ponteiro para $\texttt{str}$ ou $\texttt{NULL}$.
	Portanto, esse trecho de código lida quando chegamos no final da execução.
3) A função $\texttt{strcspn}$ encontra a primeira ocorrência de um caractere $\texttt{"\\n"}$ e retorna essa posição. Note que esse trecho, portanto, substitui a ocorrência desse caractere para um zero character.

## process_line:


