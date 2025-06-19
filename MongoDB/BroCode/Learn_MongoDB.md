Dentro dos documentos de um banco de dados Mongo, há o par campo-chave para designar valores a serem salvos.

Prerequisites:
- Some concepts of OOP

MongoDB Compass : GUI interface for our DB.
MongoShell: CLI interface for our DB.

## Configurando dentro do VSCode.
1) Baixe a extensão MongoDB for VSCode.
2) Configure o localhost
3) Com o botão direito podemos abrir o terminal do mongoDB.

## Primeiros Comandos.

Para listar as base de dados que estão dentro do nosso servidor dentro do terminal podemos usar
```shell
show dbs # Show databases
```
Se desejarmos acessar um dos bancos listados podemos simplesmente escrever:
```shell
use nome_do_banco
```
Desse mesmo modo, para criarmos uma base de dados nova podemos simplesmente escrever um nove que não existe dentro do banco que ele cria automaticamente.
Para criar ,dentro desse novo banco de dados, uma coleção podemos escrever:
```shell
db.createCollection("students") # Se o nome desejado for students.
```
Para dropar uma database podemos simplesmente fazer:
```shell
db.dropDatabase() # Dropa a database que estamos.
```
## Inserindo os primeiros dados dentro do banco.
Para inserir um dado dentro de um arquivo precisamos primeiramente criar um banco. Lembre que você pode user o método 'use' para acessar um banco. Depois disso, você pode criar uma Collection através do comando 'createCollection' como mostrado acima. Assim, podemos fazer:
```javascript
db.students.insertOne({
	name: 'Spongebob',
	age: 30,
	gpa: 3.2
})
```
Caso você deseje inserir mais de um documento através de um comando podemos fazer:
```javascript
db.students.insertMany([
	{
		name: 'Patrick',
		age: 38,
		gpa: 1.5
	},
	{
		name: 'Sandy',
		age: 27,
		gpa: 4.0
	},
	{
		name: 'Gary',
		age: 14,
		gpa: 3.9
	}
])
```

## Datatypes
Vamos descobrir sobre os tipos de dados através de uma inserção no nosso banco de dados 'students':
```javascript
db.students.insertOne({
	name : "Larry", // String
	age: 32, // Integer
	gpa: 2.8, // Double
	fullTime: false, // Boolean
	registerDate: new Date(), // Date
	graduationDate: null, // Null (create a placeholder)
	courses: ['Biology', 'Chemistry', 'Calculus'], // Arrays	
	address: {
		street: '123 Fake St.',
		city: 'Bikini Bottom',
		zip: 12345	
	} // Nested documents
})
```

## Sort and Limit:
Para ordenar podemos fazer um 'method chaining'
```javascript
db.students.find().sort({name:1})
```
O parâmetro de name decide se ordenamos em ordem crescente ou decrescente.

Agora, se desejamos limitar o resultado da nossa consulta podemos usar:
```javascript
db.students.find().limit(2)
```
## Find:
Para encontrar todas as pessoas com o nome: 'Spongebob' podemos fazer:
```javascript
db.students.find({name:'Spongebob'})
```
O padrão para executar uma query de find é 
```javascript
db.students.find({query}, {projection})
```
## Update:
Os comandos básico para fazer Update são:
```javascript
db.students.updateOne({filter}, {update})
db.students.updateMany()
```
Por exemplo, se quisermos adicionar a 'Spongebob' o parâmetro fullTime:
```javascript
db.students.updateOne({name:'Spongebob'}, {$set: {fullTime:true}})
```
Note que podemos alterar vários nomes através da consulta, então é mais seguro que você altere por ObjId. 
Também podemos remover campos de objetos através do comando 'unset'.
```javascript
db.students.updateOne({name:'Spongebob'}, {$unset:{fullTime}})
```
Vamos supor que agora desejamos adicionar o campo fullTime para todos os documentos que não possuem esse campo, desse modo podemos fazer:
```javascript
db.students.updateMany({fullTime:{$exists:false}}, {$set:{fullTime:false}})
```
## Delete:
Para deletar documentos dentro do nosso banco dois métodos são principalmente utilizados. 'deleteOne' e o 'deleteMany' o padrão de argumentos é:
```javascript
db.students.deleteOne({filter})
```
Algo como:
```javascript
db.students.deleteMany({registerDate:{$exist:false}})
```
é útil para deletar documentos que não possuem o valor registerDate.

## Comparison Operators:
Se quisermos encontrar todas as pessoas que o nome não é 'Spongebob' podemos fazer:
```javascript
db.students.find({name:{$ne:'Spongebob'}})
```
Utilizando os comparadores maior e menos:
Para encontrar todos os estudantes com idade menor que 20.
```javascript
db.students.find({
	age:{$lt:20}
})
```
Se quisermos combinar dois operadores de comparação podemos fazer:
```javascript
db.students.find({
	gpa: {$gte: 3, $lte: 4}
})
```
também podemos utilizar o operador 'in'
```javascript
db.students.find({
    name:{$in:['Spongebob', 'Gary']}
})
```
também podemos utilizar o operador 'nin' para not in
```javascript
db.students.find({
    name:{$nin:['Spongebob', 'Gary']}
})
```
## Logical Operators:
Existem apenas 4 operadores lógicos: 'and', 'not', 'nor', 'or'
```javascript
db.students.find({
    $and:[{fullTime:true},{age:{$lte:22}}]
})
```
Note que o comando 'not' pode ser útil para encontrar tipos não definidos como no caso:
```javascript
db.students.find({
    age:{$not:{$gte:30}}
})
```
Nesse caso haverá o retorno das idades menores que 30 e null também incluso.

## Indexes:
Index podem ser usados para acelerar a busca dos documentos, contudo torna quase todas as outras operações mais lentas. Então escolha com sabedoria se você deve usá-los
Para criar um índice de um campo podemos simplesmente fazer:
```javascript
db.students.createIndex({field})
```
Para sabermos os indices que estão sendo utilizados no nosso banco podemos fazer:
```javascript
db.students.getIndexes()
```
O resultado de tal consulta é algo como:
```
[
  {
    "v": 2,
    "key": {
      "_id": 1
    },
    "name": "_id_"
  },
  {
    "v": 2,
    "key": {
      "name": 1
    },
    "name": "name_1"
  }
]
```
Veja que o índice possui nome, então para removê-lo podemos fazer:
```javascript
db.students.dropIndex('name_1')
```
## Collections:
Uma collection é um grupo de documentos.
Dentro de um database podemos fazer:
```
show collections
```
para verificar as collections presentes.
Podemos criar uma nova collections através do comando:
```javascript
db.createCollection('teachers',{capped:true, size:10_000_000, max:100})
```