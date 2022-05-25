# creacion-Backen-MEAN

# Nodemon y Express

## **Nodemon**

**[https://www.npmjs.com/package/nodemon](https://www.npmjs.com/package/nodemon)**

Esta herramienta se instala a través de npm y nos sirve para estar escuchando cambios en nuestra configuración de node.js y reinicia automáticamente el servidor.

Instalación global:

`npm install -g nodemon`

Ejecutar:

`nodemon app.js`

## **Express**

**[https://expressjs.com/es/](https://expressjs.com/es/)**

- Express es una infraestructura de aplicaciones web Node.js mínima y flexible que proporciona un conjunto sólido de características para las aplicaciones web y móviles (Framework).
- Con miles de métodos de programa de utilidad HTTP y middleware a su disposición, la creación de una API sólida es rápida y sencilla.

`npm i express`

## **[#](https://bluuweb.github.io/node/02-servidor/#express-hello-world)Express Hello World**

**[https://expressjs.com/es/starter/hello-world.html](https://expressjs.com/es/starter/hello-world.html)**

```jsx
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`);
});
```

Ejecute:

`nodemon app`

## **[#](https://bluuweb.github.io/node/02-servidor/#rutas)Rutas**

**[https://expressjs.com/es/starter/basic-routing.html](https://expressjs.com/es/starter/basic-routing.html)**

```jsx
app.get("/contacto", (req, res) => {
  res.send("ruta de contacto");
});
```

## **[#](https://bluuweb.github.io/node/02-servidor/#archivos-estaticos)Archivos Estáticos**

**[https://expressjs.com/es/starter/static-files.html](https://expressjs.com/es/starter/static-files.html)**

Para el servicio de archivos estáticos como, por ejemplo, imágenes, archivos CSS y archivos JavaScript, utilice la función de **middleware** incorporado express.static de Express.

- Cree una carpeta `public` con un archivo `index.html`

```jsx
app.use(express.static(__dirname + "/public"));
```

**path.join**

He visto varios ejemplos con path.join, este nos sirve hacer uniones de rutas (aquí public no lleva el "/"), ¿Es necesario?

```jsx
app.use(express.static(path.join(__dirname, "public")));
```

**Importante**

El orden es clave al ordenar nuestras rutas:

```jsx
app.get("/", (req, res) => {
  res.send("Hello World!");
});

`app.use(express.static(__dirname + "/public"));`
```

`__dirmane` es la ruta según la máquina donde se ejecuta el código:

```jsx
app.get("/contacto", (req, res) => {
  res.send(__dirname);
});
```

## **Middleware**

- **[https://expressjs.com/es/starter/faq.html](https://expressjs.com/es/starter/faq.html)**
- **[https://expressjs.com/es/guide/using-middleware.html](https://expressjs.com/es/guide/using-middleware.html)**

En palabras simples es una acción que se ejecuta antes de nuestra función de ruta.

El middleware es el software que brinda servicios y funciones comunes a las aplicaciones, además de lo que ofrece el sistema operativo. Generalmente, se encarga de la gestión de los datos, los servicios de aplicaciones, la mensajería, la autenticación y la gestión de las API.

Ayuda a los desarrolladores a diseñar aplicaciones con mayor eficiencia. Además, actúa como hilo conductor entre las aplicaciones, los datos y los usuarios.

En el caso de las empresas con entornos de contenedores y multicloud, el middleware puede rentabilizar el desarrollo y la ejecución de las aplicaciones según sea necesario.

- Configurar "Página 404"

```jsx
`<!DOCTYPE html>
<html lang="es"><head><meta charset="UTF-8" /><meta name="viewport" content="width=device-width, initial-scale=1.0" /><title>Document</title></head><body><h2>Esta es la página 404</h2><img
      src="https://sparktco.com/wp-content/uploads/2019/07/perdido.gif"alt=""/></body></html>`

