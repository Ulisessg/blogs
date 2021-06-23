# Lo nuevo de React 18

React 18 está pronto a ser lanzado luego de meses sin actualizaciones, en esta ocasión con mejoras en el rendimiento y con APIs interesantes.

## Qué será mejorado en React 18

### Batching

Batching es el proceso en el cual React agrupa múltiples actualizaciones de estado en un solo re-renderizado, por ejemplo, si ejecutas el siguiente código verás que solo se imprime en consola **('render')** la primera vez que se renderiza el componente, y cada vez que haces click solo se imprime **('Click')** y **('render')**

![Ejemplo de batching que actualiza dos estados, uno realiza una suma y es otro cambia el booleano.](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2Fv2%2Fblogs%2Freact%2018%2Freact%20batching%20one%20render.png?alt=media&token=80b22400-f413-46c4-9c3c-b1690295cbd4)

<script src="https://gist.github.com/Ulisessg/6333110dc4c18f62f1a408a8939e65d8.js"></script>

Esto es genial, ya que re-renderizar el componente por cada actualización de estado utilizaría recursos innecesarios, además evita que las actualizaciones se hagan a medias.

Sin embargo **React aún no es consistente en la forma que realiza batching en todas las situaciones**, por ejemplo cuando realizas una petición a una API al hacer click y actualizas el estado cuando la petición se resuelve, se realiza un renderizado por cada estado que actualices, esto ocurre porque React solo realiza batching en eventos síncronos que recibe del navegador (como un click) y no en Promesas.

![Ejemplo de btaching asíncrono, cada vez que se hace click, en consola aparecen dos renders](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2Fv2%2Fblogs%2Freact%2018%2Freact%20batching%20as%C3%ADncrono.png?alt=media&token=54817510-59e5-4636-8f35-6b6cace01aac)

<script src="https://gist.github.com/Ulisessg/0b315adb57b106421984ce41bbca4cbc.js"></script>

Ahora con **React 18** el batching ocurrirá sin importar dónde ocurran las actualizaciones (Promise, setTimeOut, fetch, EventListener, etc).

Esto no tendría que romper ningún componente de función o de clase, sin embargo si llega a generar algún error puedes utilizar [flushSync](https://stackoverflow.com/questions/62725935/what-does-flushsync-do-in-react) que fuerza al componente se re-renderize por cada actualización de estado que añadas (sin embargo es poco recomendable, ya que puede causar bugs).

### La arquitectura interna del Server Side Render (SSR)

Existen 2 formas en las que se construye un sitio en el navegador utilizando React:

- Client Side Render

Donde el usuario recibe un archivo HTML con múltiples archivos JS, cuando los archivos JS son cargados se comienza a construir la UI con los componentes.

- Server Side Render

En el Server Side Render, desde el servidor, se genera un archivo HTML con todos los componentes que utilizamos, haciendo que el usuario pueda ver el contenido del sitio sin tener que esperar a que carguen los archivos JS.

Cuando realizamos Server Side Render se realizan los siguientes pasos en el backstage:

- En el servidor se hace las peticiones a la base de datos con toda la información que necesita el sitio.

- Luego el servidor envía el HTML ya construido con los componentes en la respuesta, sin embargo **el sitio no es interactivo**.

- Luego en el lado del cliente se cargan archivos JavaScript para hacer el sitio interactivo.

- Por último, el HTML estático se vuelve interactivo haciendo un proceso llamado "hydration" (hidratación)

Sin embargo existen 2 problemas con hacer Server Side Render de esta forma:

1. El sitio es interactivo hasta que los archivos JS son descargados y todo el HTML estático es "hidratado", haciendo que en sitios grandes el tiempo de espera sea aún mayor.

2. Todo el sitio tiene que ser construido desde el servidor por lo que hay que esperar a que **todas** las peticiones a la base de datos se resuelvan, haciendo esperar a los usuarios más tiempo para ver nuestro sitio.

**Para resolver esto React 18 añadió 2 nuevos features:**

#### Streaming HTML

El Streaming HTML viene a resolver el problema de que todo tiene que ser construido en el servidor antes de ser enviado a la usuaria.

En palabras sencillas, el Streaming HTML nos permitirá que el usuario reciba nuestro sitio y retrasar el envío de los componentes que hacen peticiones a la base de datos, mientras tanto al usuario se le mostrará un componente de carga ([como un spinner](https://ulisessg.com/gists/loading-spinner)).

Similar a lo que hacemos cuando utilizamos la API [**React.lazy**](https://es.reactjs.org/docs/code-splitting.html#reactlazy).

Para hacer esto solo es necesario envolver el componente que queremos retrasar en un **Suspense** sin necesidad de usar **React.lazy**.

Esto permitirá que las usuarias reciban nuestro sitio de una forma más eficiente enviando y dando más importancia a cierto contenido, por ejemplo lo que aparece en el ViewPort y retrasar lo que no es visible desde el inicio.

#### Hidratación selectiva

La hidratación selectiva permitirá que la hidratación de los componentes sea más dinámica y sobre todo que no pueda ser bloqueada.

En anteriores versiones de React hay que esperar a que todos los componentes y archivos JS carguen para poder comenzar con la "hidratación", esto hace que los componentes que utilizan **React.lazy** o en los que se hizo **code splitting** bloqueen el renderizado y la "hidratación" del sitio, ya que son cargados de forma diferida.

Ahora en React 18 cada componente va a "hidratarse" según vaya cargando, de esta forma se hace más eficiente la "hidratación" del sitio y se eliminarán los bloqueos, sobre todo en sitios grandes.

Además de esto en React 18 los componentes podrán cambiar la prioridad en la que son "hidratados", esto a través de clicks: Cuando la usuaria de click sobre alguno de nuestros componentes se le va a dar mayor cantidad de recursos para "hidratarse" más rápido.

## Qué se añade en React 18

### Start transition

Start transition es una nueva API de React que te permite indicar a React qué actualizaciones de estado son urgentes y cuáles no.

Actualmente React le da la misma importancia a las actualizaciones de estado por igual, sin embargo en ocasiones no todos los estados necesitan actualizarse a una gran velocidad por lo que darles la misma cantidad de recursos hace que nuestra aplicación sea más lenta.

Por ejemplo si tienes un input de búsqueda que va dando sugerencias de completado según lo que escriba la usuaria y este componente tiene que filtrar entre una gran lista de sugerencias o lo hace con una promesa (haciendo una petición por ejemplo), esperar a que la sugerencia aparezca para actualizar el estado y luego la UI hace que la experiencia de usuario empeore.

Esto no solo permitirá mejorar el rendimiento de la aplicación usando menos recursos, también permitirá utilizar menos ancho de banda en redes lentas al realizar menos peticiones en múltiples actualizaciones de estado.

<script src="https://gist.github.com/Ulisessg/5883bc7934acd581326350239384a83a.js"></script>

> Este post es una adaptación al español [de la documentación](https://reactjs.org/blog/2021/06/08/the-plan-for-react-18.html)