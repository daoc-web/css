---
lang: es
---

# Tutorial de CSS

CSS, Cascading Style Sheets, u Hojas de Estilo en Cascada, es un **lenguaje de hojas de estilo** utilizado para dar formato y estilo a un documento o página web. Generalmente se aplica sobre HTML.

Una hoja de estilo es un archivo, o de manera general un bloque de texto (por que CSS podría estar incluido en archivos que también tengan otro tipo de contenido, por ejemplo HTML), con instrucciones para renderizar una página web. El navegador lee el documento HTML para tener la estructura, significado y contenido de la información en general, y luego lee el documento CSS para saber cómo presentar ese contenido, y por ende la página web, al usuario.

El término Cascading (en cascada), se refiere a la forma como las instrucciones son aplicadas al documento. Estas instrucciones pueden venir de varias fuentes o de varias hojas de estilo. Unas forman parte del navegador, otras las puso el desarrollador del sitio web, y otras pueden haber sido proporcionadas incluso por el usuario. Estos orígenes o fuentes se clasifican según su especificidad e importancia para luego aplicarse a los elementos del html. El orden en el cual aparecen las instrucciones en las hojas afectará también este proceso. Más aún, los estilos que se aplican a un elemento, pueden tener efecto o transmitirse a sus elementos hijos cuando la propiedad es compatible.

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