`app.use((req, res, next) => {
  // res.status(404).send("Sorry cant find that!");
  res.status(404).sendFile(__dirname + "/public/404.html");
});`
```

En este caso `sendFile` abre un archivo en específico.

## **¿Qué sigue?**

Hasta el momento hemos trabajado con archivos estáticos pero la gracia de Express es que podemos utilizar gestores o motores de plantillas HTML, lo que nos facilitará la vida al momento de trabajar con bases de datos. Continuemos en la siguiente sección 😃

**[https://www.npmjs.com/package/nodemon](https://www.npmjs.com/package/nodemon)**

Esta herramienta se instala a través de npm y nos sirve para estar escuchando cambios en nuestra configuración de node.js y reinicia automáticamente el servidor.

Instalación global:

`npm install -g nodemon`

Ejecutar:

`nodemon app.js`

## **Express**

**[https://expressjs.com/es/](https://expressjs.com/es/)**

- Express es una infraestructura de aplicaciones web Node.js mínima y flexible que proporciona un conjunto sólido de características para las aplicaciones web y móviles (Framework).
- Con miles de métodos de programa de utilidad HTTP y middleware a su disposición, la creación de una API sólida es rápida y sencilla.

`npm i express`

## **Express Hello World**

**[https://expressjs.com/es/starter/hello-world.html](https://expressjs.com/es/starter/hello-world.html)**

```jsx
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`);
});
```

Ejecute:

`nodemon app`

## **Rutas**

