Até o final do Capítulo você deverá ser capaz de:
-[ ] Find out about the games we will build.
-[ ] Learn a bit about C++
-[ ] Explore SFML and its relationship with C++
-[ ] Look at the Visual Studio software
-[ ] Set up a game development environment
-[ ] Create a project template for reusing it in the future
-[ ] Plan and prepare the first Project (Timber)
-[ ] Write a executable in C++ that draws background

## Projects
#### Timber:
Clone of the Timberman game. 

![[0c0cc60c-5b90-4f1e-8d7c-68bf07c8687fss_3ac16eb48edf0f019caec63ea6234d4c123cf5db.webp|center|420x300]]

#### Zombie Arena:
Clone of Over 9000 Zombies game.
![[maxresdefault.jpg|center|420x300]]
#### Thomas was Late:
Clone of Thomas was Alone game.
![[e6bc549454e71e0e0e2146d237a4cc1a3bc706393d9557b725c88a69e2d1f3d8.avif|center|420x300]]

## Why C++?
-> Very-Fast Language.

Why is it fast? Because it generate a code that translates pretty close to machine executable. To make this possible it makes a **Pre-Processing** Phase in which dependencies are resolved, The process of **Object-Files** and the **Linking** Phase.
It is a **OOP language** (Object-Oriented Programming). This will increase reusability and organization which is necessary to easy things.

## SFML:
Simple Fast Media Library (SFML) is a easy-to-use library for media. It uses **OOP** approach to handle it's entities, so it is easier to work. It focuses on developing 2D games, which some pretty well known and developed games use, this means that the library is not a bottle-neck for your skills. It uses OpenGL under the hood for processing the Graphics of the videogame, so when you are using SFML implies that you are using OpenGL as well.

## Setting up your environment.
- Instale o SFML 
- Instale o Visual Studio

Após selecionar um nome e um local para seu projeto dentro do Visual Studio você deve indicar os "headers" do SFML dentro do Visual Studio. Para isso selecione a "aba" Projeto -> <nome_projeto> Propriedades.
- Primeiro: C/C++ -> Geral -> Diretórios de Inclusão Adicional. Adicione o caminho para o SFML (include).
- Segundo: Vinculador -> Diretórios de Bibliotecas Adicionais. Adicione o caminho para o SFML (lib). 
- Terceiro: Vinculador -> Entrada -> Adicione as dependências adicionais
```
sfml-graphics-d.lib;sfml-window-d.lib;sfml-syst
em-d.lib;sfml-network-d.lib;sfml-audio-d.lib;
```
Agora vamos criar um Template para que não tenhamos que fazer esse processo novamente.
Projeto -> Exportar Modelo 

### Opening a project Template.

Na aba de criação de projetos o Template HelloSFML agora deve aparecer como padrão.

# Começando a falar sobre o jogo:
Como dito anteriormente o primeiro projeto que será desenvolvido é o Timber. Algumas mecânicas que temos que nos atentar no jogo são:
- Tempo sempre está andando
- Você ganhar pontos e tempo ao cortar um tronco.
- Cortar a árvore faz com que os galhos caiam.
- Se o Jogador encostar nos galhos ele perderá.
- Se o Jogador ficar sem tempo ele também perderá.


![[Pasted image 20250529212455.png | center]]

Uma ilustração do jogo pode ser visualizada na figura acima.

#### Controles
- O jogador corta o tronco com as teclas de direção (<- ou ->) para indicar para qual lado ele vai se mover e consequentemente cortar o tronco.

# Game Assets:
FreeSound é um site para utilizar sons grátis sem propósito comercial.
BFXR - é um software que pode nos ajudar a criar os sons.

# Coordinates

![[Pasted image 20250529212706.png | center]]
A seguinte imagem nos mostra a orientação de pixels dentro da nossa tela. Contudo, cada objeto possui seu próprio sistema de coordenadas. Portanto, podemos ter em um objeto algo como:

![[Pasted image 20250529212802.png | center]]
Note que dependendo da escolha de referência dentro da imagem podemos criar situações confusas como a de colocar o objeto no "centro" da image provoca essa sensação dele estar um pouco deslocado para direita.
Objetos Visuais 2D dentro de jogos são conhecidos como Sprites.

## Programação:

Toda linha que termina com um ';' é um statement dentro do C++.

Abrir um janela dentro do SFML:
- Incluir o cabeçalho de SFML/Graphics.hpp
- Instanciar sf::VideoMode
- Instanciar sf::RenderWindow

