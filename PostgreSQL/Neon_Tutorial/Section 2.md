## Where Clause

Nós vimos que a clausula SELECT em [[Section 1]] retorna as linhas de uma Tabela dada a especificação das colunas que desejamos. A clausula WHERE atua de modo a filtrar as linhas que não desejamos.

```SQL
SELECT
	selected_columns
FROM
	table_name
WHERE
	condition
ORDER BY
	sort_expression;
```
a condição precisa ser uma expressão que retorna um booleano. Se você utilizar "aliases" para os elementos definidos no SELECT, eles não podem ser utilizados no WHERE.

A seguinte Query irá listar todos os clientes que possuem o nome 'Jamie'.
```SQL
SELECT
    first_name,
    last_name
FROM
    customer
WHERE
    first_name = 'Jamie';
```
A seguinte Query irá listar todos os clientes que possuem o nome 'Jamie' e sobrenome 'Rice'
```SQL
SELECT
    first_name,
    last_name
FROM
    customer
WHERE
    first_name = 'Jamie'
    AND last_name = 'Rice';
```
OBS: Note que há a utilização do operador AND.

A seguinte Query utilizará o operador "OR" para selecionar pessoas com o primeiro nome 'Jamie' OU sobrenome 'Stewart'
```SQL
SELECT
    first_name,
    last_name
FROM
    customer
WHERE
    first_name = 'Jamie'
    OR last_name = 'Stewart';
```
A seguinte Query utilizará o operador "IN" que verifica a pertinência em um conjunto de valores. 
```SQL
SELECT
    first_name,
    last_name
FROM
    customer
WHERE
    first_name = 'Jamie'
    OR last_name = 'Stewart';
```
A seguinte Query utilizará o operador "LIKE" para verificar expressões similares.
```SQL
SELECT
	first_name,
	last_name
FROM
	customer
WHERE
	first_name LIKE 'Ann%';
```
Nesse caso teremos que o retorno podem ser nomes como "Ann", "Anna", "Annie", "Annette", "Anne".

A seguinte Query utilizará o operador "BETWEEN" e "LIKE" para avaliar as pessoas em que a primeira letra do nome é 'A' e possuem comprimento do nome entre 3 até 5.
```SQL
SELECT
    first_name,
    LENGTH(first_name) AS len_name
FROM
    customer
WHERE
    first_name LIKE 'A%'
    AND LENGTH(first_name) BETWEEN 3 AND 5
ORDER BY
    len_name ASC;
```
Note que dentro do 'WHERE' não utilizamos o len_name, pois 'aliases' não podem ser utilizados dentro do WHERE.

Podemos combinar com o operador '!=' que é o NOT EQUAL por algum motivo... 
```SQL
SELECT
    first_name,
    last_name
FROM
    customer
WHERE
    first_name LIKE 'Bra%'
    AND last_name != 'Motley';
```

## AND

Aqui tem uma coisa relevante para se saber:
O postgres utiliza várias formas de representação do true e false
true -> true, 't', 'true', 'y', 'yes', '1'
false -> false, 'f', 'false', 'n', 'no', '0'
```SQL
SELECT true AND null AS result;   -- result <- null
SELECT false AND false AS result; -- result <- false
SELECT false AND null AS result;  -- result <- false
SELECT null AND false AS result;  -- result <- false
SELECT null AND null AS result;   -- result <- null
```
## OR
```SQL
SELECT true OR null;  -- return true
SELECT false OR null; -- return null
```

## LIMIT

Determina um número máximo de linhas que devem ser retornadas de uma QUERY.
```SQL
SELECT
	columns_names
FROM
	table_name
ORDER BY
	sort_expression
LIMIT
	row_count;
```
A diretiva LIMIT pode ser acompanhada da diretiva OFFSET que determina quantas das linhas iniciais serão puladas. Note que por se tratar de um banco relacional a ordem das linhas não importa de fato, portanto, é importante utilizar um ORDER BY para ter controle tanto sobre LIMIT quanto OFFSET.
```SQL
SELECT
	col_names
FROM
	table_name
ORDER BY
	sort_expression
LIMIT
	row_lim
OFFSET
	rows_to_skip;
```
## FETCH

Dentro do padrão SQL não há definição para a cláusula LIMIT, portanto, dentro do postgres há essa cláusula FETCH para pular uma certa quantidade de linhas.
Vamos lembrar que para essa busca ser conveniente precisamos usar o ORDER BY.
```SQL
OFFSET row_to_skip {ROW | ROWS}
FETCH {FIRST | NEXT} [row_count] {ROW | ROWS} ONLY
```
Essa consulta SQL verifica os dois primeiros filmes ordenados em ordem alfabética.
```SQL
SELECT
    film_id,
    title
FROM
    film
ORDER BY
    title
FETCH FIRST 2 ROW ONLY;
```
OBS: Essa convenção é mais conveniente de ser utilizada, pois segue o padrão SQL.

## IN

```SQL
values IN {value1, value2, value3, ...}
```
Essa cláusula é muito utilizada quando desejamos fazer subqueries.

Essa consulta SQL verifica os nomes dos 'films' com id = 1 ou id = 2 ou id = 3.
```SQL
SELECT
    film_id,
    title
FROM
    film
WHERE
    film_id IN (1, 2, 3);
```
A seguinte consulta SQL busca as pessoas com sobrenome iguais a 'Allen', 'Chase', 'Davis'.
```SQL
SELECT
    first_name,
    last_name
FROM
    actor
WHERE
    last_name IN ('Allen', 'Chase', 'Davis')
ORDER BY 
    last_name;
```

A seguinte consulta avalia os pagamentos que foram feitos em determinadas datas:
```SQL
SELECT
    payment_id,
    amount,
    payment_date
FROM
    payment
WHERE
    payment_date::date IN ('2007-02-15', '2007-02-16');
```
A seguinte consulta SQL deve consultas os gastos entre os dias destacados:
```SQL
SELECT
    payment_date::date AS spend_day,
    SUM(amount) AS total_gastos
FROM
    payment
WHERE
    payment_date::date BETWEEN '2007-02-15' AND '2007-02-20'
GROUP BY
    payment_date::date
ORDER BY
    payment_date::date;
```
Podemos combinar o operador NOT com o IN formando o NOT IN.
Por exemplo como na seguinte consulta SQL
```SQL
SELECT
    film_id,
    title,
    length
FROM
    film
WHERE
    film_id NOT IN (1, 2, 3)
ORDER BY
    film_id;
```

## LIKE

Podemos retornar informações a partir de partes de informação. 
Supondo que você desejasse lembrar o nome completo de uma pessoa, mas você lembra apenas o prefixo 'Jen' do nome da pessoa, então podemos fazer:
```SQL
SELECT
	customer_id,
	first_name,
	last_name
FROM
    customer
WHERE
    first_name LIKE 'Jen%'
ORDER BY
    customer_id;
```
Veja que agora a lista de nome é bem reduzida.
OBS: podemos fazer com o NOT LIKE.
OBS: existem 2 wildcards que podem ser utilizados para pattern matching o '%' ou o '\_'.
	'%': matches any sequence of characters (including empty).
	'\_': matches any singles character.

Um exemplo de uso do '\_' é o seguinte:
```SQL
SELECT
    customer_id,
    first_name,
    last_name
FROM
    customer
WHERE
    first_name LIKE '_her%'
ORDER BY
    customer_id;
```
Os nomes 'Cheryl', 'Theresa', 'Sherry', 'Sherri' são os nomes retornados e veja que o '\_' apenas corresponde a um caracteres.

Existe também a cláusula ILIKE - Insensitive LIKE, não considera o case para match.


