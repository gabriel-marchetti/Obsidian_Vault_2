---
tags:
  - HTML
---
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
        <style>
            html {
                font-size: 22px;
            }
            
            body {
                background-color: #333;
                color: whitesmoke;
            }
        </style>
    </head>

    <body>
        <h1>Hello, World!</h1>        
        <p>This is my first webpage.</p>
    </body>
</html>
```

o código agora possui mais campos dentro do $\texttt{head}$, de modo que adicionamos novos metadados associados e também estabelecemos um link. Além disso, podemos criar um arquivo $\texttt{main.css}$ que conterá o nosso código CSS.
```css
html {
    font-size: 22px;
}
            
body {
    background-color: #333;
    color: whitesmoke;
}
```
Ficando com o seguinte código dentro do HTML:
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
        <p>This is my first webpage.</p>
    </body>
</html>
```