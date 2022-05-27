

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
