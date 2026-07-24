---
tags:
  - engenharia-de-software
---
Esses estilos arquiteturais geralmente são acompanhados de algum esquema de reutilização. Isto é, raramente iremos desenvolver algo que seja desenvolvido do *scratch*. Desse modo, pensemos em dois tipos de desenvolvimento: o **Desenvolvimento para Reutilização** e o **Desenvolvimento com Reutilização**.

![[Pasted image 20260601145721.png]]

A ideia aqui é que quanto mais uma componente é desenvolvida mais testes ela irá sofrer e, portanto, se tornará uma componente mais robusta. Assim como, há um claro ganho de tempo quando utilizamos ferramentas já desenvolvidas.

# Estilos Arquiteturais:
Eles tentam definir um vocabulário para definir **componentes** e **conectores** entre esses componente, mediante a um conjunto de **restrições**.

Nesse eles facilitam a comunicação e discussão para integrantes de uma equipe.

## Tipos de Estilos Arquiteturais:
- Pipes and Filters.
- Arquitetura Orientada à Objetos.
- Invocação Implícita (Publish/Subscribe).
- Camadas (Layering).
- Repositórios.
- Interpretadores.
- Controle de Processos.
- Model-View-Controller (MVC).
- Cliente-Servidor.
- Chamada Remota de Procedimentos.
- Barramento de Serviços.
- Microsserviços.

## Pipes and Filters:
Processo sequencial em que cada unidade representa uma unidade de processamento.
![[Pasted image 20260601151355.png]]
Exemplo: Pipelines de treinamento de Redes Neurais.
## Invocação Implícita (Publisher/Subscriber):
**Publisher**: Publica mensagens a um conjunto de assinantes por um canal de comunicação, além de definir uma interface. O envio da mensagem só ocorre mediante a inscrição do **Subscriber** no canal.
**Subscriber**: Serviços que assinam/recebem a mensagem.

![[Pasted image 20260601151914.png]]
Exemplos: **RSS**, **Twitter**, **Facebook**, **Instagram**, **RabbitMQ** e **Apache Kafka**.
## Camadas (Layering):
-  Resolver problemas de Acoplamento e Manutenção.
Cada camada irá definir um conjunto específico de serviços que há uma hierarquia entre as diferentes camadas.

![[Pasted image 20260601152316.png]]
 Note que se você fizer uma requisição da Camada 1 para a Camada 3, então estamos ferindo esse padrão de arquitetura.
 Exemplos: **Sistemas Operacionais como o Android**.

 ![[Pasted image 20260601152639.png]]

## Repositórios (Shared Repositories):
![[Pasted image 20260601152721.png]]
Duas aplicações compartilham informações através de um sistema intermediário como um Banco de Dados, XML ou até mesmo um sistema de arquivos.

É um sistema que não é muito utilizado, pois todos os sistemas terão que ser modificados para atender novas demandas disponibilizadas pelo repositório. Ou seja, o componente A e o componente B devem implementar novas funcionalidades.

## Model-View-Controller (MVC):
Muito utilizado dentro de aplicações Web.
**Model**: Modelo de dados e serviços da aplicação.
**View**: Apresentação do Modelo e Interface Gráfica.
**Controlador**: Invocar e sincronizar o modelo com a visualização.

Foi desenvolvida para desenvolver aplicações de Small Talk. 

## Arquitetura Orientada a Serviços (SOA):
![[Pasted image 20260601153556.png]]
o Service Registry serve como Proxy para encontrar os domínios dos Provedores.

Outra ideia da arquitetura orientada a serviços:
![[Pasted image 20260601153803.png]]
Note que o **Service Orchestration** é especialmente importante para funcionamento do sistema.

## Microsserviços:
![[Pasted image 20260601153921.png]]
Veja que os quadradinhos da direita representam unidades computacionais, portanto, podemos escalar cada serviço de modo que cada um deles atenda a uma determinada demanda.

## Representational State Transfer (REST):
![[Pasted image 20260601154201.png]]
REST é muito associado a HTTP, contudo REST é independente do HTTP e pode ser implementado em diversos locais.