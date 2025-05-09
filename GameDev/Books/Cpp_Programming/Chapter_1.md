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