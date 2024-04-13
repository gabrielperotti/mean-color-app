# mean-color-app

Claro, vamos a dividir la creación de este proyecto MEAN (MongoDB, Express.js, Angular, Node.js) en partes, utilizando Docker y Git submódulos para organizar el código. La aplicación que describes parece una buena forma de demostrar estos conceptos. Comenzaremos por establecer la estructura general del proyecto y luego procederemos paso a paso.

### Paso 1: Configuración Inicial del Proyecto
Primero, configuraremos el repositorio principal y los submódulos para el frontend y el backend.

#### 1.1 Crear el Repositorio Principal
- Crea un nuevo repositorio en GitHub. Puedes llamarlo, por ejemplo, `mean-color-app`.
- Clónalo en tu máquina local:
  ```bash
  git clone https://github.com/your-username/mean-color-app.git
  cd mean-color-app
  ```

#### 1.2 Crear los Submódulos (Frontend y Backend)
- Crea dos nuevos repositorios en GitHub para el frontend y el backend. Puedes nombrarlos `mean-color-app-frontend` y `mean-color-app-backend`.
- Añade cada uno como un submódulo en tu repositorio principal:
  ```bash
  git submodule add https://github.com/your-username/mean-color-app-backend.git backend
  git submodule add https://github.com/your-username/mean-color-app-frontend.git frontend
  ```

### Paso 2: Configuración del Backend
En este paso, configuraremos el backend con Node.js y Express, conectándolo a MongoDB, y prepararemos un script de inicialización para la base de datos.

#### 2.1 Configuración del Proyecto Backend
- Navega al directorio del backend y inicializa un nuevo proyecto Node.js:
  ```bash
  cd backend
  npm init -y
  ```
- Instala las dependencias necesarias:
  ```bash
  npm install express mongoose body-parser cors dotenv
  ```
- Crea un archivo `server.js` con el siguiente contenido básico:
  ```javascript
  const express = require('express');
  const mongoose = require('mongoose');
  const bodyParser = require('body-parser');
  const cors = require('cors');

  const app = express();
  const PORT = process.env.PORT || 3000;

  // Middleware
  app.use(cors());
  app.use(bodyParser.json());

  // MongoDB Connection
  mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => console.log('MongoDB connected'))
    .catch(err => console.log(err));

  // Routes
  app.get('/', (req, res) => {
    res.send('Hello from Express!');
  });

  // Start the server
  app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
  });
  ```
- Añade un modelo simple en `models/Color.js`:
  ```javascript
  const mongoose = require('mongoose');
  const Schema = mongoose.Schema;

  const colorSchema = new Schema({
    name: String
  });

  module.exports = mongoose.model('Color', colorSchema);
  ```

#### 2.2 Inserción de Datos Iniciales
- Modifica el `server.js` para insertar algunos colores iniciales en la base de datos al iniciar el servidor:
  ```javascript
  const Color = require('./models/Color');

  mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => {
      console.log('MongoDB connected');
      Color.find().countDocuments((err, count) => {
        if (count === 0) {
          Color.insertMany([{ name: 'Red' }, { name: 'Green' }, { name: 'Blue' }])
            .then(() => console.log('Initial colors added'))
            .catch(err => console.log(err));
        }
      });
    })
    .catch(err => console.log(err));
  ```

#### 2.3 Dockerfile para el Backend
- En el directorio `backend`, crea un `Dockerfile`:
  ```dockerfile
  FROM node:14
  WORKDIR /app
  COPY package*.json ./
  RUN npm install
  COPY . .
  EXPOSE 3000
  CMD ["node", "server.js"]
  ```

Hasta aquí hemos configurado el backend con una conexión a MongoDB y una inserción inicial de datos. En el siguiente mensaje, procederemos con el frontend y la integración de todo con Docker Compose. ¿Te gustaría continuar con el frontend o necesitas ajustar algo del backend?
