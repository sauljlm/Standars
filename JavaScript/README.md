JavaScript Coding Standards
===========================

## <a name='TOC'>Tabla de Contenido</a>
  
  1. [Puntuaci&oacute;n](#puntuacion)
  1. [Tipos](#types)
  1. [Arreglos](#arrays)
  1. [Cadenas de Texto](#strings)
  1. [Funciones](#functions)
  1. [Propiedades](#properties)
  1. [Variables](#variables)
  1. [Hoisting](#hoisting)
  1. [Expresiones de comparación e igualdad](#conditionals)
  1. [Comentarios](#comments)
  1. [Casting de Tipos & Coerción](#type-coercion)
  1. [Funciones de Acceso](#accessors)
  1. [Constructores](#constructors)
  1. [Eventos](#events)
  1. [Módulos](#modules)
  1. [Recursos](#resources)


## Sintaxis y formato

A manera general queremos:

* Indentar con **2** espacios, no tabs.
* Deja un espacio antes de la llave de apertura `{`.
* Usar llaves con todos los bloques de múltiples líneas (```if``` , ```function```).
* Un espacio antes del paréntesis de apertura en las sentencias de control (```if```, ```while```, etc.).
* Bloques de muchas líneas con ```if``` y ```else```, poner el ```else``` en la misma línea que el ```if```.
* No espacio entre el keyword function o el nombrede la funcion y el primer parentesis (`function() {}`)
* Separar a los operadores con espacios. `var x = y + 5;`
* Deja una línea en blanco luego de los bloques y antes de la siguiente sentencia.
* Ser descriptivo con nombres de variables, m&eacute;todos, funciones, etc.
* camelCase para nombrar objetos, funciones e instancias, ejem: `thisIsMyObject`, `thisIsMyFunction`
* PascalCase cuando nombre constructores o clases.
* No usar [palabras reservadas](http://es5.github.io/#x7.6.1) para nombres de propiedades, funciones o variables.
* Nombre sus funciones. Esto será de ayuda en caso de errores.

## <a name='puntuacion'>Puntuacion: comas, puntos y coma</a>

  - **No** usar comas al inicio de línea:

    ```javascript
    // mal
    var story = [
        once
      , upon
      , aTime
    ];

    // bien
    var story = [
      once,
      upon,
      aTime
    ];
    ```

  - **Sip.**

    ```javascript
    // mal
    (function() {
      var name = 'Skywalker'
      return name
    })()

    // bien
    (function() {
      var name = 'Skywalker';
      return name;
    })();

    // super bien (evita que la funcion se vuelva un argumento
    // cuando dos archivos con IIFEs sean concatenados)
    ;(function() {
      var name = 'Skywalker';
      return name;
    })();
    ```

## <a name='arrays'>Arreglos</a>
    ```
  - Usa Array#push, en vez de asignación directa, para agregar elementos a un arreglo.

    ```javascript
    var someStack = [];

    // mal
    someStack[someStack.length] = 'abracadabra';

    // bien
    someStack.push('abracadabra');
    ```

  - Cuando necesites copiar un arreglo usa Array#slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

    ```javascript
    var len = items.length;
    var itemsCopy = [];
    var i;

    // mal
    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // bien
    itemsCopy = items.slice();
    ```

## <a name='strings'>Cadenas de Texto</a>

  - Usa comillas simples `''` para las cadenas de texto

    ```javascript
    // mal
    var name = "Bob Parr";

    // bien
    var name = 'Bob Parr';

    // mal
    var fullName = "Bob " + this.lastName;

    // bien
    var fullName = 'Bob ' + this.lastName;
    ```

## <a name='functions'>Funciones</a>

  - Expresiones de función:

    ```javascript
    // expresion de funcion anonima
    var anonymous = function() {
      return true;
    };

    // expresion de funcion nombrada
    var named = function named() {
      return true;
    };

    // expresion de funcion inmediatamente invocada (IIFE)
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  - Nunca nombres a un parámetro como `arguments`, esto tendrá precedencia sobre el objeto `arguments` que es brindado en cada ámbito de función.

    **[[⬆ regresar a la Tabla de Contenido]](#TOC)**



## <a name='properties'>Propiedades</a>

  - Usa la notación de punto `.` cuando accedas a las propiedades.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    // mal
    var isJedi = luke['jedi'];

    // bien
    var isJedi = luke.jedi;
    ```

    **[[⬆ regresar a la Tabla de Contenido]](#TOC)**


## <a name='variables'>Variables</a>

  - Siempre usar `var` para declarar variables. No hacerlo resultará en variables globales. Debemos evitar contaminar el espacio global (global namespace).

  - Usar una declaración `var` por variable.

    ```javascript
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';
    ```

  - Declarar a las variables sin asignación al final. Esto es útil cuando necesites asignar una variable luego dependiendo de una de las variables asignadas previamente.

    ```javascript
    var items = getItems();
    var goSportsTeam = true;
    var dragonball;
    var length;
    var i;
    ```

  - Asigna las variables al inicio de su ámbito. Esto ayuda a evitar inconvenientes con la declaración de variables y temas relacionados a 'hoisting'.

    ```javascript
    // mal
    function() {
      test();
      console.log('doing stuff..');

      //..otras cosas..

      var name = getName();

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // bien
    function() {
      var name = getName();

      test();
      console.log('doing stuff..');

      //..otras cosas..

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // mal - llamada a funcion innecesaria
    function() {
      var name = getName();

      if (!arguments.length) {
        return false;
      }

      this.setFirstName(name);

      return true;
    }

    // bien
    function() {
      if (!arguments.length) {
        return false;
      }

      var name = getName();
      this.setFirstName(name);

      return true;
    }
    ```

    **[[⬆ regresar a la Tabla de Contenido]](#TOC)**

## <a name='conditionals'>Expresiones de comparación e igualdad</a>

  - Usa `===` y `!==` en vez de `==` y `!=` respectivamente.
  - Expresiones condicionales son evaluadas usando coerción con el método `ToBoolean` y siempre obedecen a estas reglas sencillas:

    + **Objects** son evaluados como **true** (también considera así al objeto vacío ```{}``` y arreglos sin contenido ```[]```)
    + **Undefined** es evaluado como **false**
    + **Null** es evaluado como **false**
    + **Booleans** son evaluados como **el valor del booleano**
    + **Numbers** son evaluados como **false** si **+0**, **-0**, o **NaN**, de otro modo **true**
    + **Strings** son evaluados como **false** si es una cadena de texto vacía `''`, de otro modo son **true**

    ```javascript
    if ([0]) {
      // true
      // un arreglo es un objeto, los objetos son evaluados como true
    }
    ```

  - Usa atajos.

    ```javascript
    // mal
    if (name !== '') {
      // ...stuff...
    }

    // bien
    if (name) {
      // ...stuff...
    }

    // mal
    if (collection.length > 0) {
      // ...stuff...
    }

    // bien
    if (collection.length) {
      // ...stuff...
    }
    ```

    **[[⬆ regresar a la Tabla de Contenido]](#TOC)**


## <a name='comments'>Comentarios</a>

  - Usa `/** ... */` para comentarios de múltiples líneas. Incluye una descripción, especificación de tipos y valores para todos los parámetros y valores de retorno.

    ```javascript
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param {String} tag
     * @return {Element} element
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

  - Usa `//` para comentarios de una sola línea. Ubica los comentarios de una sola línea encima de la sentencia comentada. Deja una línea en blanco antes del comentario.

    ```javascript
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }
    ```

    **[[⬆ regresar a la Tabla de Contenido]](#TOC)**


## <a name='type-coercion'>Casting de Tipos & Coerción</a>

  - Ejecuta coerción al inicio de una sentencia.
  - Strings:

    ```javascript
    //  => this.reviewScore = 9;

    // mal
    var totalScore = this.reviewScore + '';

    // bien
    var totalScore = '' + this.reviewScore;

    // mal
    var totalScore = '' + this.reviewScore + ' total score';

    // bien
    var totalScore = this.reviewScore + ' total score';
    ```

  - Usa `parseInt` para números y siempre con la base numérica para el casting de tipo.

    ```javascript
    var inputValue = '4';

    // mal
    var val = new Number(inputValue);

    // mal
    var val = +inputValue;

    // mal
    var val = inputValue >> 0;

    // mal
    var val = parseInt(inputValue);

    // bien
    var val = Number(inputValue);

    // bien
    var val = parseInt(inputValue, 10);
    ```

  - Booleans:

    ```javascript
    var age = 0;

    // mal
    var hasAge = new Boolean(age);

    // bien
    var hasAge = Boolean(age);

    // bien
    var hasAge = !!age;
    ```

    **[[⬆ regresar a la Tabla de Contenido]](#TOC)**


## <a name='accessors'>Funciones de Acceso</a>

  - Funciones de acceso para las propiedades no son requeridas, pero s&iacute; se crean, usar  ```getVal()``` y ```setVal('hello')```. Ejem: `getAge()`, `setAge(25)`.

  - Si la propiedad es un booleano, usa ```isVal()``` o ```hasVal()```.

    **[[⬆ regresar a la Tabla de Contenido]](#TOC)**


## <a name='events'>Eventos</a>

  - Cuando envíes paquetes de datos a los eventos (ya sea con eventos del DOM o algo propietario como los eventos de Backbone), pasa un mapa en vez de un valor directo. Esto permitirá a un próximo colaborador a agregar más datos al paquete de datos sin que tenga que encontrar o actualizar un handler para cada evento. Por ejemplo, en vez de:

    ```js
    // mal
    $(this).trigger('listingUpdated', listing.id);

    ...

    $(this).on('listingUpdated', function(e, listingId) {
      // hacer algo con listingId
    });
    ```

    prefiere:

    ```js
    // bien
    $(this).trigger('listingUpdated', { listingId : listing.id });

    ...

    $(this).on('listingUpdated', function(e, data) {
      // hacer algo con data.listingId
    });
    ```

  **[[⬆ regresar a la Tabla de Contenido]](#TOC)**

## <a name='recursos'>Recursos</a>
  
  - [JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
  - [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108)
  - [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting)
  - [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml) (Guía de Estilo de Javascript de Google)
  - [jQuery Core Style Guidelines](http://docs.jquery.com/JQuery_Core_Style_Guidelines) (Lineamientos de Estilo con el núcleo de jQuery)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwldrn/idiomatic.js/) (Idiomatic Javascript: Principios de Escritura Consistente)
  - [JavaScript Standard Style](https://github.com/feross/standard) (Estilo estándar de JavaScript)
  - [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript/tree/es5-deprecated/es5)


**[[⬆ regresar a la Tabla de Contenido]](#TOC)**

# };