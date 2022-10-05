# Tutorial de CSS

CSS, Cascading Style Sheets, u Hojas de Estilo en Cascada, es un **lenguaje de hojas de estilo** utilizado para dar formato y estilo a un documento o página web. Generalmente se aplica sobre HTML.

Una hoja de estilo es un archivo, o de manera general un bloque de texto (por que CSS podría estar incluido en archivos que también tengan otro tipo de contenido, por ejemplo HTML), con instrucciones para renderizar una página web. El navegador lee el documento HTML para tener la estructura, significado y contenido de la información en general, y luego lee el documento CSS para saber cómo presentar ese contenido, y por ende la página web, al usuario.

El término Cascading (en cascada), se refiere a la forma como las instrucciones son aplicadas al documento. Estas instrucciones pueden venir de varias fuentes o de varias hojas de estilo. Unas forman parte del navegador, otras las puso el desarrollador del sitio web, y otras puededn haber sido proporcionadas incluso por el usuario. Estos orígenes o fuentes se clasifican según su especificidad e importancia para luego aplicarse a los elementos del html. El orden en el cual aparecen las instrucciones en las hojas afectará también este proceso. Más aún, los estilos que se aplican a un elemento, pueden tener efecto o transmitirse a sus elementos hijos cuando la propiedad es compatible.

El algoritmo de cascada aplicado por los navegadores puede ser muy complejo. [En este link puede obtener más información](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade).


## Reglas

Una hoja de estilo CSS está formada por un grupo de reglas de estilo. Las reglas tienen como sintaxis de base la siguiente:

```css
/* 1 */
selector {
    propiedad: valor;
}
```

>- En primer lugar se escribe un selector que indica los elementos html que se van a seleccionar para aplicar el formato.
>- Luego, entre llaves (`{ ... }`) se indica la declaración, es decir la propiedad que se va a modificar, seguida de dos puntos (`:`), seguidos del valor que se pondrá a la propiedad, terminando la declaración por punto y coma (`;`).
>- Pueden ponerse comentarios, de preferencia en su propia línea, entre los símbolos `/*` y `*/` (como en C o Java).

Una alternativa muy utilizada para agrupar reglas es:

```css
/* 2 */
selector {
    p1: valor;
    p2: valor;
    ...
}
```

>- Se puede incluir varias propiedades dentro de una misma regla. Basta con poner todas las propiedades con sus valores dentro de las llaves, cuidando siempre de que cada *propiedad:valor* finalice con punto y coma. 

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
y la siguiente regla selecciona aquellos vínculos   sobre los cuales está pasando el mouse:
```css
a:hover {
    color: gray;
}
```

Las reglas, entonces, seleccionan elementos en el documento HTML, para establecer o cambiar los valores de sus propiedades.

[Familiarísese con todos los tipos de selectores.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

[Familiarísese con todas las propiedades.](https://www.w3schools.com/cssref/)

### Box model

Todos los elementos HTML se representan en el navegador como una caja (box) rectangular. Estas cajas responden a un modelo (model) específico, que les otorga ciertas propiedades comunes. Esto es lo que se conoce como el *Box model*.

El box model consta de cuatro áreas, cada una con sus propiedades que pueden modificarse:

- **Contenido,** es donde va el contenido relevante del elemento. Si es un párrafo, por ejemplo, es el texto.
    - Sus propiedades más relevantes (con respecto al modelo) son `width` y `height`.
    - Al asignar valor a estas propiedades, solo consideran el contenido (ni el relleno ni el borde). Esto se debe a que por defecto los elementos tienen la propiedad `box-sizing` igual a `content-box`.
    - Si se cambia la propiedad `box-sizing` a `border-box`, los valores de `width` y `height` considerarán o incluirán también el relleno y el borde
        - ciertos (pocos) elementos como `table` o `input`, tienen este valor por defecto.

- **Relleno (padding),** es un espacio interno, entre el contenido y el borde.
    - El tamaño del relleno puede controlarse con la propiedad `padding`, la cual permite modificar todo el padding por igual, o de manera independiente los cuatro (top, right, bottom, left).

- **Borde,**  es un rectángulo que marca el límite del contenido (y su relleno) y que se puede visualizar como cuatro líneas que demarcan la caja.
    - Sus propiedades más relevantes pueden modificarse con `border-color`, `border-style` y `border-width`.

- **Margen,** es un espacio externo, que va más allá del borde, y que separa a este elemento de los otros elementos que lo rodean en la página.
   - El tamaño del margen puede controlarse con la propiedad `margin`, la cual permite modificar todo el margen por igual, o de manera independiente los cuatro (top, right, bottom, left).

![Box model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model/boxmodel-(3).png)

[Conozca más sobre el Box model.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model)

### Posicionamiento

Los elementos deben ubicarse en algún lugar del documento. Esta ubicación generalmente está dada por la ubicación del elemento en el html, es decir ajustándose al *flujo normal* del documento, o puede modificarse bajo ciertas condiciones.

La propiedad relevante es `position`, y su valor por defecto es `static`. En este caso no hay modificaciones que se puedan aplicar. Hay, sin embargo, otros valores de la propiedad que permiten variaciones interesantes:

- `relative`, primero ubica al elemento en su posición por defecto, y luego lo desplaza, relativo a dicha posición, de acuerdo a los valores de las propiedades `top`, `right`, `bottom` y `left`.

- `absolute`, se retira al elemento de su posición por defecto, como si no estuviera ahí, y se lo ubica en una posición relativa a aquella de su ascendiente (padre generalmente) más cercano. El desplazamiento con respecto al elemento padre se determina por las propiedades `top`, `right`, `bottom` y `left`. 

- `fixed`, se retira al elemento de su posición por defecto, como si no estuviera ahí, y se lo ubica en una posición relativa a aquella del contenedor principal, generalmente la página. El desplazamiento con respecto a la página se determina por las propiedades `top`, `right`, `bottom` y `left`. Esta propiedad suele ocasionar que el elemento permanezca en una posición fija en la página, aunque el resto se desplaze al hacer scrolling.

- `sticky`, primero ubica al elemento en su posición por defecto, y luego lo desplaza, en una posición relativa a aquella de su contenedor más cercano con capacidades de "scrolling". El desplazamiento con respecto al elemento padre se determina por las propiedades `top`, `right`, `bottom` y `left`. Esta propiedad suele ocasionar que el elemento permanezca en una posición fija en su contenedor, aunque el resto se desplaze al hacer scrolling. Esta posición "fija" variará, sin embargo, al cruzar ciertos límites (es una especie de *fixed-relative* si se quiere).

[Conozca más sobre el posicionamiento.](https://developer.mozilla.org/en-US/docs/Web/CSS/position)

### Normal flow: Block o Inline



[Conozca más sobre el layout del documento.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout)

### Responsive design

https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design

### Flexbox

https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout

### Grid

https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout

### Viewport

https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_concepts

### Media queries

https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries

