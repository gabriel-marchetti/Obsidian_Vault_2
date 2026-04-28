---
tags:
  - redes-de-computadores
---
Uma página Web consiste em diversos objetos. Geralmente temos um arquivo HTML base e vários objetos referenciados, cada um referenciado por meio de URL.

**HTTP**: 
É um protocolo presente na camada de aplicação da rede que segue o **Paradigma** cliente-servidor.
Uma requisição **HTTP** utiliza um socket para se comunicar com a camada de transporte, assim como utiliza o serviço TCP 

**HTTP não-persistente**:
- Realiza o handshake entre cliente e servidor, depois manda uma mensagem e fecha a conexão.
- RTT: 2 RTT + tempo transferência do objeto.
	Nesse contexto um RTT é para o handshake e outro é para requisição/resposta
**HTTP persistente**: 
- Aqui a conexão não é fechada após o envio da resposta. 

**Mensagens de Requisição HTTP**:
**GET**: Apenas lê os dados do servidor, parâmetros de busco mandados pelo cliente.
**POST**: Enviar dados para o servidor para serem processados. Dados enviados no corpo.
**HEAD**: É idêntico ao GET, mas o servidor apenas responde com o header.
**PUT**: Modificar um recurso já existente.

**Mensagens de Resposta HTTP**:
**200 Ok** 
**404 Not Found**

