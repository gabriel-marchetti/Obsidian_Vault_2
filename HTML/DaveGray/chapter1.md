---
tags:
  - HTML
---
A primeira tag que é comentada dentro do vídeo é 
```html
<html>

</html>
```
Depois disso há uma tag que contém metadados sobre a páginas, que é a head
```html
<html>
	<head>
	
	</head>
</html>
```
Agora iremos colocar o elemento que define os elementos que serão dispostos na página.
```html
<html>
	<head>
	
	</head>
	<body>
	
	</body>
</html>
```

Dessa maneira criamos a primeira página através do HTML:
```html
<html>
    <head>
        <title>My First Web Page</title>
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

Para validar a página que criamos, podemos utilizar o W3C validation service: https://validator.w3.org/#validate_by_upload