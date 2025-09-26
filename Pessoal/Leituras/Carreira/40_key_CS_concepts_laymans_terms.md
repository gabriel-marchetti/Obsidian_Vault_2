Link: https://carlcheo.com/compsci

# Coisas que eu não conhecia antes de ler esse artigo:
- Droste Effect.
- Hill Climbing de um ponto de vista mais formal.
- Simulated Annealing de um ponto de vista mais formal.
- Rootkit.
- DDoS significa **Distributed Denial-of-Service**.
- Symmetric and Asymmetric cryptography.

# 1st Concept - Algorithms and Data Structures
1) **Big-O Notation**.
	Aqui o artigo sugere um exemplo muito legal sobre a notação *Big-O* para o dia-a-dia. 
	Exemplo da entrega de correio em tempo constante dada uma quantidade de filmes e o tempo de demora de downloads de filme. A questão fundamental é: A entrega dos correios tem tempo constante, enquanto o download aumento conforme o número de filmes, isto é, $O(1)$ vs $O(n)$.
	**Links:**
	[Big-O Notation (video)](https://www.youtube.com/watch?v=V6mKVRU1evU)
	[Plain English Explanation of Big-O](http://stackoverflow.com/questions/487258/plain-english-explanation-of-big-o)
	[A Beginner's Guide to Big-O Notation](http://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/)
2) **Sorting Algorithms**.
	Ele apenas mostra alguns vídeos e ferramentas que abordam o assunto.
	[15 Sorting Algorithms in 6 Minutes](https://www.youtube.com/watch?v=kPRA0W1kECg&t=63s)
3) **Recursion**.
	Exemplo de recursão: Número da cadeira de um teatro ou cinema. Pergunte para a pessoa na carteira abaixo e incremente em um, caso você esteja na primeira fileira apenas diga que você está na primeira fileira.
	Recursão parece ser o princípio básico do **Droste Effect**.
4) **Big-Data**.
	Não gostei muito do exemplo, foi bem superficial. Compara o vazamento de um cano caseiro e outro industrial. Basicamente, você precisa de abordagens diferentes para lidar com cada um dos casos.
	[Big-Data by TED-Ed](https://www.youtube.com/watch?v=j-0cUmUyb-Y)
	[What is Big-Data and Hadoop](https://www.youtube.com/watch?v=FHVuRxJpiwI)
5) **Data Structures**.
	Array, Tree, Stack, Queue, Graph, Hash Table, Linked List, Heap.
# 2nd Concept - Artificial Intelligence
1) **Greedy Algorithm**.
	Escolha a melhor alternativa momentânea e não se preocupe com os efeitos.
2) **Hill Climbing**.
	Conceito de otimização. 
3) **Simulated Annealing**.
	Conceito de otimização, mas parece mais restritivo. 
