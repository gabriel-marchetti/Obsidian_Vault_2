Após a finalização do capítulo anterior, agora temos um começo de jogo! Apenas colocamos o plano de fundo dentro do jogo.

#### Objetivos Capítulo:
[ ] Animar algumas nuvens para elas se moverem no céu de modo aleatório.
[ ] Animar a abelha para que ela se mova na tela também de modo aleatório.

#### Data Types:
Nessa seção ele comenta sobre o básico dos tipos de variáveis dentro do C++. Desse modo, algumas features como "implicit type conversion" são extremamente limitadas e, portanto, sempre é uma boa prática converter explicitamente. Também é comentado o benefício de usar uma linguagem fortemente tipada, pois reduzimos a quantidade de bugs que irão aparecer.

**User-Defined Types:** Como o nome diz, são tipos definidos pelo usuário. Quando se tratando desses tipos geralmente estamos falando de classes e enumerations. 

Também é comentado o processo de **Inicialização** e **Declaração** de variáveis.

##### Constant:
Se quisermos reforçar que uma variável não seja alterada durante a execução do jogo podemos fazer:
```cpp
const float PI = 3.1415f;
const int NUMBER_OF_ENEMIES_SPAWN = 2000;
```
Em geral para nomear essas variáveis usamos o mecanismo de nomenclatura de variáveis como o NUMBER_OF_ENEMIES_SPAWN e não o padrão camel-case ou outro tipo. Se tentarmos alterar o valor da constante durante a execução do código haverá um erro de compilação.

##### Uniform Initialization:
Foi introduzido dentro do C++ na convenção de 2011. Basicamente, é um padrão de inicialização adotado que pode ser usado para os tipos definidos pelo usuário. A utilidade disso é criar uma interface com alguma API que inicialize um objeto em apenas uma linha.

##### C++ arithmetic and assignment operators:
Aqui também não tem nada de muito novo. Só que comentou de um "Spaceship" operator que eu não sei o que faz. 

### Clouds, Bee and Tree.

Aqui o processo de criação da abelha e da árvore segue o mesmo padrão da criação do SPRITE pro background. Contudo, o processo para criação das nuvens vai ser um pouco diferente. 
- Carregue APENAS UMA vez a textura de nuvem dentro da GPU.
- Crie um vetor para lidar com as múltiplas nuvens.

```cpp
	sf::Texture texture_cloud;
	texture_cloud.loadFromFile("graphics/cloud.png");

	printf("Creation of clouds textures sucessfull.\n");

	std::vector<bool> status_clouds;
	status_clouds.resize(NUMBER_OF_CLOUDS);
	std::vector<float> speed_clouds;
	speed_clouds.resize(NUMBER_OF_CLOUDS);

	std::vector<sf::Sprite> sprite_clouds;
	sprite_clouds.resize(NUMBER_OF_CLOUDS);

	for (int i{ 0 }; i < NUMBER_OF_CLOUDS; ++i)
	{
		sprite_clouds[i].setTexture(texture_cloud);
		sprite_clouds[i].setPosition(0, 250.0f * (float) i);
		status_clouds[i] = false;
		speed_clouds[i] = 0.0f;
		printf("Added cloud sprite at x: %f and y: %f\n", 0.0f, 250.0f * (float) i);
	}
```
Depois disso, precisamos apenas desenhar os SPRITES dentro da tela. Para isso a ordem de execução do draw é importante.
```cpp
window.draw(sprite_background);
for (auto& c_sprite : sprite_clouds)
{
	window.draw(c_sprite);
}
window.draw(sprite_tree);
window.draw(sprite_bee);
```
### The Frame Rate Problem:
Imagine que agora queremos implementar o mecanismo de voo da abelha pela tela. Pense que se a abelha voar a uma taxa de 200 pixels por segundo ela demoraria em torno de 10 segundos para cruzar o horizonte da tela. Isto porque 200 x 10 = 2000 ~ 1920. Mas isso depende do FPS do jogo, pois se o jogo rodar a 5000 fps então teriamos que adicionar 200/5000 em uma coordenada por mudança de tela. Assim precisamos ajustar isso de acordo o jogo roda. 

O Frame Rate de um Jogo é quantas vezes o Loop principal do jogo é executado. Para lidar com os diferentes Frame Rates dos usuários precisamos primeiramente instanciar uma classe do tipo Clock.