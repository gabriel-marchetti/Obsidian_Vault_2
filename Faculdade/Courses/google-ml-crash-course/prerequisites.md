# Introdução ao Machine Learning:
Algumas aplicações de Machine Learning variam de: **Prever Clima**, **Estimar Tempo de Viagem**, **Recomendar Músicas**, **Completar Frases Automaticamente**, **Resumir Artigos** e **Gerar imagens**.

**ML**: Treinar um **software** (chamado de **Modelo**) que pode fazer **Previsões** ou **Gerar Conteúdo** a partir de **Dados**.

Por exemplo, suponha que desejamos criar um APP para previsão de Chuvas, então poderíamos introduzir dois métodos de trabalho: **Tradicional** ou **ML**.
**Tradicional)** Envolveria uma modelagem física da atmosfera e da superfície da Terra - Equações de dinâmica de fluídos.
**ML)** Um modelo é alimentado com quantidades enormes de dados meteorológicos até que ele conseguisse identificar os padrões necessários para fazer bons chutes. Após isso, basta que você alimente o modelo com dados atuais para fazer uma previsão.

A questão aqui é: Nem todo sistema de Machine Learning é o mesmo, assim devemos decidir qual modelo devemos utilizar.

## Tipos de sistemas de ML:
Alguns sistemas podem se enquadrar em mais de um dos campos a seguir:
1) Aprendizado Supervisionado.
2) Aprendizado Não-Supervisionado.
3) Aprendizado por Reforço.
4) IA generativa.
A classificação é feita através de características como: Qual o método utilizado para aprendizagem? Qual a finalidade da aplicação?

### Aprendizado Supervisionado:
A partir de dados considerados **corretos** ou **errados**, o modelo gera conexões com os dados que favorecem um dado ser **correto** ou **errado**. O nome de **supervisionado** é devido ao fato de que o modelo deve ser alimentado com dados **previamente validados** por outra entidade (na maioria dos casos humanos).
Muitos problemas são segmentados em **Regressão** e **Classificação**:
**Regressão**) Prevê um valor numérico - milímetros de chuva ocorrerão no dia X, preço futuro de uma casa, horário de chegada de uma viagem.
**Classificação**) Prever probabilidade de algo pertencer a uma categoria - retorna um número que indica se algo pertence ou não a uma categoria - classificar se um e-mail é SPAM ou se uma foto contém um gato - classificação binária ou classificação multi-classe.
# Aprendizado Não-Supervisionado:
Modelos que fazem previsões sobre dados que não possuem resposta correta. Sua maior utilização é identificar padrões significativos entre dados.
Um modelo de aprendizagem não-supervisionada muito conhecido é o **Clustering**
![[Pasted image 20251107114816.png|center]]
Veja que esse problema de clustering é muito parecido com o problema de classificação multi-classe. Contudo, aqui não temos uma classe conhecida, portanto, a diferença entre um modelo de classificação e um modelo de clustering é que os rótulos não são definidos pelo usuário.
![[Pasted image 20251107115030.png|center]]
# Aprendizado por Reforço:
Esses modelos fazem previsões a partir de **Recompensas** ou **Penalidades** com base em ações dentro de um ambiente. Ao final o modelo irá conter uma **Política** que define estratégias para maximizar a recompensa.
Podemos utilizar esse tipo de programa para fazer com que robôs realizem uma determinada tarefa - Exemplo de jogar Xadrez.

# IA Generativa:
Um modelo que cria conteúdo conforme uma entrada de usuário - Aplicações diversas como **Criar imagens**, **Composições Musicais**, **Piadas Exclusivas** e entre outras são atividades que Modelos Generativos podem realizar.z