4) **Dynamic Programming.**
	Paradigma para soluções de problemas computacionais onde resultados anteriores são armazenados numa *cache*.
	[Dynamic Programming - From Novice to Advanced (TopCoder)](https://www.topcoder.com/thrive/articles/Dynamic%20Programming:%20From%20Novice%20to%20Advanced)
	[Tutorial for Dynamic Programming (CodeChef)](https://www.codechef.com/learn/course/dynamic-programming)
5) **Machine Learning**.
	Analogia: https://www.quora.com/How-do-you-explain-Machine-Learning-and-Data-Mining-to-non-Computer-Science-people/answer/Pararth-Shah
6) **P vs NP Problem**
	Um problema é NP (Non-deterministic polynomial) se sua solução é de fácil checagem, mas sua solução é complexa. Encontrar os dois números que multiplicados resultam em um terceiro número é uma tarefa complexa.
	[Much higher intelligence than Human](https://www.youtube.com/watch?v=aTZyVZBtP70&t=526s)
	[Integer Factorization](https://en.wikipedia.org/wiki/Integer_factorization)
	[List NP-Complete Problems](https://en.wikipedia.org/wiki/List_of_NP-complete_problems)
	[Protein Folding](https://en.wikipedia.org/wiki/Protein_folding)
	[RSA Crypto System](https://en.wikipedia.org/wiki/RSA_cryptosystem)
	[P vs NP Video](https://www.youtube.com/watch?v=YX40hbAHx3s)
	[Wikipedia](https://simple.wikipedia.org/wiki/P_versus_NP_problem)
# 3rd Concept - Computer Architecture and Engineering.
1) How do computers work?
	[Numberphile](https://www.youtube.com/watch?v=lNuPy-r1GuQ)
	[SimpleCPU.com](http://www.simplecpu.com/)
2) Halting Problem.
	[Simple Wikipedia](https://simple.wikipedia.org/wiki/Halting_problem)
	[Numberphile Video](https://www.youtube.com/watch?v=macM_MtS_w4)
**Computer Architecture** e **Computer Engineering** envolvem grandes áreas da computação:
- **Operating Systems**.
- **Compilers**.
[Computer Architecture Wikipedia](https://en.wikipedia.org/wiki/Computer_architecture)
[Computer Engineering](https://en.wikipedia.org/wiki/Computer_engineering)
[Operating Systems](https://en.wikipedia.org/wiki/Operating_system)
[Compiler](https://en.wikipedia.org/wiki/Compiler)

# 4th Concept - Concurrency.
Conceito fundamental para sistemas computacionais modernos. Um sistema deve executar diversos programas simultaneamente. Exemplo da secretária que deve alternar entre tarefas. Além disso, ele aprofunda nesse exemplo falando que a secretária para tudo para atender o celular.
1) **Parallelism**.
2) **Race Conditions**.
3) **Mutual Exclusion (Mutex)**.
	Método Busy-Waiting para lidar com problemas de sincronização de operações.
4) **Semaphore**.
	**Binary Semaphore** and **Counting Semaphore**.
	Aparentemente você consegue atribuir uma prioridade para as tarefas.
5) **Deadlock**
	Exemplo muito legal de relacionamentos.
	**(Boy) Let her approach me first**.
	**(Girl) Let him approach me first.**
	**(No love acquired)**
# 5th Concept - Computer Security.

## Hacking.
1) **Brute-Force Attack**.
	Start Guessing Likely Passwords.
2) **Social Engineering**.
	Tricking Users to giver their personal information.
3) **Security Exploit**.
	Encontre a maneira mais fácil de invadir uma casa.
4) **Trojan Horse**.
	Um ladrão simula ser um encanador. A questão aqui é: Ele fingiu ser útil.
5) **Rootkit**.
	Um ladrão que se finge de chaveiro e adquire acesso à sua casas. No âmbito computacional ele consegue permissão de usuário raiz no seu computador.
6) **Distributed Denial-of-Service Attack(DDoS)**.
	Inundar um site através de supostas requisições de serviço. Exemplo da loja de Livros.
## Cryptography.
1) **Symmetric Cryptography**.
	Dois usuários utilizam exatamente a mesma chave para abrir uma caixa.
2) **Asymmetric Cryptography**.
	**Public Key** vs **Private Key**. Não entendi como isso se resolve muito bem.
	[Diffie-Hellman Key Exchange](https://www.youtube.com/watch?v=3QnD2c4Xovk)

# 6th Concept - Software Development Methodologies.
1) **Waterfall Development**.
	![[Waterfall_model.svg.png|center]]
2) **Agile Development**.
	[Scrum](https://en.wikipedia.org/wiki/Scrum_(software_development))
	[Extreme Programming](https://en.wikipedia.org/wiki/Extreme_programming)
	[Kanban](https://en.wikipedia.org/wiki/Kanban_(development))

Algumas coisas que ele comenta mais como curiosidade:
[Cowboy Coding](https://en.wikipedia.org/wiki/Cowboy_coding)
[Technical Debt](https://en.wikipedia.org/wiki/Technical_debt)

- Objects encapsulam complexidade. Exemplo da lavadora de louça.
- API são como restaurantes e seus menus.

