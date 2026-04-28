---
tags:
  - redes-de-computadores
---
1) O que caracteriza uma arquitetura cliente-servidor? E o que caracteriza uma arquitetura P2P? Dê um exemplo de aplicação para cada caso e cite uma diferença importante entre elas.

**Resposta**: Uma arquitetura cliente-servidor é uma arquitetura em que pelo menos dois hosts estão envolvidos, sendo que um deles deverá fazer requisições para um host, sendo esse o cliente, e outro irá responder às requisições, sendo esse o servidor. Enquanto uma aplicação P2P (peer-to-peer) é uma arquitetura em que qualquer entidade pode requisitar ou oferecer um serviço. Uma aplicação que funciona na arquitetura cliente-servidor são os servidores Web que fornecem os conteúdos para uma página para diversos clientes, enquanto uma aplicação P2P é a transferência de arquivos tipo torrent. Algumas da diferenças que podem ser destacadas são que os servidores geralmente tem IPs estáticos, enquanto os clientes podem ter IPs dinâmicos. Veja que dentro da aplicação P2P os fornecedores de serviços podem ter IPs dinâmicos.

OBS: 
- Adicionar comentário sobre host "always-on" na arquitetura cliente-servidor.
- Autoescalabilidade de modelos P2P

2) Em uma comunicação de rede, quem é o cliente e quem é o servidor? Explique por que essa distinção depende do papel exercido no processo, e não apenas de qual máquina é “mais forte”.

**Resposta**: Em uma comunicação de rede o cliente é o host que faz solicitações para um outro host, enquanto o servidor é o host que responde essas solicitações. Veja que esse funcionamento não implica que o servidor sempre deva ser mais forte que um cliente, contudo servidores com maior carga devem responder diversas requisições e, portanto, tendem a ser mais fortes que seus cliente, pense por exemplo quantas requisições um servidor do youtube deve receber por dia. Desse modo, conseguimos definir quem é o cliente e quem é o servidor pelo papel que eles exercem.

OBS:
- Distinção entre **processo servidor** e **processo cliente** 

3) O que é um protocolo de camada de aplicação? Explique sua função e como ele se relaciona com os serviços oferecidos pela camada de transporte.

**Resposta**: Protocolos dentro da camada de aplicação são protocolos que definem como a mensagem deve ser definida. Desse modo, definem os tipos de mensagem trocadas, a semântica da mensagem e a sintaxe da mensagem. Veja que pela Rede se tratar de um sistema com uma arquitetura em camadas, então obrigatoriamente haverá a passagem de uma mensagem para uma camada inferior, essa é a camada de transporte. Nela podemos utilizar o UDP ou TCP para fazer a transferência, além de que aqui será utilizado um segmento (ou cabeçalho da camada de transporte) que irá comunicar com a camada de transporte do outro extremo da comunicação.

OBS:
- Falar que a interface de comunicação entre a camada de aplicação e a camada de transporte é o **Socket**.
- Explicar porque a escolha entre um dos serviços TCP e UDP é importante.
- O termo para essa ação de adicionar um *header* é conhecida como **Encapsulamento**.

4) O que são aplicações sensíveis à largura de banda e aplicações elásticas? Dê um exemplo de cada tipo e explique como esses perfis influenciam requisitos de rede.

Aplicações sensíveis à largura de banda são aplicações que precisam de uma performance adequada para oferecimento do seu serviço, pense nos serviços de streaming que precisam de uma quantidade de vazão de dados entre os hosts para que a transmissão de um vídeo não seja travada. 
Assim como, aplicações elásticas são aplicações que poderão realizar a sua função independente da quantidade de vazão disponível, ou seja, ela usará a quantidade de vazão disponível. Nesse caso, pense nos serviços de distribuição e compartilhamento de arquivos, você pode baixar um arquivo com 10 Mbps ou 1 Gbps, contudo os dois irão baixar o arquivo.
Veja que cada um desses perfis influenciam requisitos da rede, uma vez que serviços de streaming podem admitir algumas perdas, uma vez que a reconstrução do vídeo a partir dos sinais admite essa taxa. Enquanto outros serviços dependem de serviços mais robustos.

5) Explique por que o HTTP é considerado um protocolo stateless. Em seguida, comente como aplicações Web conseguem manter contexto mesmo sobre esse modelo.

**Resposta**: o HTTP é um protocolo considerado stateless, pois cada requisição é executada de maneira independente, de modo que a requisição e o servidor não guardam informações (ou estados) da requisição. Entretanto, existem mecanismos para garantir estados dentro de requisições HTTP. Isso pode ser feito através de cookie, onde uma requisição HTTP origina um ID para a requisição do usuário e para seguinte requisições pode recuperar esse estado dentro de um servidor backend.

OBS:
- Mostrar que essa decisão torna a quantidade de processamento menor.

6) O que são request messages e response messages em HTTP? Explique a função geral de cada uma e cite exemplos de informações que normalmente aparecem nelas.

**Resposta**: As request messages e response messages são dois tipos de mensagens que são fornecidas dentro do protocolo HTTP, dentro das request messages elas são classificadas como, por exemplo, em mensagens de **GET**, **POST**, **HEAD** e **PUT**, dentro dessas mensagens há um cabeçalho que define o URL da requisição seguida de informações adicionais sobre a requisição específica, além disso há o anexo de uma mensagem que pode ou não estar presente dependendo do tipo de mensagem. Enquanto as response messages são mensagens que carregam também os cabeçalhos e informações adicionais, como a versão do HTTP, seguida de um status para a operação.

7) Para que serve o método POST? Como a funcionalidade do POST pode ser replicada com o GET?

