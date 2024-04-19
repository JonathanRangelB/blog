---
title: Hard refresh en mobile
publishDate: 18 April 2024
description: Como poder hacer refresh en dispositivos moviles eliminando la chache.
---

TLDR: escribe esto en la barra del navegador de tu dispositivo móvil:
```html
javascript:location.reload(true)
```

Hace unos días estuve en la encrucijada de forzar la actualizacion de una página hecha en Angular, la cual tiene habilidato el módulo de PWA, por lo cual el service worker es el que se encarga de hacer las actualizaciones.

El motivo principal que tuve en mente era poder cargar mi aplicación web lo más rápido posible en todas las visitas subsecuentes a la primera. Pero por alguna razón un usuario me reportaba que en especifico los dispositivos de apple tenian un problema y no se veian los nuevos modulos de la aplicación en dichos dispositivos, lo cual me resulta muy dificil de validar dado a que no cuento con alguno para hacer las pruebas por mi cuenta, así que me toco trabajar de alguna manera a ciegas.

Mi primer paso fue algo quiza algo obvio pero necesario fue validar que en todos los demas dispositivos la aplicación funcionara correctamente y que el service worker hacia correctamente su trabajo. Efectivamente PC´s y Android´s funcionaban correctamente, los diferentes OS´s no mostraban comportamientos extraños o incorrectos, asi que entre diferentes tecnicas que me tope en foros ninguna parecia funcionar cada vez que le indicaba al usuario que probara la implementacion en el ambiente de staging al cual le di acceso,  asi que despues de 2 semanas de prueba y error llegue a la conclusion que... no supe como resolverlo, hasta hace poco.

Los días pasaron, y de momento la instruccion era no usar dispositivos Apple hasta nuevo aviso, dado a que no era un problema mayor para los usuarios.

Encontre una solucion bastante curiosa la cual desconocia por completo, que puedo ejecutar javascript desde la barra del navegador, si, así como estas leyendo esto, se puede ejecutar código javascript de esta manera, si no me crees has la prueba tu mismo/misma:

```html
javascript:alert("hi")
```
> Nota: si haces copias la linea de código y lo pegas el navegador te va a borrar el prefijo "javascript:", el navegador hace un proceso de sanitización de lo que pegas en la barra de navegación, asi que te recomiendo escribir eso a mano y posteriormente pegar, o terminar de escribirlo.

Con esto en mente, ahora puedo combinar esta manera de ejecutar javascript con las API'S del navegador, en especifico el reload, y aun mas especifico mandandole true como parametro, este último es la parte que forzara la recarga invalidando la chache para obtener todos los datos de la página.

[Gracias a este post de stackoverflow por darme este conocimiento extra.](https://stackoverflow.com/questions/18571213/how-can-i-force-a-hard-reload-in-chrome-for-android)

Esto momentaneamente fue mi solución hasta encontrar una manera correcta de manejar la situación, idealmente con un dispositivo IOS en mis manos, pero por lo pronto esto me parecio bastante curioso.

¿Sabias que esto se podia hacer?