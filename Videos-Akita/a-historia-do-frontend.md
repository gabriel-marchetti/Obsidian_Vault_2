---
tags:
  - videos-akita
---
A história do frontend é muito relacionada com a história da Web. Portanto, diversas ferramentas e questões só fazem sentido se voltarmos para essas épocas. A primeira questão que devemos observar é que digitamos um endereço dentro do navegador por exemplo $\texttt{https://meusite.com.br}$ precisa ser traduzido em um endereço **IP** que é feito por um **DNS** (Domain Name Server). 

O Akita comenta sobre o funcionamento de uma rede através da comunicação com protocolo **TCP/IP**, em que é aberto um socket e algumas decisões são arbitrárias, como qual porta será usada. Um exercício simples de faculdade envolveria conectar a uma porta através de um programa e outro programa deverá escutar essa porta.

Também é explicado como surgiu a World Wide Web ou a Internet. Em que textos são referenciados através de textos por meio de **Hypertext**. Nesse sentido, antigamente eram dados pelo servidores sites estáticos, ou seja, que não se modificam com o tempo, de modo que algumas requisições começaram a requisitar execução de um executável que retornaria algum tipo de texto. Assim, houve a criação da **CGI** (Common Gateway Interface) que era uma interface para programas em C que retornariam um texto HTML. Contudo, pela dificuldade de processamento de strings dentro da linguagem C, então foram usadas outras linguagens, como o **Perl**, por conta das suas **Regular Expressions**. 

Veja que o HTML é uma linguagem de marcação que apresenta apenas o conteúdo das páginas, de modo que a customização de elementos da página poderia ser feita pelo próprio usuário dentro de um navegador. Assim, surgiu o CSS como estilizador de página. Guerra entre **Microsoft** e **Netscape**.

Agora que temos uma parte do processo sendo executado dentro de um servidor, há uma nova possibilidade de oferecer serviços por meio dessa interface Web. Veja que isso se torna ainda mais amplo se utilizarmos banco de dados e diversas tecnologias para integrar os nossos sistemas. 