**Resposta**: O comando POST serve para enviar dados de formulários através de requisições HTTP para o servidor. Para conseguir reproduzir um comando de POST através de um GET podemos mandar informações anexadas através do Query String, contudo é limitado para dados do tipo ASCII.

8) Quais são as vantagens e desvantagens de reutilizar a mesma conexão TCP para múltiplas trocas HTTP? Relacione sua resposta a RTT, overhead e desempenho percebido.

**Resposta**: A vantagem de utilizar a mesma conexão TCP para múltiplas trocas HTTP é a questão de que não precisaremos fazer várias chamadas de handshake seguida de várias mensagens de requisição/resposta. Veja que isso é o ponto que diferencia HTTP persistente e não-persistente, dentro do não-persistente qualquer troca HTTP entre cliente e servidor precisa de um tempo de 2 RTT + tempo de envio dos objetos, contudo o HTTP persistente garante que cada envio subsequente ao handshake tenha apenas 1 RTT + tempo de envio dos objetos. Uma desvantagem é que a porta de envio deve permanecer ativa dentro de um cliente e servido, não disponibilizando o recurso para outros clientes.
Veja que essa abordagem diminui o overhead, pois o servidor precisa reduzir bastante a quantidade de processamento de handshake para diversas requisições, além do desempenho ser maior uma vez que o fator 2 RTT é reduzido apenas para RTT

9) O que é RTT e por que ele importa no projeto de aplicações distribuídas?

**Respota**: O RTT é o tempo para que um pacote leva para viajar do cliente até o servidor e depois voltar para o cliente, portanto, envolve todos as latências de processamento, enfileiramento, propagação e emissão dentro da arquitetura da rede. Veja que ele importa para o projeto de aplicações distribuídas, pois ele define um limite de projeto importante. Pense que estamos projetando um sistema crítico para frear um carro dado o acionamento de um sensor, veja que nessa situação o RTT é crítico, portanto, soluções através do paradigma de cliente e servidor não são conveniente, pois um dos problemas é a latência introduzida pelo RTT.

10) Explique, com suas palavras, como os cookies funcionam. Cite ao menos uma vantagem para o servidor e uma desvantagem ou risco para o usuário.

**Resposta**: Os cookies funcionam da seguinte maneira. Dentro do cabeçalho da mensagem HTTP pode haver um campo definindo o número dentro do servidor backend que gerencia os cookies, caso esse número não exista ele pode ser criado, além disso as requisições podem controlar a utilização de cookies. Em suma, com a identificação do cookie podemos criar estados dentro do servidor para que tanto experiências diferentes sejam criadas para o usuário, além de que cookies podem ser armazenados localmente com informações que melhoram o processamento de uma página web, por exemplo. Contudo, uma desvantagem é que os usuários podem acabar expondo diversas informações sensíveis para o proprietário do site.

OBS:
- Poderia comentar sobre a situação de persistência da sessão, que não é possível dentro de protocolo HTTP sem os cookies.
- o banco não guarda o ID, mas sim os estados daquele cookie.
- Um dos riscos é o Session Hijacking que uma pessoa que interceptar o cookie poderá se fazer como você dentro da sessão.

11) O que é um servidor proxy?

**Resposta**: Um proxy atua como intermediário entre um servidor e um cliente. De modo que requisições do cliente serão primeiro encaminhadas a um proxy que trocará mensagens com o servidor original e passará essas informações de volta ao cliente.
Servidores proxy podem melhorar o desempenho através de caching, uma vez que uma requisição pode já estar presente localmente dentro do proxy. Segurança, pois os servidores proxy podem fazer checagens básicas de segurança dentro de uma requisição. 

12) Qual é a diferença entre HTTP e SMTP? Comente os objetivos de cada protocolo e por que não usamos simplesmente HTTP para envio de e-mails

**Respota**: HTTP É um protocolo de "pull", ou seja, um cliente solicita informações de um servidor quando quiser vê-las. Enquanto o SMTP é um protocolo de "push", ou seja, quem envia a mensagem toma a iniciativa de empurrar o conteúdo para o servidor. Além disso, não utilizamos HTTP para envios de e-mail pois isso impossibilita a lógica de usuário e domínio do SMTP onde temos usuário@domínio, portanto, como isso é uma lógica presente em e-mails, esse protocolo já exige isso e não precisa das adequações para HTTP. Além disso, o SMTP é trocado entre servidores de e-mail e, portanto, possui mecanismos para reenvio de e-mails não vistos, uma coisa que não é implementada nativamente através do HTTP.

13) O que é uma CDN e para que ela serve?

**Resposta**: o CDN (Content Delivery Network) é uma série de servidores distribuídas geograficamente, veja que ele serve para redução de latência, uma vez que os servidores ficam mais próximos geograficamente. Não gera sobrecarga dentro do servidor original, além de disponibilidade e redundância. Veja que esse mecanismo é oferecido com auxílio do DNS, pois digitar um endereço irá fazer com que o DNS procure por um servidor CDN próximo de você.

14) Que funções o DNS oferece além da tradução de nomes para endereços IP? Cite pelo menos duas e explique brevemente sua utilidade.

**Resposta**: O DNS oferece como funcionalidades adicionais a distribuição de carga e aliasing para hosts. A primeira funcionalidade oferece um serviço em que podemos encontrar servidores que oferecem o mesmo serviço só que em hosts diferentes, portanto, não há sobrecarga do servidor original. Além disso, um mesmo endereço de host pode possuir diversos identificadores legíveis, uma vez que essa funcionalidade é oferecida pelo DNS.

