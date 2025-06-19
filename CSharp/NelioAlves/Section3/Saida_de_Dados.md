**Comandos:**
```csharp
Console.WriteLine(valor);
Console.Write(valor); // Escrevo sem uma quebra-de-linha.
```
Controlar a precisão do número.
```csharp
Console.WriteLine(saldo.ToString("F2"));
```
Pode haver o problema do seu console mostrar números decimais com vírgula. Podemos fazer a seguinte mudança.
```csharp
using System.Globalization;
Console.WriteLine(saldo.ToString("F4", CultureInfo.InvariantCulture));
```

## Placeholders, concatenação e interpolação.

```csharp
int idade = 32;
double saldo = 10.34651;
string nome = "Maria";

Console.WriteLine("{0} tem {1} anos e tem saldo igual a {2:F2} reais", nome, idade, saldo);

Console.WriteLine($"{nome} tem {idade} anos e tem saldo igual a {saldo:F2} reais");

Console.WriteLine(nome + " tem " + idade + " anos e tem saldo igual a " saldo.ToString("F2", CultureInfo.InvariantCulture) + " reais");
```
