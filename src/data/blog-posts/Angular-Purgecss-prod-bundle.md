---
title: Angular 17, PrimeNG, PrimeFlex y Purgecss production bundle
publishDate: 18 May 2024
description: Reduce el tamaño de tu css de producción 10X (aproximadamente).
---

TLDR: Visita el GIST donde te dejo toda la configuración que yo uso actualmente 👇:

[AQUÍ.](https://gist.github.com/JonathanRangelB/c0865e8ed9d76a644884c6b3685a7f9e)

He estado trabajando últimamente con un proyecto en Angular 17, y quería hacerme la vida un poco más fácil para maquetar la aplicación y darle un estilo uniforme, y entre las opciones que tengo para angular me decidí por PrimeNG y PrimeFlex, me ha gustado la facilidad de uso y lo bien que se ven las páginas con los componentes que me ofrece PrimeNG.

Por si solo PrimeNG no me da todo lo que necesito en temas de utilerias, es ahí donde entra PrimeFlex, lo malo es que para mi gusto (y para el gusto del builder de angular) es el tamaño resultante del CSS al hacer el build de producción el cual ronda los 506kb para la carga inicial, lo cual es muchísimo, incluso el proceso de build te lo deja saber con un bonito mensaje en tu terminal, ya sea de advertencia o de plano un error dependiendo de tu archivo `angular.json`.

Tampoco quería hacer trampa en mi build haciendo uso de un CDN porque el usuario termina descargando todo el CSS de PrimeFlex de igual forma.

> La propia documentación de PrimeFlex te indica que utilices Purgecss para [reducir las clases de css no utilizadas](https://primeflex.org/installation#productionsize).

Comencé a probar con PurgeCss y me di cuenta de que el archivo se reducía en magnitud de 10x, pero pronto me di cuenta de que algo no estaba bien, el CSS de producción se había roto.

El css que yo veía correctamente al usar `ng serve` no correspondía el css resultante al hacer `ng build`, usar purgecss y verificarlo con `npx http-server`, así que me puse a investigar y no encontré mucho hasta que di con un [post de stackoverflow](https://stackoverflow.com/questions/65554596/purgecss-and-tailwind-css-how-to-preserve-responsive-classes-using-the-command) donde alguien tuvo el mismo problema pero con tailwind, y como la sintaxis es extremadamente similar comencé a hacer pruebas.

Mi problema al usar PurgeCss era que al correr el proceso, este eliminaba varias clases que yo tenía definidas para los distintos tamaños de pantalla, los prefijos `sm:`, `md:`, `xl:` por ejemplo, descubrir que este era mi problema me tomó bastante tiempo.

Para no hacer el post innecesariamente largo te dejo la explicación de la configuración que yo utilizo en mi proyecto, que después de tanta prueba y error es la que mejor me ha funcionado.

> Crea el archivo 'purgecss.config.js' en la raiz de tu proyecto e incluye el siguiente código

```js
module.exports = {
  // content, son los archivos a purgar: como es una SPA solo tengo al index.html.
  // Tambien necesito que purgecss revise todos los archivos .js
  content: ['dist/**/index.html', 'dist/**/*.js'],
  // css, busca todos los archivos de cc en mi carpeta dist
  css: ['dist/**/*.css'],
  // output, es en donde pondra los css resultantes del proceso de purgecss,
  // se deja ./ para que los archivos del paso anterior se sobreescriban y quede la misma estructura
  output: './',
  // Usa expresiones regulares para asegurarte de que las clases de PrimeFlex no se eliminen.
  //standard incluye patrones comunes para las clases de PrimeFlex con diferentes prefijos de tamaño de pantalla.
  safelist: {
    standard: [
      /(^|\s)sm:(\s|$)/,
      /(^|\s)md:(\s|$)/,
      /(^|\s)lg:(\s|$)/,
      /(^|\s)xl:(\s|$)/,
    ],
  },
  // Define cómo PurgeCSS extrae las clases de tus archivos.
  // La expresión regular [\w-/:]+(?<!:) es bastante genérica y debería cubrir la mayoría de las clases de PrimeFlex.
  // incluyendo valores fraccionados como 2.5
  extractors: [
    {
      extractor: (content) => content.match(/[\w-/:.]+(?<!:)/g) || [],
      // Sólo valido html y js, no ts porque yo uso purgecss despues de usar ng build
      extensions: ['html', 'js'],
    },
  ],
};
```

Ahora queda correr `purgecss --config purgecss.config.js` desde tu terminal.

> Nota: si utilizas MessageService inyectado directamente en tus componentes va a causar que los colores del toast invocado se vea de color gris dado a que no hay referencias de css a los colores y purgecss los va descartar, asi que te recomiendo usar el componente "p-toast", "p-messages" o incluir los colores de manera manual en tu tag html.

Recomiendo incluir purgecss a tus scripts en el package.json de tu proyecto:

```js
  "purgecss": "purgecss --config purgecss.config.js",
  "build:purgecss": "ng build --configuration production && npm run purgecss",
```

De momento, esta es la configuración ganadora para mi caso. Quizás tú necesites agregar o quitar algunas líneas en la configuración, dado que mi configuración actual la deje de la manera más general posible para abarcar mis casos de uso en mis aplicaciones de angular.

Espero que te sirva, bye 👋.
