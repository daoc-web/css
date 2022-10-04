# Tutorial de CSS

CSS, Cascading Style Sheets, u Hojas de Estilo en Cascada, es un **lenguaje de hojas de estilo** utilizado para dar formato y estilo a un documento web, generalmente en HTML.

Una hoja de estilo es un archivo, o de manera general un bloque de texto (por que CSS podría formar parte de archivos con otros contenidos, como HTML), con instrucciones para renderizar una página web. El navegador lee el documento HTML para tener la estructura, significado y contenido de la información en general, y luego lee el documento CSS para saber cómo presentar ese contenido, y por ende la página web, al usuario.

El término Cascading (en cascada), se refiere a la forma como las instrucciones son aplicadas al documento. Estas instrucciones pueden venir de varias fuentes o de varias hojas de estilo. Unas vienen ya con el navegador, otras las puso el desarrollador, e incluso el usuario puede de alguna manera indicar ciertas preferencias. Estos orígenes se clasifican por especificidad e importancia para aplicarse a los elementos del html, y también el orden en el cual aparecen las instrucciones afectará. Más aún, los estilos que se aplican a un elemento, pueden tener efecto sobre sus elementos hijos cuando la propiedad es compatible.

El algoritmo de cascada aplicado por los navegadores puede ser muy complejo. En [este link](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade) puede obtener más información.


## Reglas

Una hoja de estilo CSS está forma por un grupo de reglas de estilo. Las reglas tienen como sintaxis de base las siguientes:

```css
/* 1 */
selector {
    propiedad: valor;
}
```

>- En primer lugar se escribe un selector que indica los elementos html que se van a seleccionar para aplicar el formato.
>- Luego, entre llaves (`{ ... }`) se indica la declaración, es decir la propiedad que se va a afectar, seguida de dos puntos (`:`) y seguido del valor que se pondrá a la propiedad, terminada por punto y coma (`;`).
>- Pueden ponerse comentarios, de preferencia en su propia línea, entre los símbolos `/*` y `*/` (como en C o Java).

```css
/* 2 */
selector {
    p1: valor;
    p2: valor;
    ...
}
```

>- Se puede aplicar o modificar varias propiedades dentro de una misma regla. Basta con poner todas las propiedades con sus valores dentro de las llaves, cuidando siempre de que cada propiedad:valor finalice con punto y coma. 

Un ejemplo de regla a continuación:

```css
p {
    color: red;
}
```

> Esta regla selecciona los elementos `p` (párrafo) y les cambia el valor de la propiedad `color` a `red` (rojo). La propiedad `color`se refiere al color del primer plano, en este caso el texto del párrafo.

### Selectores

Vamos a ver aquí los principales tipos de selectores:

- Cualquier elemento html:
```css
p {}
div{}
h1{}
... 
```
- Grupos de elementos, separados por coma. Todos los elementos de los tipos indicados serán seleccionados por la regla:
```css
p, h1, h2 {
    color: yellow;  
}
```

- Clases, que se definen dentro de los elementos html en el atributo `class` y que permiten agrupar elementos html diversos. Se especifican en CSS con un punto (`.`) antes del nombre. Si tenemos los siguientes elementos html:
```html
<p class="uno">Un párrafo</p>
<h1 class="uno">Un header uno</h1>
<h2 class="dos">Un header dos</h2> 
```
Solo `p` y `h1` se verán afectados por la regla:
```css
.uno {
    color: blue;
}
```

- Id, que se definen dentro de los elementos html en el atributo `id`. Las id son únicas (no puede haber dos elementos con la misma id en un documento html). Se especifican en CSS con un símbolo numeral (`#`). Si tenemos los siguientes elementos html:
```html
<p id="uno">Un párrafo</p>
<p id="dos">Otro párrafo</h1>
```
Solo el párrafo con el texto "Un párrafo" se verá afectado por la regla:
```css
#uno {
    color: blue;
}
```
- Elementos hijo directos, separados por un símbolo mayor que `>`. Si tenemos estos elementos html:
```html
<p>Un párrafo</p>
<div>
    <p>Otro párrafo</h1>
</div>
<div>
    <span>
        <p>Tercer párrafo</h1>
    </span>
</div>
```
Solo el párrafo con el texto "Otro párrafo" se verá afectado por la regla:
```css
div > p {
    color: blue;
}
```

- Elementos descendientes, separados por un espacio ` `. Si tenemos estos elementos html:
```html
<p>Un párrafo</p>
<div>
    <p>Otro párrafo</h1>
</div>
<div>
    <span>
        <p>Tercer párrafo</h1>
    </span>
</div>
```
Los párrafos con los textos "Otro párrafo" y "Tercer párrafo" se verán afectados por la regla:
```css
div p {
    color: blue;
}
```

- Pseudo clases, que seleccionan elementos con base en información de su estado. Se utiliza los dos puntos `:` entre el elemento y su estado. La siguiente regla selecciona los vínculos que ya han sido visitados:
```css
a:visited {
    color: green;
}
```
y la siguiente aquellos sobre los cuales está pasando el mouse:
```css
a:hover {
    color: gray;
}
```

[Familiarísese con todos los tipos de selectores.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