**[https://expressjs.com/es/starter/basic-routing.html](https://expressjs.com/es/starter/basic-routing.html)**

```jsx
app.get("/contacto", (req, res) => {
  res.send("ruta de contacto");
});
```

## **Archivos Estáticos**

**[https://expressjs.com/es/starter/static-files.html](https://expressjs.com/es/starter/static-files.html)**

Para el servicio de archivos estáticos como, por ejemplo, imágenes, archivos CSS y archivos JavaScript, utilice la función de **middleware** incorporado express.static de Express.

- Cree una carpeta `public` con un archivo `index.html`

`app.use(express.static(__dirname + "/public"));`

**path.join**

He visto varios ejemplos con path.join, este nos sirve hacer uniones de rutas (aquí public no lleva el "/"), ¿Es necesario?

```jsx
app.use(express.static(path.join(__dirname, "public")));
```

**Importante**

El orden es clave al ordenar nuestras rutas:

```jsx
`app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.use(express.static(__dirname + "/public"));`

`__dirmane` es la ruta según la máquina donde se ejecuta el código:

`app.get("/contacto", (req, res) => {
  res.send(__dirname);
});`
```

## **Middleware**

- **[https://expressjs.com/es/starter/faq.html](https://expressjs.com/es/starter/faq.html)**
- **[https://expressjs.com/es/guide/using-middleware.html](https://expressjs.com/es/guide/using-middleware.html)**

En palabras simples es una acción que se ejecuta antes de nuestra función de ruta.

- Configurar "Página 404"

```jsx
`<!DOCTYPE html>
<html lang="es"><head><meta charset="UTF-8" /><meta name="viewport" content="width=device-width, initial-scale=1.0" /><title>Document</title></head><body><h2>Esta es la página 404</h2><img
      src="https://sparktco.com/wp-content/uploads/2019/07/perdido.gif"alt=""/></body></html>`

`app.use((req, res, next) => {
  // res.status(404).send("Sorry cant find that!");
  res.status(404).sendFile(__dirname + "/public/404.html");
});`
```

En este caso `sendFile` abre un archivo en específico.

resumen: 

1. abrir una carpeta en vsc
2. abrir una carpeta src
3. dentro de src → abrir estas carpetas (controller, models, routers,database.js,  index.js )
4. npm init 
5. npm i express nodemon mongoose cors morgan body-parser bcryptjs jsonwebtoken.

estos son todos los modulso necesarios para correr el backend. luego en package.json intalamos esto en e**l script**

```jsx
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "nodemon src/index.js"
  },
```

1. en consola ejecutar el servidor → npm run dev
2. en **index.js** ponemos:

```jsx
//requerimos los modulos necesarios

const express = require('express');
const app = express();
const morgan = require('morgan');
const cors = require('cors');
const bodyParser = require('body-parser')
//aqui va ir la base de datos
```

1. *vamos a configurar el puerto que vamos escuchar*

```jsx
app.set('Port', process.env.PORT || 3000);
app.use(morgan('dev')
```

process.env.PORT —> obtiene el puerto que le estan otrogando si no se conecta al puerto 3000.

sirve para obtener el puerto del servidor externo

1. *vamos a configurar el puerto que vamos escuchar*

```jsx

app.use(morgan('dev'));
app.use(bodyParser.urlencoded({extended: true}));
app.use(bodyParser.json());
app.use(cors({origen: '*'}));
```

1. *aqui vamos a utilizar las rutas*

```jsx

```

1. ir a la carpeta models y abrir un archivo llamado **personas.models.js**
2. *establecemos el esquema con el que vamos a trabajar es decir los campos o atributos.*

```jsx
**const mongoose = require('mongoose');
const Schema = mongoose.Schema;**

const personasSchema = new Schema({
    nombres:{type: String,required:[true, 'Nombre Obligatorio']},
    primerApellido:String,
    segundoApellido:String,
    cedula:String,
    edad:Number,
    nota: Number
})
```

1. *conversion a modelo debemos exportarlo para que sea obtenido por otro.* 

```jsx
module.exports = mongoose.model("personas", personasSchema);
```

1. en **database.js** *establecemos la conexion en la bd, debemmos tener en cuenta la direccion, sea local o externa(servidor)*

```jsx
const mongoose = require("mongoose");
URL=('mongodb://localhost/dbPrsonasBit');
```

1. *//enviamos la conexion de la bd, establecemos unas configuraciones predeterminadas.*

```jsx
mongoose
  .connect(URL, {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  })
  .then((db) => console.log("Base de datos conectada:", db.connection.name))
  .catch((error) => console.log(error));
```

1. *//exportamos nuestro modulo de la bd*

```jsx
module.exports = mongoose;
```

1. vamos a **index.js**

```jsx
const express = require("express");
const app = express();
const morgan = require("morgan");
const cors = require("cors");
const bodyParser = require("body-parser");
//aqui va ir la base de datos

require("./database"); --> este fue el que pusimos :)

//aqui estamos realizando nuestra primera peticion:
// POST, la cual se va a enviar la info que requerimos

app.set("Port", process.env.PORT || 3000);
app.use(morgan("dev"));
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
app.use(cors({ origen: "*" }));

//aqui vamos a utilizar las rutas

//aqui vamos a llamar nuestro puerto
app.listen(app.get("Port"), () => {
  console.log("El servidor esta escuchando por el puerto: ", app.get("Port"));
});
```

y se establece conexion! en la consola dice dbPsonasBit

1. dentro de controlador creamos una carpeta que se llame personas.controller.js

```jsx
const personaCtrl = {};
const persona = require("../models/personas.models");
//aqui estamos realizando nuestra primera peticion
personaCtrl.crear = async (req, res) => {
  const { nombres, primerApellido, segundoApellido, cedula, edad, nota } =
    req.body;
  const nuevaPersona = new persona({
    nombres,
    primerApellido,
    segundoApellido,
    cedula,
    edad,
    nota,
  });

//aqui evaluamos la respuesta, si es ok nos va a retornar el mensaje

  const respuesta = await nuevaPersona.save()
  res.json({
      mensaje: 'Persona creada',
      respuesta
  })
};
module.exports = personaCtrl
```

1. vamos a la carpeta route y creamos un archivo llamado personas.route.js

```jsx
const { Router } = require("express");
const router = Router();
const personaCtrl = require("../controller/personas.controller");

router.post("/crear", personaCtrl.crear);

module.exports = router;
```

1. luego vamos al index y ponemos la ruta 

```jsx
//aqui vamos a utilizar las rutas

app.use('/personas', require('./routes/personas.route'));
```
