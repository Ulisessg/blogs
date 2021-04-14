# SEO - Lo básico

El SEO (posicionamiento en buscadores) son las acciones que ayudan a tu (como Google o Bing por ejemplo) muestren a las personas nuestro sitio cuándo buscan el problema que buscan solucionar, por ejemplo si buscas [cómo comenzar con la accesibilidad web](https://ulisessg.com/como-comenzar-con-la-accesibilidad-web).

## Comenzar a mejorar el SEO de tu sitio es muy sencillo, solo debes revisar lo siguiente:

## Meta etiquetas

Las meta etiquetas son etiquetas HTML que le dan información extra al motor de búsqueda, por ejemplo una descripción de lo que trata tu sitio o ¿Alguna vez has visto que al compartir artículos en una red social se puede ver una imagen y una descripción?, las meta tags le dicen al motor de búsqueda (o red social):

> Cuando alguien vea o comparta esta página quiero que se muestre esta foto, esta descripción y el nombre del sitio.

Las meta etiquetas tienen 2 valores:

- name: Es el nombre de la meta etiqueta
- description: Es el contenido de la meta etiqueta

**Estructura básica de un meta tag:**

![Estructura básica de un meta tag, el código HTML es así: <meta name="twitter:title" content="El mejor título jamás existente" />](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2Fmeta_tags_structure.png?alt=media&token=b90a0e84-d12c-46a1-a76c-a6d4c523859a)

**Este meta tag hará que cuando se comparta tu página en Twitter se vea "The best title ever"**

### Los meta tags básicos que necesitas son:

- Url canónica: Sirve en los casos en los que el sitio tenga contenido similar a otras páginas, así el motor de búsqueda sabe que es una página original.

      <link rel="canonical" href="https://ulisessg.com/seo-basico"/>

- description: Es una descripción del contenido del sitio, por ejemplo un resumen de lo que hablas en el post.

- keywords: Son palabras clave que identifican a tu sitio o post, por ejemplo si en tu post hablas sobre Server Side Render debes incluir el keyword SSR, cada keyword debe estar separado por una coma.

### Meta etiquetas para Twitter:

- twitter:title: Es el título que aparecerá cuando el sitio sea compartido en Twitter.

- twitter:description: Es la descripción que aparecerá cuando se comparta el sitio en Twitter.

- twitter:image: Es la imagen que aparecerá en el post donde se comparta el sitio en Twitter.

- twitter:card: Es el tamaño que debe tener el card (imagen, titulo y descripción), la mayor parte del tiempo _summary_large_image_ es el tamaño necesario.

- twitter:site: Debe ser tu @ de Twitter.

- twitter:creator: Debe ser tu @ de Twitter.

### Meta etiquetas para cualquier otra red social o sitio:

- og:site_name: Es el nombre de tu sitio, por ejemplo si tu sito es Facebook ese sería el valor.

- og:locale: Indica el idioma de tu sitio y el país del que eres, por ejemplo: es_MX sería español-mexico.

- og:type: Indica el tipo de contenido de tu sitio, por ejemplo: article(articulo), website(sitio web).

- og:title: Es el título que aparecerá cuándo se comparta tu sitio en otro lugar que no sea Twitter.

- og:description: Es una descripción del contenido del sitio, por ejemplo un resumen de lo que hablas en el post.

- og:image: Es la imagen que aparecerá en el post donde se comparta el sitio.

- og:url: Indica cuál es la url de tu sitio.

### Así se verían las meta etiquetas en tu archivo HTML:

![Todos los meta tags](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2Fseo_basico.png?alt=media&token=befd0ba2-f0c7-4678-9328-3183e0ad6220)

## Si deseas copiarlo aquí está el código:

<script src="https://gist.github.com/Ulisessg/35c352b5fae51dbfe2a35f1f912a6fd0.js"></script>

## robots.txt

Los robots.txt es un archivo con extensión txt que debemos incluir en nuestro hosting, igual que los archivos HTML.

La forma más fácil de entender los robots.txt es:

> Motores de búsqueda, tienen acceso a estas urls y archivos, a estas otras no.

![Meme del guardia](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2Fmeme_guardia.jpg?alt=media&token=1dd16f98-0ad1-4ee6-8576-af66fe80f5cd)

Esto es útil si por ejemplo si no queremos que una página con contenido premium sea rastreada, aquí es dónde lo indicaremos. Esto NO significa que las personas no puedan entrar, esto significa que cuando busquen tu sitio esa página no aparecerá en los resultados de búsqueda.

Para indicar a qué carpetas puede acceder usamos **Allow** para indicar las url a las que puede entrar y **Disallow** para indicar que NO puede entrar.

### Ejemplo de un archivo robots.txt:

<script src="https://gist.github.com/Ulisessg/4b198281a865e6d6842615266038972f.js"></script>

Esto indica que los motores de busqueda pueden rastrear cualquier url excepto las que comienzan con: /premium.

**Advertencia:** Si tu sito utiliza frameworks de JavaScript como React y indicas que los motores no pueden acceder a la url dónde están tus archivos de JavaScript el motor de busqueda no podrá ejecutar tu sitio por lo que no encontrará contenido y no le dará importancia a tu sitio.

## Crea enlaces a tus páginas

Es posible hacer que Google rastree tus páginas de dos formas:

1. Con un mapa de sitio.
2. Creando enlaces entre tus páginas, por ejemplo en tu Header crea un menú de navegación con un enlace a tus otros sitios.

Yo recomiendo comenzar con la segunda opción, crear una página que enlace a todos tus posts, no solo te ayudará a mejorar tu marca persona, también facilita el rastreo de tus sitios.

Esto ya que cuando Google inspecciona tu sitio y encuentra un enlace lo registra, entre más veces aparezca un enlace en diferentes sitios más arriba aparecerá en los resultados de búsqueda.

## Haz Server side render (SSR)

El server side render es hacer que nuestro servidor cree el contenido del sitio antes de enviarlo al cliente, por el contrario el client side render es hacer que el contenido se muestre una vez el cliente terminó de recibir el sitio.

El SSR tiene dos principales ventajas sobre el _client side render_:

1. La velocidad de carga

El principal inconveniente del _renderizado del lado del cliente_ es el tiempo que se tarda en mostrar contenido ya que necesitamos que todos los archivos sean descargados, luego se muestra un HTML con una pantalla de carga, mientras tanto de fondo se está generando nuestro sitio y cuando por fin termina podemos usar el sitio, esto suele ser demasiado tardado sobre todo si realizamos peticiones a una API para obtener el contenido.

Por el contrario el SSR se encarga de generar todo el contenido del sitio y nos entrega el sitio ya construido, aunque sin ser interactivo ya que de fondo se descargan los archivos JavaScript, pero desde el principio podemos ver todo el contenido.

2. SEO

A pesar de que Google sí ejecuta JavaScript al momento de rastrear páginas, no todos los motores funcionan de la misma manera.

El proceso por el cual los motores de búsqueda encuentran nuestras aplicaciones es: Primero abren nuestro sitio sin ejecutar JavaScript para ver su contenido, buscar palabras clave, buscar enlaces y luego de un tiempo (que depende del motor de búsqueda) se ejecuta JavaScript, este tiempo no está definido e incluso puede que nunca se realice ya que algunos motores de búsqueda **NO** pueden ejecutar JavaScript, esto es problemático si utilizamos React, Angular ó Vue.js ya que puede que el motor de búsqueda nunca podrá ver el contenido de nuestro sitio.

La ventaja de SSR es que los motores desde el principio pueden acceder al contenido del sitio y así rastrearlo mucho mejor y posicionarlo por encima de otros sitios.

## Evaluar el rastreo de tus páginas

Puedes revisar que páginas de tu sitio están siendo rastreadas por Google buscando en Google site:nombreDeTuSitio.com, por ejemplo cuando evalúo mi sitio busco en Google: site:ulisessg.com

Además puedes utilizar [Google Search Console](https://search.google.com/search-console/about?hl=es) que además de mostrarte cómo va el SEO de tu sitio también te dice de dónde vienen las visitas y cuántas veces han entrado a las diferentes páginas y cómo mejorar el SEO de las mismas.

Por último puedes solicitar a Google que analice tu sitio para que sea indexado en Google, recuerda tener una página que recopile tus posts o asegurate de tener enlaces a tus sitios para que sean rastreables.

## Utiliza HTML semántico

La mejor forma de entender qué es el HTML semántico es:

> "Usa la etiqueta que describa lo que se está mostrando o se va a realizar."

Por ejemplo, es más semántico utilizar la etiqueta **<_a_>** que un **<_div_>** con la capacidad de abrir otra página, además de volver más sencillo el proceso de desarrollo permite que el teclado detecte los elementos enfocables como lo son los enlaces y le ayuda a entender al motor de busqueda que es un enlace.

Además no olvides utilizar la etiqueta **title** ya que da información de lo que trata tu sitio.

Si tienes duda de que etiqueta utilizar [puedes visitar esta página](https://www.htmlquick.com/es/reference/tags.html).

## Utiliza urls memorables:

Al momento de compartir tu sitio con otras personas lo puedan recordar fácilmente, además de que permite seguir añadiendo palabras clave para que el motor de busqueda sepa más del sitio.

## Analizar las cards al compartir

Es posible analizar cómo se verá la publicación en la que compartas tu sitio en diferentes redes sociales, por ejemplo:

- [Inspector de LinkedIn](https://www.linkedin.com/post-inspector/inspect/)
- [Inspector de Facebook](https://developers.facebook.com/tools/debug/)
- [Inspector de Twitter](https://cards-dev.twitter.com/validator)

Solo debes ingresar la url de la página que quieres inspeccionar y ten en cuenta que debes tener una cuenta en cada sito para poder utilizar el inspector.
