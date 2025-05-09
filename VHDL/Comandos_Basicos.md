Existe um conjunto de comandos concorrentes básicos que estão implementados dentro do VHDL.

**Básicos:**
- When-Else
- With-Select
- Block
- Process
- Generate

---
**When-Else**
```VHDL
architecture behavioral of ent is
begin
	signal <= expression_1 when condition_1 else
			  expression_2 when condition_2 else
			  expression_3;
end architecture behavioral;
```
Podemos entender como uma sequência de multiplexadores decidindo o estados da sua aplicação.

![[Pasted image 20250330174235.png]]

Um exemplo de uso é um Multiplexador.
```VHDL
ENTITY MULTIPLEXADOR IS
	PORT(
		D0, D1, D2, D3 : in std_logic;
		S0, S1 : in std_logic;
		Y : out std_logic
	);
END ENTITY MULTIPLEXADOR; 

ARCHITECTURE MAIN OF MULTIPLEXADOR IS
	SIGNAL SEL : std_logic_vector(1 downto 0) := '0';
BEGIN
	SEL <= S1 & S0;

	Y <=
		D0 WHEN SEL = "00" else
		D1 WHEN SEL = "01" else
		D2 WHEN SEL = "10" else
		D3;
END ARCHITECTURE MAIN;
```

Note que se fizermos
```VHDL
Y <=
	EXPRESSION_1 WHEN CONDITION_1 ELSE
	EXPRESSION_2 WHEN CONDITION_2 ELSE
	EXPRESSION_3 WHEN CONDITION_3 ELSE
	EXPRESSION_4 WHEN CONDITION_4
```
Estaremos fazendo um LATCH para quando nenhuma das condições forem atendidas, isto é, Y recebe Y se nenhuma das 4 condições forem satisfeitas. Um modo mais claro de fazer isso, se for sua intenção é:
```VHDL
Y <=
	EXPRESSION_1 WHEN CONDITION_1 ELSE
	EXPRESSION_2 WHEN CONDITION_2 ELSE
	EXPRESSION_3 WHEN CONDITION_3 ELSE
	EXPRESSION_4 WHEN CONDITION_4 ELSE
	UNAFFECTED;
```
![[Pasted image 20250331084003.png]]

---
**WITH-SELECT:**

Um exemplo básico para verificar se apenas um dos botões é clicado com indicação em nível-baixo.
```VHDL
WITH buttons SELECT
	status <=
		'0' WHEN "0001",
		'0' WHEN "0010",
		'0' WHEN "0100",
		'0' WHEN "1000",
		'1' WHEN OTHERS;
```
Isso é equivalente a fazer:
```VHDL
WITH buttons SELECT
	status <=
		'0' WHEN "0001" | "0010" | "0100" | "1000",
		'1' WHEN OTHERS; -- 12 condições não "lidadas".
```
Uma operação interessante para o SELECT seria fazer uma estrutura que lide com operações.
```VHDL
WITH operation SELECT
	result <= 
		a AND b WHEN 0,
		a OR b WHEN 1 to 4,
		a XOR c WHEN 5 | 7,
		NOT a WHEN 6,
		"000" WHEN OTHERS;
```
Esquema de visualização para uma estrutura genérica WITH-SELECT.
![[Pasted image 20250331084930.png]]

EXEMPLO: Modelagem ULA simples;

![[Pasted image 20250331090123.png]]

```VHDL
library ieee;
use ieee.numeric_bit.all;

entity alu_simple is 
    port(
        Ai, Bi  : in unsigned(7 downto 0); -- 8-Bit signal
        S0, S1, M  : in bit;
        Fi  :  out unsigned(7 downto 0)
    );
end entity alu_simple;

architecture main of alu_simple is 
    signal H, G  :  unsigned(7 downto 0);
    signal sel  :  bit_vector(1 downto 0);
begin
    sel <= S1 & S0;

    -- Unidade Aritmética
    with sel select
    G <=
        Ai + Bi when "00",
        Ai - Bi when "01",
        Ai + x"01" when "10", -- x"01" é hexadecimal com 8 bits.
        Ai - x"01" when others;

    -- Unidade Lógica.
    with sel select
    H <=
        Ai AND Bi when "00",
        Ai OR Bi when "01",
        Ai XOR Bi when "10",
        NOT Ai when others;

    -- Unidade de Controle.
    Fi <= G when M = '1' else H;
end architecture main;
```
---
**BLOCK:**

Utilização:
- Organização do Código e Expressões de Guarda.
- Devido a síntese limitada podemos utilizar em simulações.

EXEMPLO: ALU.

![[Pasted image 20250331091138.png]]
A unidade lógica fará parte de um BLOCK, enquanto a unidade Aritmética fará parte de outro BLOCK.

```VHDL
library ieee;
use ieee.numeric_bit.all;

entity alu_simple is 
    port(
        Ai, Bi  : in unsigned(7 downto 0); -- 8-Bit signal
        S0, S1, M  : in bit;
        Fi  :  out unsigned(7 downto 0)
    );
end entity alu_simple;

architecture main of alu_simple is 
    signal H, G  :  unsigned(7 downto 0);
begin

	-- Unidade Aritmética
	arith_unit: block
		signal sel_arith : bit_vector(1 downto 0);
	begin
		sel_arith <= S1 & S0;
		with sel_arith select
		G <=
			Ai + Bi when "00",
			Ai - Bi when "01",
			Ai + x"01" when "10",
			Ai - x"01" when others;
	end block arith_unit;

	--Unidade Lógica
	logic_unit: block
		signal sel_logic : bit_vector(1 downto 0);
	begin
		sel_logic <= S1 & S0;
		with sel_logic select
		H <=
			Ai AND Bi when "00",
			Ai OR Bi when "01",
			Ai XOR Bi when "10",
			NOT Ai when OTHERS;
	end block logic_unit;
	
	-- Saida
	Fi <= G when M = '1' else H;
end architecture main;
```
Agora se quisermos implementar um LATCH com expressão de guarda, podemos fazer:

```VHDL
library ieee;
use ieee.std_logic_1164.all;

entity latch_block is
	port(
		a  :  in std_logic;
		sel  :  in std_logic;
		x  : out std_logic	
	);
end entity latch_block;

architecture main of latch_block is
begin
	driver: block(sel = '1')
	begin
		x <= guarded a; -- Aqui precisa desse guarded para avaliar a condição do sel.
	end block driver;
end architecture main;
```
---
**PROCESS:**
-> Se trata de um dos comandos mais importantes dentro da linguagem.

Utilização:
- Bloco de código SEQUENCIAL.
- Síntese de Circuitos Sequenciais. (São diferentes dos códigos SEQUENCIAIS, aqui introduzimos memória).
- Testbenches. (Simulação dos códigos).

OBS: Podemos executar diversos PROCESS em concorrência, mas dentro do PROCESS haverá a estrutura sequencial.

---
**FOR-GENERATE:**
