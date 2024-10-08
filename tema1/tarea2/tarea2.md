1. Crear el directorio de trabajo y inicializar el repositorio

```
mkdir ~/bloggalpon
cd ~/bloggalpon
git init
```

2. Crear el archivo index.html con la estructura básica

```html
<!DOCTYPE html>
<html lang='es'>
<head>
    <meta charset='UTF-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>
    <title>Blog Galpón</title>
</head>
<body>
</body>
</html>
```

3. Crear el primer commit

```
git add .
git commit -m "Crea el esqueleto básico del index.html"
```

4. Añadir contenido al `<head>`

```html
<link rel='stylesheet' href='style.css'>
```

```
git add .
git commit -m "Añade la cabecera del index.html"
```

5. Añadir contenido al `<body>`

```html
<section></section>
```

```
git add .
git commit -m "Añade la estructura básica del body."
```

6. Añadir contenido a `<section>`

```html
<article></article>
```

```
git add .
git commit -m "Añade toda la estructura de la zona de posts."
```

7. Crear style.css y añadir CSS

```css
body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
}

body {
    margin: 0;
    padding: 0;
}
```

```
git add .
git commit -m "Añade las CSS de html y de body."
```

8. Añadir CSS para elementos HTML5

```css
header, section, article, aside, footer {
    margin: 20px;
    padding: 10px;
    border: 1px solid #ccc;
}
```

```
git add .
git commit -m "Añade las CSS de varios elementos HTML5: header, section, article, aside y footer."
```

9. Añadir el logotipo logo.png

Coloca el archivo logo.png en el directorio raíz del proyecto.

```
git add .
git commit -m "Añade el logotipo de Galpón."
```

10. Añadir CSS para <section>

```css
section {
    background-color: #f4f4f4;
}
```

```
git add .
git commit -m "Añade las CSS de section."
```

11. Añadir CSS para el `<footer>`

```css
footer {
    text-align: center;
    padding: 20px;
    background-color: #333;
    color: #fff;
}
```

```
git add .
git commit -m "Añade las CSS del footer."
```

12. Añadir CSS para `<h1>` y enlaces

```css
h1 {
    color: #333;
}

a {
    color: #007bff;
    text-decoration: none;
}
```

```
git add .
git commit -m "Añade las CSS del H1 y de los enlaces."
```

13. Crear etiqueta v1.0

```
git tag v1.0
```

14. Crear rama desarrollo

```
git checkout -b desarrollo
```

15. Crear directorio images y mover logo.png

```
mkdir images
mv logo.png images/
git add .
git commit -m "Mueve el logotipo a la carpeta images."
```

16. Crear directorio CSS y mover style.css

```
mkdir CSS
mv style.css CSS/
git add .
git commit -m "Mueve la CSS a la carpeta CSS."
```

17. Cambiar referencias en index.html

Edita index.html para referenciar correctamente a la CSS y el logotipo:

```html
<link rel='stylesheet' href='CSS/style.css'>
<img src='images/logo.png' alt='Logotipo Galpón'>
```

Luego, agrega y haz commit:

```
git add .
git commit -m "Cambia las referencias a las CSS y a las imágenes al reorganizarlas en directorios."
```

18. Crear rama bugfix

```
git checkout master
git checkout -b bugfix
```

19. Quitar comentarios en CSS

Edita el archivo CSS correspondiente para quitar los comentarios mencionados y haz commit:

Edita CSS y quita los comentarios de los punteados

```
git add .
git commit -m "Introduce los punteados en la barra derecha y en el footer."
```

20. Introducir el título “Galpon”

Edita index.htm para incluir el título:

```html
<h1>Galpon</h1>
```

Agrega y haz commit:

```
git add .
git commit -m "Introduce el título en la página."
```

21. Cambiar 2012 por 2014 en el footer

Edita el footer en index.htm y quita (c):

```html
<!-- Cambia 2012 por 2014 y quita (c) -->
```

Agrega y haz commit:

```
git add .
git commit -m "Realiza pequeños ajustes en el footer."
```

22. Crear etiqueta v1.1

```
git tag v1.1
```

23. Llevar cambios a master

```
git checkout master
git merge bugfix
```

24. Borrar rama bugfix

```
git branch -d bugfix
```

25. Llevar cambios de desarrollo a master

```
git checkout master
git merge desarrollo
```

26. Crear etiqueta v1.2

```
git tag v1.2
```
