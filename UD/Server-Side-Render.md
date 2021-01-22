# Crea tu propio Server Side Render (SSR)

## Las ventajas del SSR

El SSR tiene dos principales ventajas sobre el _client side render_:

1. La velocidad de carga

El principal inconveniente del _renderizado del lado del cliente_ es el tiempo que se tarda en mostrar contenido ya que necesitamos que todos los archivos sean descargados, luego se muestra un HTML con una pantalla de carga, mientras tanto de fondo se está generando nuestro sitio y cuando por fin termina podemos usar el sitio, esto suele ser demasiado tardado sobre todo si realizamos peticiones a una API para obtener el contenido, como es el caso de este tutorial.

Por el contrario el SSR se encarga de generar todo el contenido del sitio y nos entrega el sitio ya construido, aunque sin ser interactivo ya que de fondo se está descargando los archivos JavaScript, pero desde el principio podemos ver todo el contenido.

2. SEO

El proceso por el cual los motores de búsqueda encuentran nuestras aplicaciones es: Primero abren nuestro sitio sin ejecutar JavaScript para ver su contenido, buscar palabras clave, buscar enlaces y luego de un buen tiempo (que depende del motor de búsqueda) se ejecuta JavaScript, este tiempo no está definido e incluso puede que nunca se realice ya que algunos motores de búsqueda **NO** pueden ejecutar JavaScript, esto es problemático si utilizamos React, Angular ó Vue.js ya que puede que el motor de búsqueda nunca podrá ver el contenido de nuestro sitio.

La ventaja de SSR es que los motores desde el principio pueden acceder al contenido del sitio y así rastrearlo mucho mejor y posicionarlo por encima de otros sitios.

## Necesitamos

- Conocer un poco sobre la [Rick and Morty API](https://rickandmortyapi.com/).

- Tener instalado [Node](https://nodejs.org/es/).

## Pasos

1.  Iniciamos el proyecto.

        npm init -y

2.  Instalamos la libreria Axios para realizar peticiones a la API.

        npm i axios -D

3.  Creamos el archivo index.js

        touch index.js

4.  Requerimos los módulos **fs**, **join** y **axios** en el archivo index.js, estos nos van a ayudar dentro de poco.

        const fs = require('fs');
        const axios = require('axios');
        const { join } = require('path');

5.  Creamos una función para traer los datos que necesitamos de la API, en esta ocasión únicamente vamos a requerir la información de un personaje: Rick Sánchez.

        function getCharacterInfo() {
            const URL = 'https://rickandmortyapi.com/api/character/1';

            const result = axios.default.get(URL);

            return result;
          }

6.  Ejecutamos la función getCharacterInfo para traer los datos de la API, esta función retorna una promesa por lo que podemos manejar la respuesta con un "_try catch_" usando las funciones **.then** y **.catch**

        getCharacterInfo()

        .then((response) => {
                const character = response.data;
        })
        .catch((err) => {
                // If an error happend throw the error
                throw err;
        });

7.  Ahora debemos crear la estructura de un archivo HTML dentro de JavaScript, para eso guardamos un template en una variable con comillas invertidas, esto va a permitirnos añadir los datos que obtuvimos cuando ejecutamos **getCharacterInfo(),** el template debe tener toda la estructura de un archivo HTML:

        const HtmlBase = `
        <!DOCTYPE html>
        <html lang="en">
                <head>
                        <meta charset="UTF-8" />
                        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
                        <title>'Dynamic title'</title>
                </head>
                <body>
                        <article>
                                <img src="image" alt="name" />
                                <h2>Name</h2>
                                <h3>Status:</h3>
                                <h3>Species:</h3>
                                <h3>Gender:</h3>
                                <h3>Origin:</h3>
                                <h3>Last Location:</h3>
                        </article>
                </body>
        </html>
        `;

8.  Ahora hay que usar los datos obtenidos dentro del HTML, como estamos usando comillas invertidas podemos escapar al string con el símbolo **${ }** y usar código de JavaScript.

        const HtmlBase = `
        <!DOCTYPE html>
        <html lang="en">
                <head>
                        <meta charset="UTF-8" />
                        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
                        <title>${character.name}</title>
                </head>
                <body>
                        <article>
                                <img src=${character.image} alt="${character.name}" />
                                <h2>${character.name}</h2>
                                <h3>Status: ${character.status}</h3>
                                <h3>Species: ${character.species}</h3>
                                <h3>Gender: ${character.gender}</h3>
                                <h3>Origin: ${character.origin.name}</h3>
                                <h3>Last Location: ${character.location.name}</h3>
                        </article>
                </body>
        </html>
        `;

Ya casi tenemos todo listo para crear nuestro propio SSR, solo hace falta almacenar el archivo para poder enviarlo a nuestro servidor.

9. Creamos la carpeta en la que vamos a almacenar nuestros archivos

Node tiene dos módulos que permiten crear carpetas:

- mkdir: Crea una carpeta de forma asíncrona.
- mkdirSync: Crea una carpeta de forma síncrona.

Ambos se encuentran en el módulo fs.

En este caso necesitamos crear la carpeta de forma síncrona ya que Node al ser asíncrono es posible que termine de crear el archivo antes de crear la carpeta y si no existe la carpeta el archivo no puede guardarse.

mkdirSync recibe dos parámetros:

- Path: Indica dónde queremos crear la carpeta, para esto vamos a utilizar una variable que tiene **Node** llamada _dirname_ que indica la carpeta donde nos encontramos actualmente y el módulo _join_ que nos permite estandarizar la ubicación de carpetas para evitar problemas cuando se utilizan diferentes sistemas operativos. En este caso vamos a crear la carpeta dist.

- Configuraciones: Es necesario utilizar un objeto de configuración que permita crear la carpeta en caso de que no exista dentro de un sub-directorio **{ recursive: true }**:

        fs.mkdirSync(join(__dirname, 'dist'), { recursive: true });

10. Usar el módulo fs.writeFile:

El módulo fs.writeFile permite crear el archivo HTML y necesita tres parámetros

- Path: Vamos a usar la variable **dirname** y el nombre del personaje para nombrar el archivo.
- Content: Es un string con el contenido del archivo, en este caso va a ser nuestro HTML ya con los datos.
- Call back: Esta función la utilizaremos para indicar que el archivo fue creado.

        // La variable character.name debemos transformarla para que el nombre del archivo quede sin espacios y separado por guiones para tener una URL amigable para los motores de búsqueda.

        fs.writeFile(
                join(__dirname, 'dist', `${character.name
                .toLowerCase()
                .split(' ')
                .toLocaleString()
                .replace(',', '-')}.html`),
                HtmlBase,
                () => {
                        console.log('File created');
                },

                );
        })

Y está listo nuestro SSR, este blog fue creado utilizando este SSR y podemos utilizarlo para realizar cosas más complejas, por ejemplo [este post dónde hablo sobre la accesibilidad web.](https://ulisessg.com/como-comenzar-con-la-accesibilidad-web.html)

## El código completo quedaría así

<script src="https://gist.github.com/Ulisessg/fe5997e0a4413adc3db1f75c79a6cab5.js"></script>