Note que dentro do SFML invocamos duas classes. Essas classes possui toda sua complexidade já implementada para que nós possamos utilizar sem muitos problemas. Além disso, dentro do C++ toda classe está contida em um 'namespace'. O namespace é utilizado para distinguir entre classes de diferentes contextos, vamos supor que você faça uma aplicação para um zoológico, podemos ter tanto a classe de controle do Mouse do seu computador como também podemos ter uma classe Mouse se referindo a algum rato dentro do Zoológico.

O código:
```cpp
sf::VideoMode vm(1920, 1080);
sf::RenderWindow window(vm, "Timber", Style::Fullscreen);
```
Em VideoMode definimos a resolução da tela do jogador. Enquanto dentro de RenderWindow estamos invocando qual resolução desejamos renderizar, além de um título e o estilo que a janela será aberta.


## Game Loop
```cpp
#include <SFML/Graphics.hpp>

int main()
{
	sf::VideoMode vm(1920, 1080);

	sf::RenderWindow window(vm, "Timber", sf::Style::Fullscreen);
	
	while (window.isOpen())
	{
		if (sf::Keyboard::isKeyPressed(sf::Keyboard::Escape))
		{
			window.close();
		}
	}
}
```
Adicionando novas linhas dentro do nosso código podemos ver que adicionamos um loop dentro do jogo. Veja que para sair do jogo precisamos clicar 'Esc' e caso não façamos isso continuamos dentro dele.

Apesar de parecer bobo esse código será o corpo de qualquer jogo desenvolvido. Contudo, dentro desse código temos um 'pipeline' comum para etapas do jogo.
1) Avaliamos as entradas do jogador.
2) Update dentro do jogo (AI, física ou player input).
3) Desenhamos a cena.
4) Repetimos o processo.

Esse ciclo é conhecido como Input, Update, Draw, Repeat (IUDR). 

Dentro do código podemos adicionar alguns comandos dentro da seção DRAW.
```cpp
#include <SFML/Graphics.hpp>

int main()
{
	sf::VideoMode vm(1920, 1080);

	sf::RenderWindow window(vm, "Timber", sf::Style::Fullscreen);
	
	while (window.isOpen())
	{
		if (sf::Keyboard::isKeyPressed(sf::Keyboard::Escape))
		{
			window.close();
		}

		// DRAW
		window.clear();
		// Aqui iremos desenhar os sprites
		window.display();
	}
}
```
Apesar do nome window.clear() aparentar limpar a tela de display na verdade não mexemos no que o jogador está vendo. Apenas limpamos a janela para a renderização da próxima imagem. Veja que entre o clear() e o display() estamos desenhando os sprites. Esse processo é utilizado para que o jogador não veja o processo de geração da cena. Apenas mostramos a cena quando ela está pronta para ser mostrada. 
Você pode até experienciar isso, quando estamos jogando um jogo travado a tela é congelada, mesmo que o jogo ainda esteja rodando, isso ocorre porque ele ainda não terminou de rodar o código para mostrar a próxima imagem.

O processo de esperar o processamento da imagem é reconhecido como **double buffering** e essa técnica evita o **tearing**. 

Agora precisamos invocar o mecanismo para desenhar dentro da Tela.

Para isso podemos utilizar as classes **Sprite** e **Texture** implementadas pelo SFML. Uma "Texture" é um graphic armazenado dentro da GPU.
A dependência de classe fica:
Um SPRITE precisa de uma TEXTURE para ser mostrada na tela. 
Desse modo as etapas que precisamos fazer são:
1) Instanciar um objeto do tipo Texture.
2) Carregar o conteúdo da imagem dentro da textura.
3) Instanciar um objeto do tipo Sprite.
4) Configurar que o Sprite receba a texture.
5) Escolher a posição de renderização do sprite.

Esse processo deve ocorrer **FORA** do loop de jogo. Pense que esse processo todo só está redirecionando o conteúdo que deve ser processado pela placa gráfica na memória da placa gráfica. Esse processo é **LENTO** e, portanto, desejamos fazer isso apenas uma vez. Isso é, não queremos ter que ficar lidando com as TEXTURE's dentro do loop de jogo.

Pense que a associação entre SPRITE e TEXTURE faz a comunicação para a CPU onde devemos renderizar a texture. Portanto, lidar com a lógica e componentes do ambiente que o SPRITE participa é feito pela CPU, enquanto a parte de "pintar" a cena do jogo será feita pela GPU. 

Os pontos principais que devem ser compreendidos aqui são:
- O processo de transferir uma Texture para a GPU é um processo lento.
- Contudo, estando na memória da GPU você consegue acessar a texture rapidamente.
- Um SPRITE precisa de uma TEXTURE. 
- Controlamos a lógica de jogo sobre o SPRITE.
- Invocamos o método de desenhar dentro de WINDOW para desenhar o SPRITE.

