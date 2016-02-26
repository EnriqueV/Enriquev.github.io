---
layout: post
title: React Primeros pasos
cover: react.png
date:   2016-02-23 19:00:00
categories: posts
---

[React](https://facebook.github.io/react/ "react"), es un framework creado por facebook que
se enfoca en la creación de aplicaciones tipo [SPA](https://es.wikipedia.org/wiki/Single-page_application "SPA") y en construcción de interfazes para el usuario, en este tutorial veremos un poco sobre como podemos dar nuestros
primeros pasos con este framework, entremos en materia!

### Flux
Antes de ver un poco de código es importante conocer algunos conceptos que rigen la filosofia de react, para ellos veamos un poco sobre:  Dispatchers - Stores - Views

![Flux](/images/flux.png "flux")

#### Actions:
Estas son diferentes operaciones que podemos realizar, en nuestra applicación
como por ejemplo hacer click en un botón que realize un submit, borrar un elemento,
crear un item nuevo en una lista etc.

#### Dispatcher:
Es en cargado de manejar el trafico de los eventos en nuestra applicación, es quien se encarga
de recibir todas la acciones y decide cuales se realizan, algo importante de este elemento es que, es el unico que tiene su propia libreria para su implementación [dispatcher](https://github.com/facebook/flux/blob/master/src/Dispatcher.js)

#### Stores:
Los stores juegan un papel muy importante, podriamos llamarlos como los encargados de la
comunicación de los Dispatcher y las vistas, ya que mantiene los datos que iran mostrados en
nuestra vista.

Con estos conceptos podemos dar paso a hacer nuestro primer **Hello word con react**
veamos un poco de codigo :

Primero agregamos react a nuestro proyecto:

`<script src="build/react.js"></script>`

`<script src="build/react-dom.js"></script>`

Para este ejemplo, descargue react desde su [pagina](http://facebook.github.io/react/docs/tooling-integration.html) oficial, pero existe
otras formas en como puedes agregar react a tu proyecto y puedes ver las [aqui](http://facebook.github.io/react/docs/tooling-integration.html)

Creamos la estructura basica de nuestro proyecto:

  ```
  <!DOCTYPE HTML>
  <html>
    <head>
      <meta charset="utf-8">
      <title>React Hello World</title>
    <script src="build/react.js"></script>
    <script src="build/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
    </head>
    <body>
      <div id="saludo"></div>
     <script type="text/babel">
       ReactDOM.render(
         <h1>Hola, Mundo con react!</h1>,
         document.getElementById('saludo')
       );
     </script>


    </body>
  </html>

```

###El codigo
Bien veamos un poco sobre el ejemplo,antes que nada aclaro que estoy usando react con
[Babel](https://babeljs.io/), ya que se encarga de traducir la sintaxis de
[JSX](https://facebook.github.io/react/docs/jsx-in-depth.html)
 a javascript, el codigo es bastante simple hemos utilizado el [DOM](https://developer.mozilla.org/es/docs/DOM) para renderizar en nuestra vista las etiquetas `h1` y poder mostrar nuestro saludo en un div que en este caso lo insertamos por medio de su id, con esto hemos realizado nuestro primer "Hola Mundo con react".

 Veamos un ejemplo un poco mas complejo:

 ``````
 <!DOCTYPE HTML>
  <html>
    <head>
      <meta charset="utf-8">
      <title>React Hello World</title>
    <script src="build/react.js"></script>
    <script src="build/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
    </head>
    <body>
      <div id="search"></div>
     <script type="text/babel">

var Buscador = React.createClass({

    getInitialState: function(){
        return { palabra: '' };
    },

    handleChange: function(e){



        this.setState({palabra:e.target.value});
    },

    render: function() {

        var autos = this.props.items,
            palabra = this.state.palabra.trim().toLowerCase();


        if(palabra.length > 0){



            autos = autos.filter(function(l){
                return l.name.toLowerCase().match( palabra );
            });

        }

        return <div>
  <input type="text" value={this.state.palabra}
  onChange={this.handleChange} placeholder="Escribe el nombre de un auto" />

                    <ul>

                        { autos.map(function(l){
                            return <li>{l.name} <a href={l.url}>{l.url}</a></li>
                        }) }

                    </ul>

                </div>;

    }
});


var autos = [

    { name: 'Mustang Shelby Clasic', url: 'http://goo.gl/Re8iab'},
    { name: 'Jeep Patriot', url: 'http://www.moibbk.com/images/jeep-patriot-4.jp'},
    { name: 'Hummer', url: 'http://ep.yimg.com/ay/yhst-66365157547983/hummer-h2-sut-lift-kits-7.jpg'},
    { name: 'Honda Civic', url: 'http://goo.gl/G2koV6'},
    { name: 'Subaru', url: 'http://zombdrive.com/images/subaru-1.jpg'},
    { name: 'Cayman', url: 'http://goo.gl/Xv1vE8'},
    { name: 'Ferrary', url: 'http://goo.gl/bJCREh'},

];

ReactDOM.render(
    <Buscador items={ autos } />,
    document.getElementById('search')
);
     </script>


    </body>
  </html>
``````
Con esto realizamos un buscador, para el cual hemos creado un componente en **react**, el cual busca los autos que considan con lo que digitamos en el input y reutilizamos un contanier para renderizar nuestra vista.

Esto a sido todo! pero aca dejo el enlace al codigo del ultimo [ejemplo](https://gist.github.com/EnriqueV/e0f5aad50d3515730959) para que puedas modificarlo y probarlo en tu navegador, hasta el siguiente tutorial!