[Familiarícese con todos los tipos de selectores.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

[Familiarícese con todas las propiedades.](https://www.w3schools.com/cssref/)

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


### Normal flow: Block o Inline

Antes de que a los elementos de una página web se les aplique cualquier tipo de modificación de estilo, son ubicados en el documento en lo que se conoce como el "flujo normal". Esto brinda el layout de base sobre el cual empezarán a aplicarse los cambios de posición o formato.

Todos los elementos tienen un "flujo" por defecto, el cual viene dado por la propiedad `display`, la cual tiene dos valores fundamentales: `block` e `inline`.

Los elementos de tipo `block` se posicionan verticalmente, uno bajo el otro. Figurativamente, es como si su caja ocupara todo el espacio horizontal de la página (como si, por que la caja solo ocupa el espacio necesario). Adicionalmente, luego de cada elemento se añada una línea adicional de espacio, separándolo del siguiente. [Aquí tiene una lista de los elementos tipo `block`.](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements#elements)

Los elementos de tipo `inline` se posicionan horizontalmente, uno junto al otro, mientras haya espacio disponible, y solo luego se desplazarán verticalmente, o a ls siguiente fila de elementos. Su caja ocupa exclusivamente el espacio necesario para su contenido (literal y figurativamente). Ningún espacio adicional se añade para separar a los elementos entre ellos. [Aquí tiene una lista de los elementos tipo `inline`.](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements#list_of_inline_elements)

El valor de la propiedad `display` puede modificarse para cualquier elemento.

> **Bloque flotante**. Los elementos pueden sacarse de su flujo normal,alineándose hacia el borde izquierdo o derecho de su contenedor, y permitiendo que otros elementos como texto por ejemplo, se ajusten o peguen a ellos adaptándose a su caja. Esto se define con la propiedad `float` que por defecto tiene el valor `none`, pero que puede modificarse con `left` o `right`.

[Conozca más sobre el layout del documento.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout)

### Posicionamiento

Los elementos deben ubicarse en algún lugar del documento. Esta ubicación generalmente está dada por la ubicación del elemento en el html, es decir ajustándose al *flujo normal* del documento, o puede modificarse bajo ciertas condiciones.

La propiedad relevante es `position`, y su valor por defecto es `static`. En este caso no hay modificaciones que se puedan aplicar. Hay, sin embargo, otros valores de la propiedad que permiten variaciones interesantes:

- `relative`, primero ubica al elemento en su posición por defecto, y luego lo desplaza, relativo a dicha posición, de acuerdo a los valores de las propiedades `top`, `right`, `bottom` y `left`.

- `absolute`, se retira al elemento de su posición por defecto, como si no estuviera ahí, y se lo ubica en una posición relativa a aquella de su ascendiente (padre generalmente) más cercano. El desplazamiento con respecto al elemento padre se determina por las propiedades `top`, `right`, `bottom` y `left`. 

- `fixed`, se retira al elemento de su posición por defecto, como si no estuviera ahí, y se lo ubica en una posición relativa a aquella del contenedor principal, generalmente la página. El desplazamiento con respecto a la página se determina por las propiedades `top`, `right`, `bottom` y `left`. Esta propiedad suele ocasionar que el elemento permanezca en una posición fija en la página, aunque el resto se desplaze al hacer scrolling.

- `sticky`, primero ubica al elemento en su posición por defecto, y luego lo desplaza, en una posición relativa a aquella de su contenedor más cercano con capacidades de "scrolling". El desplazamiento con respecto al elemento padre se determina por las propiedades `top`, `right`, `bottom` y `left`. Esta propiedad suele ocasionar que el elemento permanezca en una posición fija en su contenedor, aunque el resto se desplaze al hacer scrolling. Esta posición "fija" variará, sin embargo, al cruzar ciertos límites (es una especie de *fixed-relative* si se quiere).

[Conozca más sobre el posicionamiento.](https://developer.mozilla.org/en-US/docs/Web/CSS/position)

## Diseño web adaptable (Responsive Web Design, RWD)

En la actualidad, la variedad de dispositivos en los cuales deberá presentarse una página web es enorme. Las diferencias sobre todo en lo que respecta con el tamaño y la resolución de las pantallas, obliga a que el diseño no pueda ser estático (enfocado a un solo tamaño y resolución) sino adaptable.

El diseño adaptable o "Responsive" (RWD), es una serie de guías, prácticas, técnicas y elementos, que permiten a la página web adaptarse de manera grácil y amigable con el usuario, a diferentes tamaños y resoluciones de pantallas.

Si bien el RWD consta de muchos conceptos, hay cuatro que son tal vez los más relevantes: cuadrículas, imágenes y texto fluidos o adaptables, y media queries.

> Otro elemento importante relacionado con RWD es el Viewport, el cual es una "meta" etiqueta HTML, y lo puede revisar [aquí](https://github.com/dordonez-ute-apweb/html#viewport).

### Imágenes adaptables

Una de las técnicas más sencillas es poner la propiedad `max-width` de las imágenes al 100%. Esto permitirá que, si el espacio disponible es limitado, la imagen se achique para adaptarse. Sin embargo, nunca sobrepasará su tamaño real.

```css
img {
  max-width: 100%;
}
```

### Texto adaptable

Al indicar el tamaño del texto que se usará en una parte del documento, siempre es preferible usar medidas relativas (em, rem, vw), en lugar de medidas fijas (px, mm, cm, ...).

- `rem` es una medida relativa al tamaño de la fuente del elemento raíz del documento (generalmente `html`). Si dicho valor no ha sudo definido, se usa el tamano de fuente por defecto del browser (que suele ser 16px). `1rem` indica que la medida es igual, `2rem` que es el doble, `0.5rem` que es la mitad, y así. Esta es una medida más predecible dado que se basa en un valor único.
    ```css
    h1 {
        font-size: 3em;
    }
    ```
- `em` es una medida relativa al tamaño de la fuente del contenedor inmediato, que se comporta com `rem`. Esta medida, al ser más local dado que el contenedor padre variará, permite controlar de mejor manera la adaptabilidad de ciertas secciones del documento. Sin embargo, al combinarse de contenedor en contenedor, puede tener efectos indeseables, como texto muy pequeño o muy grande.
    ```css
    h1 {
        font-size: 2em;
    }
    ```
- `vw` es una medida relativa al ancho del viewport. `1vw` equivale a 1% de su ancho. El inconveniente de esta medida es que al usarla no permite hacer zoom del texto definido así.
    ```css
    h1 {
        font-size: 5vw;
    }
    ```
- `calc(?rem + ?vw)` es una alternativa muy flexible que combina `rem` y `vw` gracias a la función `calc`. Esto combina una parte a la que se puede hacer zoom (`rem`) a la cual se añade un valor adicional (`vw`).
    ```css
    h1 {
        font-size: calc(1.5rem + 3vw);
    }
    ```
[Conozca más sobre el diseño adaptable.](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)

### Media queries

Este es probablemente el componente que hace posible el diseño adaptable en general. Permite efectuar un test sobre las condiciones del dispositivo, como tamaño y resolución de la pantalla, y dependiendo de ellas aplicar selectivamente ciertas reglas u hojas de estilo.

Se utiliza mediante la regla `@media`, luego de la cual se indican los tipos de media y las características de los mismos. Finalmente se incljuye un bloque CSS que aplicará solo si las condiciones se cumplen. Un ejemplo:

```css
@media screen and (min-width: 1024px) and (orientation: landscape) {
  /* … */
}

```
> Esta media query indica que el bloque CSS se aplicará solo si el tipo de media es pantalla, si el ancho mínimo de dicha pantalla es 1024 pixeles, y si el dispositivo está orientado horizontalmente.

Los tipos de medio pueden ser `all`, que indica que cualquier medio es aceptado, `print` y `screen`.

Las características hay en gran número ([revíselas](https://developer.mozilla.org/en-US/docs/Web/CSS/@media#media_features)), pero en general nos interesa aquellas relacionadas con las pantallas, como `(min|max)-width`, `orientation` y `(min|max)-resolution`.

Los tipos y las características se pueden combinar mediante los operadores `and` y `not`, y pueden presentarse en una lista separada por comas. Si cualquier elemento de la lista se valida, se aplicará el bloque CSS. Un ejemplo:
```css
@media (min-width: 640px), screen and (not orientation: portrait) {
  /* … */
}
```
> Esta regla se validará si ocurre cualquiera de dos cosas (como un operador "or"): el ancho mínimo del medio (cualquier medio) es 640 pixeles, por un lado, o el medio es pantalla y la orientación NO es vertical, por otro lado.

[Conozca más sobre las media queries.](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries)

### Cuadrículas adaptables

Las cuadrículas adaptables permiten reducir el número de media queries que se efectúan, y por ende el número de CSSs que hay que diseñar. Al usar cuadrículas adaptables, estas maximizan el uso del espacio disponible, distribuyendo de la mejor manera sus elementos internos, y reaccionando inmediatamente a cambios en el tamaño de la visualización que puedan ocasionarse, por ejemplo, por el usuario al redimensionar la ventana del browser.

Las técnicas que más se usan actualmente son el diseño multicolumna, las flexbox y las grid.

#### Diseño multicolumna

Utiliza principalmente la propiedad `column-count` para distribuir automáticamente el contenido del elemento indicado, en el número de columnas especificadas.

```css
.columnas {
  column-count: 3;
}
```
> Esta instrucción haría que todos los elementos pertenecientes a la clase `columnas` distribuyan su contenido en tres columnas.

Alternativamente puede utilizarse la propiedad `column-width`, indicando un valor en pixeles. El sistema creará tantas columnas como sean necesarias, cada una del ancho indicado (o lo más cercano posible), para llenar el espacio disponible.

Otras propiedades como `column-gap` o `column-rule` existen, que facilitan el formateo de las columnas.

[Familiarícese con estas propiedades.](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Multiple-column_Layout)

#### Flexbox

Permite distribuir los elementos dentro de un contenedor en una sola dimensión, sea esta horizontal o vertical.

Para crear un contenedor flex, hay que cambiar su propiedad `display` al valor `flex`. Todos los elementos hijos del contenedor se convierten automáticamente en items flex, y serán distribuidos de acuerdo a las reglas del flexbox.

Dado que el flexbox solo actúa en una dimensión, hay que especificar la orientación de los items con la propiedad `flex-direction`, que puede tomar los valores `row` (izquierda a derecha), `row-reverse` (derecha a izquierda), `column` (arriba hacia abajo) o `column-reverse` (abajo hacia arriba). El valor por defecto es `row`.

[Familiarícese con el flexbox.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout)

#### Grid

Este es probablemente el más flexible, y por ello también el más usado, de los elementos para crear cuadrículas adaptables. Es similar al flexbox, pero ya trabaja en dos dimensiones, lo que le permite ubicar sus elementos tanto en filas como en columnas, o en celdas si se prefiere.

Para crear un contenedor grid, hay que cambiar su propiedad `display` al valor `grid` o `inline-grid`. Todos los elementos hijos del contenedor se convierten automáticamente en items grid.

Para definir cuántas columnas o filas deberá tener la cuadrícula, se usan las propiedades `grid-template-columns` y `grid-template-rows`, las cuales funcionan muy parecido, y en general solo hay que usar una de ellas. Es decir, si se define un número específico de columnas, se crearán cuantas filas sean necesarias para albergar a todos los grid items.

Para indicar cuántas columnas tendrá la cuadrícula (para filas será igual), se especifica el ancho de cada una de ellas:

```css
.rejilla {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
}
```

> Cualquier elemento en la clase `rejilla` se convierte en una cuadrícula, gragias a `display: grid`. `grid-template-columns: 1fr 1fr 1fr` indica que habrán tres columnas, la del medio del doble del ancho que las otras dos.
>> `fr` es una medida relativa que otorga una fracción del espacio disponible.

Cuando varias columnas seguidas tienen la misma medida, se puede usar `repeat`:

```css
grid-template-columns: 20px repeat(6, 1fr) 30px;
```

> Aquí se indica que primero habrá una columna de 20 pixeles, luego habrán 6 columnas de 1fr, y finalmente una columna de 30 pixeles, 8 columnas en total.

Los grid items por defecto se posicionarán dentro de las celdas en el orden en que fueron definidos en el html. Sin embargo, puede indicarse exactamente en qué posición deberán ir, con las propiedades `grid-column` y `grid-row`, en cada grid item.

```css
.caja1 {
    grid-column: 2;
    grid-row: 5;
}
```

> `caja1` se ubicará en la celda en la intersección de la columna 2 y de la fila 5

[Familiarícese con el grid.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)


