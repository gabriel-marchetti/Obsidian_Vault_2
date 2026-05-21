---
tags:
  - HTML
---
Agora vamos observar o que há dentro do $\texttt{body}$ de um arquivo HTML. 

Dentro de um arquivo HTML ele não processa diversos espaços dentro do conteúdo de uma página. O nome disso é "Whitespace Collapse".

Existem alguns elementos que são reconhecidos como "HTML Entities". Você pode invocar eles através do $\texttt{\&<texto>}$ 

Após essa lição, ficamos com o seguinte código disponível:
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="author" content="Gabriel Cunha Marchetti">
        <meta name="description" content="This page contains all the things i am learning how 
        to create as i learn HTML">

        <title>My First Web Page</title>
        <link rel="icon" href="html5.png" type="image/x-icon">
        <link rel="stylesheet" href="main.css" type="text/css">
    </head>

    <body>
        <h1>Hello, World!</h1>        

        <hr>

        <h2>I'm ready to learn HTML</h2>
        <p>This is my first webpage.</p>

        <h3>This should be an subtopic</h3>
        <p>
            Let me tell you how: 
            <br>&nbsp;&nbsp;&nbsp;... I learn about Web dev.
            <br>&nbsp;&nbsp;&nbsp;... I plan out my schedule.
            <br>&nbsp;&nbsp;&nbsp;... I use resources from <abbr title="Mozilla Developer Network">MDN</abbr>.
        </p>
        
        <hr>

        <h2>I'm also planning a vacation.</h2>
        <p>I've been working hard and really <em>need a getaway</em></p>
        <p>I live in Kansas, so i want to visit a beach.</p>

        <!-- TODO: Add more places -->
        <h3>Places i'd like to visit</h3>
        <p>I've heard good things about the Caribbean.</p>
        <p>I've heard good thing about <abbr title="Sao Paulo">SP</abbr></p>
        <p>I've heard good things about:</p>
        <address>
            Margaritaville Island Reserve Riviera Cancún<br>
            Bahia Petempich Puerto Morelos, Mexico<br>
            Colonia Morelos, Mexico 122343
        </address>

        <h3>Places i want to avoid</h3>
        <p>Anywhere cold. <strong>No way!</strong></p>

        <p> 100 &lt; 120 </p>

        <hr>
        &lt;&lt;&lt; &copy; Gabriel Marchetti &gt;&gt;&gt;
    </body>
</html>
```
Veja que adicionamos alguns elementos
- Adicionamos alguns HTML Entities como o $\texttt{\&nbsp;}$ que é um separador. Ou ainda o $\texttt{\&lt;}$, $\texttt{\&gt;}$,$\texttt{\&copy;}$
- O elemento $\texttt{<br>}$ serve para quebrar a linha dentro de um documento HTML. Assim como, o elemento $\texttt{<hr>}$ que desenha uma linha horizontal.
- Também temos o elemento $\texttt{<abbr>}$.
- Os elementos $\texttt{<em>}$, $\texttt{<strong>}$.
- Por fim também adicionamos o elemento $\texttt{<addr>}$ que formata um endereço.