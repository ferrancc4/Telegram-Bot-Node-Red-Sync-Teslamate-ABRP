# Telegram Bot with Node-Red Sync Teslamate and ABRP

![GitHub release (latest by date)](https://img.shields.io/github/v/release/ferrancc4/Telegram-bot-Node-Red-Sync-Teslamate-ABRP)
![GitHub Repo stars](https://img.shields.io/github/stars/ferrancc4/Telegram-bot-Node-Red-Sync-Teslamate-ABRP)
![GitHub](https://img.shields.io/github/license/ferrancc4/Telegram-bot-Node-Red-Sync-Teslamate-ABRP)
[![](https://img.shields.io/badge/Donate-PayPal-ff69b4.svg)](https://www.paypal.me/Ferrancc12)

![Resumen general](screenshots/capture_1.jpeg)


## Requisitos para la Instalación y correcto funcionamiento

Para el correcto funcionamiento del Flow tienes que tener los siguientes módulos instalados.

```bash 
node-red-contrib-telegrambot
```
```bash 
node-red-node-smooth
```
```bash 
node-red-contrib-postgresql
```
También es necesario tener la base de datos de Teslamate abierta.

### Instalación de los modulos requeridos

Seguir los siguientes pasos para instalar los diferentes modulos necesarios.

**1-Abrir Node-Red:** Inicia Node-Red accediendo a su interfaz web a través de un navegador. Por lo general, puedes acceder a Node-Red en http://localhost:1880.

**2-Ingresar al Administrador de Paquetes:** Una vez que estés en la interfaz de Node-Red, haz clic en el icono de menú en la esquina superior derecha y selecciona "Manage palette". Esto te llevará al administrador de paquetes.

**3-Instalar un nuevo módulo:** En el administrador de paquetes, dirígete a la pestaña "Install". Aquí puedes buscar el módulo que deseas instalar. Puedes buscar por nombre o descripción del módulo.

```bash 
node-red-contrib-telegrambot
```
```bash 
node-red-node-smooth
```
```bash 
node-red-contrib-postgresql
```

**4-Seleccionar y Instalar:** Cuando encuentres el módulo que deseas instalar, haz clic en el botón "Install" junto a él. Node-Red descargará e instalará automáticamente el módulo desde el repositorio.

**5-Reiniciar Node-Red:** Una vez que se haya completado la instalación, es recomendable reiniciar Node-Red para asegurarte de que el nuevo módulo esté cargado correctamente. Puedes hacerlo desde el mismo administrador de paquetes o reiniciando el servicio de Node-Red.

### Importar el Flow

**1-Acceder al Editor:** Una vez que estés en la interfaz de Node-Red, verás el entorno de desarrollo visual. Haz clic en el icono de menú en la esquina superior derecha y a continuación, selecciona "Import" en el menú desplegable.

**2-Cargar el flow:** En la sección de importación, encontrarás varias opciones para cargar un flow. Puedes pegar el JSON del flow que deseas importar en el campo de texto, o puedes cargar un archivo JSON que contenga el flow.

**3-Seleccionar el flow:** Si estás importando desde un archivo, haz clic en el botón "select a file to import" para seleccionar el archivo JSON que contiene el flow que deseas importar. Si estás pegando el JSON directamente, simplemente pégalo en el campo de texto.

**4-Importar el flow:** Después de pegar el JSON o cargar el archivo, haz clic en el botón "Import" para comenzar el proceso de importación.


### Configurar nodo de MQTT

**1-Acceder al Editor de Nodos:** En la esquina superior derecha de la pantalla de Node-Red, haz clic en el icono con forma de rueda dentada para acceder a la configuración de nodos.

**2-Seleccionar el Nodo Mosquitto:** En la lista de nodos disponibles, busca y haz doble clic en el nodo llamado "Mosquitto" para abrir su ventana de configuración.

**3-Ajustar la Configuración:** En la ventana de configuración del nodo Mosquitto, ajusta los valores de "Server" y "Port" según la dirección IP o el nombre de host de tu servidor MQTT y el puerto MQTT que estés utilizando. Por defecto, el puerto es el 1883.

**4-Guardar los Cambios:** Una vez que hayas ajustado la configuración del nodo Mosquitto, asegúrate de hacer clic en el botón "Update" para guardar los cambios que has realizado.

### Configurar nodo de Telegram

**1-Acceder al Editor de Nodos:** En la esquina superior derecha de la pantalla de Node-Red, haz clic en el icono con forma de rueda dentada para acceder a la configuración de nodos.

**2-Seleccionar el Nodo Mosquitto:** En la lista de nodos disponibles, busca y haz doble clic en el nodo llamado "pmb_tesla_bot" para abrir su ventana de configuración.

**3-Ajustar el Token de Telegram:** En la ventana de configuración del nodo pmb_tesla_bot, busca el campo llamado Token y ajústalo con el token de acceso que hayas obtenido al crear un bot en Telegram a través del BotFather.

**4-Guardar los Cambios:** Una vez que hayas ingresado el token, asegúrate de hacer clic en el botón "Update" para guardar los cambios realizados en la configuración del nodo.

### Configurar nodo Postgres

Para poder utilizar este nodo primero tienes que tener acceso a la base de datos de Teslamate. Si ya tienes abiertos los puertos de la base de datos puedes pasar directamente al paso de configuracion del nodo Postgres.

#### Abrir puertos para acceder a la base de datos de Teslamate

Si tienes TeslaMate instalado en Docker Compose y deseas abrir puertos para conectarte a la base de datos PostgreSQL, aquí tienes los pasos que debes seguir:

**1-Edición de tu `docker-compose.yml`:**
   Abre el archivo `docker-compose.yml` en un editor de texto. En este archivo, deberías tener una sección que define el servicio de PostgreSQL. Asegúrate de que la configuración del servicio tenga la opción `ports` para mapear los puertos desde el contenedor al host.

   Por ejemplo, si la sección de PostgreSQL en tu `docker-compose.yml` luce así:

   ```yaml
   services:
     database:
       image: postgres:latest
       environment:
         POSTGRES_USER: teslamate
         POSTGRES_PASSWORD: mysecretpassword
         POSTGRES_DB: teslamate
   ```

   Puedes agregar una línea para mapear el puerto 5432 del contenedor al puerto deseado en el host:

   ```yaml
   services:
     database:
       image: postgres:latest
       environment:
         POSTGRES_USER: teslamate
         POSTGRES_PASSWORD: mysecretpassword
         POSTGRES_DB: teslamate
       ports:
         - 5432:5432
   ```

**2-Guardar y Aplicar los Cambios:** Después de realizar las modificaciones en el archivo `docker-compose.yml`, guarda los cambios.

**3-Reinicia los Contenedores:** Ejecuta el siguiente comando en la misma ubicación donde tienes tu `docker-compose.yml` para reiniciar los contenedores con la nueva configuración de puertos:

   ```sh
   docker-compose down
   docker-compose up -d
   ```

Recuerda que al abrir puertos, estás exponiendo servicios a Internet, lo que puede tener implicaciones de seguridad. Asegúrate de implementar medidas de seguridad adecuadas, como cortafuegos y autenticación sólida, para proteger tus servicios y datos.

#### Configuración nodo Postgres

**1-Acceder al Editor de Nodos:** En la esquina superior derecha de la pantalla de Node-Red, haz clic en el icono con forma de rueda dentada para acceder a la configuración de nodos.

**2-Seleccionar el Nodo Mosquitto:** En la lista de nodos disponibles, busca y haz doble clic en el nodo llamado "pmb_tesla_bot" para abrir su ventana de configuración.

**3-Conexión a la Base de Datos:** En la pestaña "Connection", ingresa los detalles de conexión a tu base de datos PostgreSQL:

    Host: La dirección IP o el nombre de host donde se encuentra la base de datos.
    Port: El número de puerto de la base de datos (por defecto es 5432).
    Database: El nombre que le hemos puesto a la base de datos en el `docker-compose.yml`.
    SSL: Dejamos la opción "false".

**4-Usuario y contraseña:** En la pestaña seguridad introducimos el usuario y contraseña que hemos definido en el `docker-compose.yml` para nuestra base de datos.

### Configurar ABRP y Telegram

**1-Configuración de ABRP:** Accede a tu cuenta en A Better Routeplanner (ABRP) y obtén tu token de usuario (abrp_user_token) y el modelo de tu automóvil (abrp_car_model) que deseas utilizar en el flow.

**2-Obtener el ChatID de Telegram:** Para obtener el chatID de Telegram, hay diferentes metodos que puedes encontrar en internet.

**3-Abrir el flow en Node-Red:** Accede al flow en Node-Red donde en el apartado MQTT to Telegram.

**4-Encontrar y Modificar la Función Variables:** Busca el nodo de función llamado "variables" dentro del flow. Haz doble clic en el nodo "variables" para abrir su ventana de edición.

**5-Actualizar Valores de las Variables:** En la ventana de texto que se abre, modifica los valores de las siguientes variables:
     - `telegram_chatId`: Reemplaza con el chatID que obtuviste de Telegram.
     - `abrp_user_token`: Reemplaza con tu token de usuario de ABRP.
     - `abrp_car_model`: Reemplaza con el modelo de automóvil que configuraste en ABRP.

**6-Guardar los Cambios:** Una vez que hayas actualizado los valores de las variables, asegúrate de guardar los cambios en la función "variables".

### Configuración Geoapify

Este flow utiliza la apy de Geoapify para obtener las direcciones de las calles a partir de las coordenadas de longitud y latitud obtenidas de la base de datos de teslamate. Para obtener la api key debes seguir los siguientes pasos:

**1-Accede al Sitio Web de Geoapify:** Abre tu navegador web y visita el sitio web de [Geoapify](https://www.geoapify.com).

**2-Crea una Cuenta o Inicia Sesión:** Si aún no tienes una cuenta en Geoapify, regístrate creando una cuenta nueva. Si ya tienes una cuenta, inicia sesión con tus credenciales.

**3-Crea un Proyecto:**
   - En el panel de control, busca la sección para crear un nuevo proyecto. Por lo general, suele haber un botón o enlace llamado "Create New Project" o similar.
   - Proporciona un nombre descriptivo para tu proyecto y cualquier otra información requerida.

**4-Obtén tu API Key:**
   - Después de crear el proyecto, en el panel de control, busca la sección donde se generan las API Keys. Puede llamarse "API Keys" o similar.
   - Aquí podrás ver una lista de tus API Keys existentes o crear una nueva.
   - Una vez creada, se te proporcionará tu API Key. Asegúrate de copiarla y guardarla en un lugar seguro, ya que será necesaria para autenticarte en las solicitudes a Geoapify.

**5-Abrir el flow en Node-Red:** Accede al flow en Node-Red donde en el apartado MQTT to Telegram.

**6-Encontrar y Modificar la Función Variables:** Busca el nodo de función llamado "variables" dentro del flow. Haz doble clic en el nodo "variables" para abrir su ventana de edición.

**7-Actualizar Valores de las Variables:** En la ventana de texto que se abre, modifica los valores de las siguientes variables:
    - `geoAPY`: Reemplaza con api key generada anteriormente.

**8-Guardar los Cambios:** Una vez que hayas actualizado los valores de las variables, asegúrate de guardar los cambios en la función "variables".

### Desplegar el flow

Después de hacer todos los cambios, asegúrate de hacer clic en el botón "Deploy" en la esquina superior derecha para guardar y activar los cambios en tu entorno de Node-Red.

## A tener en cuenta

Quiero aclarar que los enlaces a los gráficos de Grafana que encontrarás en el bot no son los gráficos predeterminados de TeslaMate. Estos enlaces están dirigidos a gráficos personalizados creados por [Carlos Cuezva - dashboards-Grafana-Teslamate](https://github.com/CarlosCuezva/dashboards-Grafana-Teslamate).

## Créditos

- Autor: Ferran Caubet

## Aviso importante

Este proyecto ha sido desarrollado de forma autodidacta por mí, Ferran Caubet, y es el resultado de mis esfuerzos y aprendizaje personal. Quiero dejar claro que no soy un programador profesional certificado, sino más bien un entusiasta autodidacta de la programación.

Inspirado por el proyecto de [Carlos Cuezva](https://github.com/CarlosCuezva/Sync-Teslamate-with-Telegram-and-ABRP), decidí embarcarme en esta iniciativa. Reconozco que pueden existir errores y áreas que podrían haber sido programadas de manera más eficiente. Cualquier defecto o deficiencia en el proyecto no debe interpretarse como una falta de esfuerzo o dedicación, sino como una parte natural del proceso de aprendizaje.

Estoy comprometido a mejorar mis habilidades y continuar perfeccionando este proyecto a medida que adquiera más experiencia. Aprecio sinceramente cualquier retroalimentación constructiva y sugerencias para mejorar este proyecto. ¡Gracias por tu comprensión y apoyo!

Atentamente,

Ferran Caubet.

## Colabora y Apoya

Si has disfrutado de mi proyecto y te ha sido útil, considera apoyar mi formación en programación mediante una colaboración en PayPal. Cada contribución, por modesta que sea, me ayudará a seguir aprendiendo y mejorando mis habilidades. Tu apoyo directo es invaluable para mí.

¡Gracias por ser parte de mi viaje de aprendizaje!

[![](https://img.shields.io/badge/Donate-PayPal-ff69b4.svg)](https://www.paypal.me/Ferrancc12)

## Licencia

Distribuido bajo [licencia MIT](./LICENSE)
