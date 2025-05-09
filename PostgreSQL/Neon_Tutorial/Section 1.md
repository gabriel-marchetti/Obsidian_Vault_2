# SELECT.
-> É a query com mais adicionais dentro do Postgres. 

- DISTINCT
- ORDER BY
- WHERE
- LIMIT or FETCH
- GROUP BY
- HAVING
- INNER JOIN, LEFT JOIN, FULL OUTER JOIN, CROSS JOIN
- UNION, INTERSECT, EXCEPT

```SQL
SELECT 
	selected_list
FROM
	table_name;
```
selected_list: pode ser tanto uma coluna quando um conjunto de colunas. o "\*" pode ser usado para invocar todas as colunas de uma tabela.
table_name: nome da tabela que você está querendo invocar.

Um exemplo de Query:
```SQL
SELECT
	first_name,
	last_name,
	email
FROM
	customer;
```
Outro exemplo:
```SQL
SELECT * FROM customer;
```
Contudo, precisamos tomar cuidado em utilizar o "\*" em aplicações que serão embarcadas em códigos de outras linguagens como o Python. O problema dessa abordagem é:
-> Performance - uma database com várias colunas pode puxar dados desnecessários.

Podemos fazer concatenações nas nossas consultas SQL, um exemplo dessa aplicação é:
```SQL
SELECT
	first_name || ' ' || last_name,
	email
FROM
	customer;
```
Note que esse esquema não atribui nome à coluna gerada, portanto, podemos fazer:

```SQL
SELECT 
	first_name || ' ' || last_name AS full_name,
	email
FROM
	customer;
```
Podemos utilizar o SELECT para retornar dados de funções, como por exemplo:

```SQL
SELECT NOW();
```

# COLUMN ALIASES

Podemos adicionar aliases para fazer tipos temporários conforme os dados do nosso banco de dados está sendo rodado.
```SQL
SELECT <column_name> AS <alias_name>
FROM <table_name>;
```

Se quisermos utilizar "space" para definir um nome podemos fazer:

```SQL
SELECT
	first_name || ' ' || last_name AS "Full Name",
	email AS "E-MAIL"
FROM
	customer;
```

# ORDER BY
```SQL
SELECT
	selected_list
FROM
	selected_table
ORDER BY
	sort_expression_1 [ASC | DESC]
	sort_expression_2 [ASC | DESC]
	...;	
```

Podemos utilizar o alias para realizar o SORT do problema.
```SQL
SELECT
	last_name || ' ' || first_name AS full_name,
	email
FROM
	customer
ORDER BY
	full_name ASC;
```
Vamos supor que desejamos fazer uma busca de quem possui o maior nome em comprimento:
```SQL
SELECT
	first_name,
	LENGTH(first_name) AS len
FROM
	customer
ORDER BY
	len DESC;
```
Além disso, a secção ORDER BY possui uma maneira de lidar com NULLS.
```SQL
ORDER BY <sort_expression> [ASC | DESC] [NULLS FIRST | NULLS LAST];
```
Vamos criar uma DB para realizar o teste desse comando:
```SQL
CREATE TABLE sort_demo(num INT);

INSERT INTO sort_demo(num)
VALUES
	(1),
	(2),
	(3),
	(null);
```
Fazer a seguinte Query irá me retornar os valores, sendo que o NULL será o primero:

```SQL
SELECT
	num
FROM
	sort_demo
ORDER BY 
	num ASC NULLS FIRST;
```

# SELECT DISTINCT.
Remove duplicatas de linhas dentro de um conjunto de consulta. Por exemplo:
```SQL
SELECT
	DISTINCT <column_1>
FROM
	<table_name>;
```
Podemos fazer algo como:
```SQL
SELECT
	DISTINCT <col_1>, <col_2>
FROM
	<table_name>;
```
Mas isso fará com que o critério de remoção de duplicatas use conjuntamente <col_1> e <col_2> como critério.

Praticando o SELECT DISTINCT:
```SQL
CREATE TABLE colors(
	id SERIAL PRIMARY KEY,
	bcolor VARCHAR,
	fcolor VARCHAR
);
```
```SQL
INSERT INTO
	colors (bcolor, fcolor)
VALUES
	('red', 'red'),
	('red', 'red'),
	('red', NULL),
	(NULL, 'red'),
	(NULL, NULL),
	('green', 'green'),
	('blue', 'blue'),
	('blue', 'blue');
```
```csvtable
source: Tables/select_distinct_table1.csv
```

Se rodarmos o seguinte script SQL:
```SQL
SELECT
	DISTINCT bcolor
FROM
	colors
ORDER BY
	bcolor;
```
```csvtable
source: Tables/select_distinct_table2.csv
```

Mas o código:
```SQL
SELECT
	DISTINCT bcolor, fcolor
FROM
	colors
ORDER BY
	bcolor;
```
```csvtable
source: Tables/select_distinct_table3.csv
```
Note que o resultado não lista as linhas 2, 7 repetidamente. Pois esses valores já estão presentes.

