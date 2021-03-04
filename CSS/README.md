CSS-Coding-Standards
====================

Para reducir al m&iacute;nimo la fricci&oacute;n de nuestro CSS, el equipo ha llegado a un consenso acerca de nuestros est&aacute;ndares de codificaci&oacute;n para:

* Sintaxis y formato del CSS.
* Naming
* Arquitectura de nuestro CSS, incluyendo objetivos, errores a evitar y buenas pr&aacute;cticas.

## Tabla de Contenidos

* [Sintaxis y formato](#sintaxis-y-formato)
* [Orden y especificidad](#orden-y-especificidad)
* [Uso de whitespace](#uso-de-whitespace)
* [Comentarios](#comentarios)
* [Performance](#performance)
* [Lectura adicional](#lectura-adicional)

## Sintaxis y formato
Tener una forma est&aacute;ndar de escribir CSS significa que, el c&oacute;digo siempre se ver&aacute; y se sentir&aacute; familiar para todos los miembros del equipo.

El código *feo* y desordenado sienta un mal precedente, por el contrario, el c&oacute;digo que se ve limpio, se siente limpio. Queremos un ambiente agradable para trabajar, lo que fomenta en otros miembros del equipo mantener el nivel de limpieza y orden que encontraron.

A manera general queremos:

* Indentar con **4 espacios**, no tabs.
* Uso significativo de espacio en blanco.
* Ordenar alfabeticamente.
* Uso de min&uacute;sculas y nombres en ingl&eacute;s.
* Cambio de palabra separado por un gui&oacute;n (**-**).

### Convenciones para nombrar

* [Principios](#principios)
* [Namespaces](#namespaces)
* [Abreviaciones](#abreviaciones)

#### Principios:

* **Claridad** - comportamiento esperado / estilo debe ser inmediatamente obvio.
* **Sem&aacute;ntica** - lo que un objeto es importa m&aacute;s que como se ve.
* **Genérico** - el nombre debe ser aplicar para la mayoría de los sitios. Nombres demasiado específicos reducen el número de casos de uso o causa que clases sem&aacute;nticas sean utilizados en una forma no sem&aacute;ntica.
* **Brevedad** - cada byte cuenta, así que mantenga nombres tan cortos como sea posible, pero siempre y cuando sea necesario. Nombres m&aacute;s de 7 caracteres deben ser abreviados.

Siempre usamos min&uacute;scula, y el cambio de palabra separado por gui&oacute;n (*-*). Esto aplica para: clases, id, mixins, funciones, variables y colores:

```css
// Mal
.main_top { 
    color: #FFC20E; 
}

// Bien
.main-top { 
    color: #ffc20e; 
}
```

#### Namespaces:

* **js-** cuando seleccionamos elementos en el DOM con Javascript lo ideal es hacerlo via: ID's (preferiblemente) y, cuando son multiples elementos, usamos clasess con el prefijo js-, por ejemplo `js-submenu`. Estas clases nunca deben ser utilizadas para *styling*.

#### Abreviaciones:

Cada byte cuenta, as&iacute; que, mantenga nombres tan cortos como sea posible. Como regla general, nombres de m&aacute;s de 7 caracteres deben ser abreviados, sin embargo, no sacrificamos la **claridad** por brevedad. Algunas ideas de abreviaciones:

* configuration => config
* introduction => intro
* subcategory => subcat
* category => cat

## Orden y especificidad
Las reglas se deben escribir de tal manera que, utilicemos la Cascada y la Herencia, y siempre tratar de que la Especificidad este a un nivel similar (en la medida de lo posible).

#### especificidad

* En la medida de lo posible, las reglas subsecuentes deben heredar, nunca sobreescribir.
* Etiquetas - s&oacute;lo darle *estilo* a etiquetas globales.
* Clases - siempre es preferible darle *estilo* a selectores de tipo clase (.nombre-selector).
* Evitar sobrecalificar selectores, esto incrementa la especificidad, limita la reutilizacion y son menos eficientes (m&aacute;s trabajo para el browser)
* Evitar anidar innecesariamente.
* Evitar *encadenar* selectores. `.nav-item.expanded`

```css
// Evitar sobrecalificar selectores

// Mal
p.intro {

}

// Bien
.intro {

}
```

```css
// Evitar anidar innecesariamente

// Mal
.slide .panel-slide {

}

// Bien
.panel-slide {

}
```

```css
// Evitar encadenar selectores

// Mal
.message.error{

}

// Bien
.msj-error {

}
```

#### orden
Ordenar de forma alfanumérica, a excepción de donde se puede romper la Cascada.

* En la hoja de estilos: pseudo-selectores (:after, :active, :before, :hover, :link, :visited), etiquetas antes que clases y antes que ids - orden natural de la especificidad.
* Reglas, propiedades y selectores se deben ordenar alfabeticamente.

**Etiquetas y clases:**
```css
// Mal
.product-list {

}

p {
    
}

ul {
    
}

// Bien
p {
    
}

ul {
    
}

.product-list {

}
```

**Propiedades:**

```css
// Mal
selector {
    font-family: Arial, sans-serif; 
    padding: 0; 
    margin: 0; 
    color: red;
}

// Bien
selector {
    color: red; 
    font-family: Arial, sans-serif; 
    margin: 0; 
    padding: 0;
}
```

**Reglas:**
```css
// Mal
.product-list-thumb {

}

.product-list-item {

}

// Bien
.product-list-item {

}

.product-list-thumb {

}
```

## Uso de whitespace

#### indentación
Indentamos con **4 espacios**, no tabs. Puede configurar su editor para que lo realice de manera autom&aacute;tica. Los espacios son la &uacute;nica forma de garantizar que el c&oacute;digo *renderea* igual en el entorno de cualquier persona.

```css
// Mal
selector {
  propiedad: valor;
}

// Bien
selector {
    propiedad: valor;
}
```

#### espacios
Una declaración (propiedad y valor) por línea.

```css
// Mal
selector {
    propiedad: valor; propiedad: valor; propiedad: valor;
}

// Bien
selector {
    propiedad: valor;
    propiedad: valor;
    propiedad: valor;
}
```

Un espacio antes **{** (*bracket que abre*).

```css
// Mal
selector{

/* Bien */
selector {
```

Cierre en su su propia línea **}** (*bracket que cierra*).

```css
// Mal
selector { }

// Bien
selector {
    
}
```

Espacio después de **:** (dos puntos), **;** (punto y coma) y **,** (comas).

```css
// Mal
selector {
    color:red;font-family:Helvetica,Arial,sans-serif;
}

// Bien
selector {
    color: red; font-family: Helvetica, Arial, sans-serif;
}
```

#### nueva línea
Después de cada regla incluimos nueva línea

```css
// Mal
selector {
    propiedad: valor; 
}
selector {
    propiedad: valor;
}

// Bien
selector {
    propiedad: valor;
}

selector {
    propiedad: valor;
}
```

Cuando agrupamos selectores, cada selector en su propia l&iacute;nea

```css
// Mal
selector, selector2, selector3 {
    propiedad: valor; 
}

// Bien
selector,
selector2,
selector3 {
    propiedad: valor;
}
```

#### strings comillas dobles (" ")

```css
// Mal
selector {
    font-family: 'Goudy Bookletter 1911', sans-serif;
}

// Bien
selector {
    font-family: "Goudy Bookletter 1911", sans-serif;
}
```

## Comentarios
El código es escrito y mantenido por personas. Asegúrese de que su código sea descriptivo, este bien comentado, y sea accesible por otros. Un código bien comentado transmite contexto o propósito. No se limite a reiterar un nombre de componente o clase.

Asegúrese de escribir en oraciones completas para comentarios más grandes y frases concisas para las notas generales.

Usamos `//` para bloques de comentarios en lugar de `/* */`. Siempre dejamos un espacio antes del comentario.

```css
// Mal
selector {
    width: 100% !important; /* Sobreescribo */
}

// Bien
selector {
    width: 100% !important; // Comentario explicando porque el uso de !import
}
```

Debido a que, los comentarios se eliminan de las hojas de estilo compiladas, no se preocupe por la longitud de lo que escribes. Al mismo tiempo, nuestro objetivo debe ser: nuestro c&oacute;digo debe autoexplicarse, las classes nos sirven para eso, y mantener al m&iacute;nimo la cantidad de comentarios, para que el propósito/uso de un documento sea claro y que el mantenimiento no se convierta en algo tedioso.

## Performance

* Cuide el [orden y especificidad](#orden-y-especificidad)
* Evite el uso del * wildcard selector.
* Como regla general, evite anidación innecesario, y nunca anidar m&aacute;s de tres niveles. Si no puede evitarlo, de un paso atrás y reconsidere su estrategia.
* Evite anidar selectores: [selectores descendientes son los selectores más lentos](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS#Guidelines_for_Efficient_CSS).
* Evite especificar unidades cuando el valor es 0 (cero), ejemplo, 
  * `margin: 0;` en lugar de `margin: 0px;`
  * `border: 0;` en lugar de `border: none;`
  * `background-position: 0 0;` en lugar de `background-position: 0% 0%;`
* Siempre que aplique, utilice shorthand, `margin: 20px 0;` en lugar de `margin: 20px 0 20px 0;`
* Pero evite utilziar shorthand cuando es innecesario, `margin-bottom: 20px;` en lugar de `margin: 0 0 20px;`
* Use shorthand para valores hex cuando sea posible, ejemplo, `#fff` en lugar de `#ffffff`

## Lectura adicional

* [CSS Style Guides - CSS-Tricks ](https://css-tricks.com/css-style-guides/)
* [Writing efficient CSS - MDN ](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS)
