CONSTANT - Valor fixo
```VHDL
constant nome_da_constante : tipo := valor;
```
SIGNAL - Meio físico onde os dados podem transitar
```VHDL
signal nome_do_signal : tipo := valor_inicial;
```
VARIABLE - Usado somente em código sequencial
```VHDL
variable nome_da_variable : tipo := valor_inicial;
```
FILE - Para criação de leitura de arquivo - utilizado em simulações.
```VHDL
file nome_do_file: tipo;
```

Exemplo de utilização de sinais:

Flip-Flop JK mestre-escravo:

![[Pasted image 20250330165730.png]]
Note que existem diversas conexões físicas dentro do sistema.

![[Pasted image 20250330165813.png]]
Note que por se tratarem se sinais internos dentro do circuito, podemos fazer:

 