## Entradas de dados dentro do C#.

```csharp
Console.ReadLine();
```
Lê até a quebra de linha. Retorna os dados na forma de uma string.

### Comando Split
Vamos supor que desejamos digitar dentro do console algo como:
```
batata tomate abacaxi
```
E armazenamos o valor p1 = "batata", p2 = "tomate", p3 = "abacaxi".

```csharp
string s = Console.ReadLine();
string[] vet = s.Split(' ');

// O processo pode ser feito através de:
string[] vet = Console.ReadLine().Split(' ');
```

### Objetivos:
1) Ler um número inteiro.
2) Ler um caractere.
3) Ler um número double.
4) Ler um nome, sexo, idade, altura.

```csharp
int n1 = int.Parse(Console.ReadLine());
char c = char.Parse(Console.ReadLine());
double n2 = double.Parse(Console.ReadLine());

```