# ¿Cómo comenzar con la accesibilidad web?

## La accesibilidad es un tema que todos los desarrolladores deben conocer y que generalmente es ignorado sin razón alguna a pesar de que es un tema muy sencillo.

## Conoce a tus nuevos amigos 🤝

Mejorar la accesibilidad de tu sitio requiere de muy pocas herramientas:

- 🦊 Firefox Accesibility Inspector o Google Lighthouse, ambos ya están instalados en el navegador, tan solo tienes que abrir las herramientas de desarrollador. Muestran las mejoras que puedes hacerle al sitio

- 👀 [NVDA](https://nvda.es/descargas/descarga-de-nvda/) es un lector de pantalla que se complementa muy bien con Firefox aunque puedes usarlo en cualquier navegador.

- ⌨ Las teclas TAB y Shift + TAB, estas teclas te permiten enfocar las diferentes secciones del sitio y permiten que NVDA lea lo que está enfocado.

## Usa HTML "semántico" ✍

La forma más fácil de entender qué es HTML semántico es:

> "Usa la etiqueta que describa lo que se está mostrando o se va a realizar."

Por ejemplo, es más semántico utilizar la etiqueta **<_a_>** que un **<_div_>** con la capacidad de abrir otra página, además de volver más sencillo el proceso de desarrollo permite que el teclado detecte los elementos enfocables como lo son los enlaces.

Si tienes duda de que etiqueta utilizar [puedes visitar esta página](https://www.htmlquick.com/es/reference/tags.html).

## Genera un layout 👩‍🎨

La gran mayoría de sitios web tienen la siguiente estructura

![Es un layout del sitio, arriba hay un menú de navegación, luego está el contenido del sitio y abajo está la información de contacto](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2Flayout.svg?alt=media&token=042c0940-a8b6-4db1-bb01-a9156077234e)

- El menú de navegación debe estar envuelto en la etiqueta <_header_>
- Todo el contenido del sitio debe estar envuelto en la etiqueta <_main_>
- Y la información de contacto o los links de interés deben de estar envueltos en la etiqueta <_footer_>

El contenido del sitio debe estar separado por secciones utilizando la etiqueta <_section_>, solo recuerda no abusar de esta etiqueta y utiliza _HTML semántico_.

Esto ayuda al lector de pantalla detectar en que parte del sitio se encuentra.

## Crea un Skip Link 🐇

Un Skip Link permite que la usuaria/o pueda acceder al contenido que desea sin esfuerzo, es algo realmente sencillo de realizar:

1.  Añade un id descriptivo a las secciones clave de tu sitio:

    ¿Recuerdas el layout generado? pues nos va a ser de mucha utilidad, solo tienes que añadir un id a la etiqueta <_main_> y a cada sección que consideres importante, solo recuerda que **los anuncios NO son importantes.**

2.  Crea un menú de navegación que tenga un enlace por cada **id** creado en el paso anterior y cada enlace debe quedar así:

        <a href="#id-de-la-seccion">Nombre de la sección</a>

    Al dar click sobre ese enlace el foco del lector de pantalla se enfocará en esa sección y comenzará a leerla. Recuerda ordenar los enlaces según que tan importante es la sección.

3.  Añade los enlaces antes del header, esto hará que sea lo primero en ser leído por el lector de pantalla, ahora solo falta ocultarlo a menos que use el la tecla TAB para navegar, existen un montón de maneras de hacerlo y [aquí te dejo una](http://web-accessibility.carnegiemuseums.org/code/skip-link/), solo recuerda 🙅‍♀️ NUNCA utilizar la propiedad "_display: hidden;_" de css porque será invisible para el lector de pantalla.

## Mi parte favorita: molestar a la gente de diseño 😄

Cuando se habla de accesibilidad se suele pensar solo en personas que son ciegas o con algo de dificultad para ver, sin embargo la accesibilidad puede ayudar a más personas con diferentes dificultades, por ejemplo:

- Degeneración macular: Enfermedad ocular que provoca pérdida de la visión.

  ![Representación de cómo se ve la degeneración macular](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2Fdegeneracion-macular.jpg?alt=media&token=fd118bf1-f2d2-4cbc-935e-c2415094f905)

- Pronatopia: Carencia de sensibilidad al color rojo.

- Tritanopia: Capacidad reducida de distinguir entre ciertos colores.

- Deuteranomalia: Dificultad para percibir el color verde.

  ![Logo de Pepsi en diferentes problemas visuales](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2Fcolor-blindness.jpg?alt=media&token=80c8c469-7061-40ef-a574-35fe18288968)

### Algunos consejos que puedes usar o sugerir son:

- Usa colores contrastantes, como el negro y el blanco, si tienes duda de si los colores son contrastantes [puedes consultar en este sitio](https://contrast-ratio.com/#white-on-black).

- En textos el font-size debe estar en medidas rem, esta medida es relativa al font-size que tiene el HTML.

- Añade estilos cuando el foco esté en los elementos enfocables por el teclado o cuando se pasa sobre ellos (_focus_ y _hover_).

- Si no puedes usar otros colores cuando se enfoca sobre un elemento puedes añadir un borde con un color que contraste con el fondo, esto ayuda cuando las personas tienen dificultad para distinguir colores:

  > Enlace sin estilos

  ![Enlace sin estilos](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2Fenlace-sin-estilos.jfif?alt=media&token=2c5852ec-7723-4b0d-9ac7-8f43bc935678)

  > Enlace con estilos

  ![Enlace con estilos](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2Fenlace-con-estilos.png?alt=media&token=fe537286-e538-45d7-89ec-585c847351ee)

## Mejora los formularios

Existen 2 elementos que son obligatorios al crear un formulario:

- Placeholders: Indican al usuario que datos incluir en el input.

- Labels: Indican al lector de pantalla que datos se deben incluir en el input, además se asocian a un input por lo que al navegar con la tecla TAB el foco se irá hacia el input asociado.

- Además es un plus implementar que los inputs de tipo contraseña puedan convertirse en inputs de texto.

  Ya que los lectores de pantalla al estar escribiendo deletrean cada letra tecleada y en los inputs de contraseña solo dicen "asterisco", esto es un problema haciendo login y especialmente a la hora de confirmar tu contraseña.

  La forma más eficiente de hacer esto es poner al lado del input de contraseña un botón "invisible" que al momento de enfocarlo se muestre y cuando se haga click cambie el tipo de input. (recuerda NO usar la propiedad "_display: hidden;_", es mejor idea que el botón se pierda en el fondo)

## Testea 🛠

Nada de lo que dije antes va a servir si no pruebas lo que haces, solo necesitas conocer 3 comandos de NVDA:

- Encenderlo y apagarlo: Esto se hace con las teclas **Control + Alt + N**

- Ir adelante : esto se logra con la tecla **Tab**

- Ir atrás: Esto se hace con las teclas **Shift + Tab**

[Si quieres conocer más shortcuts puedes ir a esta página](https://dequeuniversity.com/screenreaders/nvda-keyboard-shortcuts)

## Inspectores de accesibilidad

### Google Lighthouse

Está disponible en las navegadores Chrome y Edge, lo único que tienes que hacer es abrir las herramientas de desarrollador y seleccionar Lighthouse.

Puede que te aparezcan múltiples categorías para auditar, en este momento solo necesitamos la de accesibilidad así que desmarcamos las demás y damos click a **generar reporte**

Esperas a que termine de evaluar tu sitio y te dirá cómo mejorarlo, tu meta debe ser llegar al 100%

![Prueba de accesibilidad de Lighthouse](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2Flighthouse.png?alt=media&token=e7b4d80b-a2ca-4aa9-bdc2-de2b8d02d47f)

### Firefox Accesibility Inspector

Es más eficiente y completo que Lighthouse, te permite simular problemas visuales e incluso ir componente a componente mostrándote cómo puedes mejorarlo.

![Inspector de accesibilidad de Firefox](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2FBlogs%2FUD%2FFirefox-accesibility.jfif?alt=media&token=fd50a3b9-b12b-4228-824b-f6946258e8a7)
