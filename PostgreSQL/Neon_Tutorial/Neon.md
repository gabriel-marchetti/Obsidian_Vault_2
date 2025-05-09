# Intro do PostgreSQL Databases with PgAdmin For Beginners

Base de Dados podem ser interpretados como um grande arquivo de dados como uma planilha. Note que os dados podem ser adicionados conforme você vá fazendo uma pesquisa. Conforme você vá estendendo o suporte de um aplicativo.
Cada DBMS utiliza de uma linguagem para lidar com os dados. No caso do Postgre ele utiliza o PostgreSQL. 

PostgreSQL suporta tanto SQL(relacional) e JSON(não-relacional) querying.

1) Robust Database in the LAPP Stack.
	LAPP (Linux Apache PostgreSQL PHP) - Muito utilizado em backend para website e webapplications.
2) General-Purpose transaction database.
3) Geospatial Database.
	Suporte para Sistemas de informação geoespacial (GIS).

#### Highlighted Features
- User-Defined Types.
- Table inheritance.
- Sophisticated Locking mechanism.
- Foreign Key referential integrity.
- Views, rules, subquery.
- Nested Transactions.
- Multi-Version Concurrency Control (MVCC).
- Asynchronous Replications.

## Connect PostgreSQL Database Server

### 1) Using PSQL(postgres interactive terminal).

No terminal execute:
```
psql -U postgres
```
### 2) Using PgAdmin.

Dentro do PgAdmin clique com o botão direito em **Servers** -> **Register** -> **Server**.

![[Pasted image 20250403161306.png]]

Dê um nome para o servidor:
![[Pasted image 20250403161359.png]]

E estabeleça uma conexão no servidor.
![[Pasted image 20250403161435.png]]

# Load a Database into PostgreSQL.

OBS: Vamos utilizar a database **dvdrental**.
### 1) Using CLI-interface for postgres

1) Acesse o terminal e digite:
```
psql -U postgres
```
2) Cria a database:
```SQL
CREATE DATABASE dvdrental;
```
OBS: para listar todas as databases dentro do PostgreSQL server podemos digitar "\l"
3) Restore database from .tar file through terminal
```
pg_restore -U postgres -d dvdrental <diretorio-download>
```
4) Dentro do terminal conectado no Postgre Server
```
\c dvdrental
```
e a conexão com o database "dvdrental" será estabelecida.
para avaliar as tabelas dentro da database utilize:
```
\dt
```
![[Pasted image 20250403162423.png]]
### 2) Using PgAdmin.

1)
Acesse **Databases -> Create -> Database**.

![[Pasted image 20250403162538.png]]

