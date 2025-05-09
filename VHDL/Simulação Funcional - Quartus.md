Dado um código VHDL podemos rodar ele através de um simulador. Nesse caso, não precisaremos utilizar uma FPGA para realizar o teste do nosso código.

Dicas:
- Defina caminhos sem caracteres especiais
- Defina suas entidades dentro da mesma pasta do projeto.

Observe a hierarquia do seu projeto. Note que o nome do topo da hierarquia será o código VHDL que irá atuar como entrypoint do projeto. Portanto, defina uma entrypoint de modo que seja fácil de utilizar outras entidades definidas.

Podemos fazer simulação com ou sem um test bench. No caso, o test bench atua como um script para definir as diferenças entradas. Contudo, podemos utilizar as próprias ferramentas de excitação do Modelsim para realizar o teste das entidades.

Rodando um arquivo sem ser um testbench dentro do RTL Simulation, teremos uma janela do ModelSim que será aberta. A partir daí, podemos clicar no pacote "work" e ver compilar o teste das nossas entidades.

ModelSim:

![[Quartus_Task.png]]

Ao clicar em RTL Simulation aparecerá um janela do ModelSim.

![[Janela_modelsim_inicial.png]]

Dentro do Painel Library veja que o primeiro pacote se chama work. Ao clicar no "+" ao lado irão aparecer as suas entidades VHDL. 

![[Work_modelsim.png]]

Clique com o Botão direito na sua entidade VHDL e clique em "Simulate". Após isso sua janela irá indicar várias componentes.
![[Exemplo_componentes_modelsim.png]]

Clicando com o botão direito em qualquer um dos sinais. Clique em "Modify -> Apply Wave". Defina o tipo de sinal que você deseja simular e além disso defina os valores. Tome cuidado com a unidade de tempo associada, uma vez que poderá ocorrer problema de visualização. Na próxima janela tome cuidado com os valores das unidades e além disso, defina os valores iniciais.

![[Pasted image 20250330153037.png]]

Após definir as ondas para suas entradas como a imagem a seguir:
![[Pasted image 20250330153311.png]]

Clique com o botão direito nas saídas e apenas coloque "Add Wave". Após isso, basta que você defina um período de simulação e clique em simular.

Caso você queira visualizar o diagrama RTL basta que você acesse dentro do Quartus o "Tools -> Netlist Viewers -> RTL Viewer".

![[Pasted image 20250330153508.png]]

### PROBLEMAS POSSÍVEIS
- Defina o Simulador específico. "Tools -> Options -> EDA Tool Options" : Defina o ModelSim-Altera, por exemplo.

