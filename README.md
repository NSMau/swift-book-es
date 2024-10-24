# The Swift Programming Language en Español

Este repositorio contiene el código fuente de la traducción al español
del libro _The Swift Programming Language_ (a veces abreviado como TSPL),
el cual se encuentra publicado en [swiftbook.es][published]
y ha sido desarollado con [Swift-DocC][docc].

## Contribuciones

Para cambios pequeños,
como correcciones tipográficas y cambios en algunos párrafos,
haz un _fork_ de este repositorio y envía un _pull request_.

El proceso formal de contribución para este documento
aún se encuentra en desarrollo.
Mientras tanto, para cambios más grandes,
inicia un hilo de propuesta en los [foros de Swift][forum]
para discutir tu enfoque e identificar posibles problemas
antes de que inviertas mucho tiempo escribiendo.

El contenido de este libro sigue la [Guía de Estilo de Apple][asg]
y la [guía de estilo de este libro][tspl-style].

Reporta errores sobre el contenido usando la [página de issues][bugs] en Github.

Las discusiones y contribuciones siguen el [Código de Conducta de Swift][conduct].

Para más información, visita [Contribuyendo a The Swift Programming Language][contributing].

[asg]: https://help.apple.com/applestyleguide/
[bugs]: https://github.com/algoritmau/swift-book-es/issues
[conduct]: https://www.swift.org/code-of-conduct
[contributing]: /CONTRIBUTING.md
[forum]: https://forums.swift.org/c/swift-documentation/92
[tspl-style]: /Style.md
[published]: https://swiftbook.es
[docc]: https://github.com/apple/swift-docc

## Compilación

Ejecuta `docc preview TSPL.docc`
en el directorio raíz de este repositorio.

Luego de ejecutar DocC, abre el enlace que `docc` arroja
para visualizar una vista previa local en tu navegador.

> Nota:
>
> Si instalaste DocC descargando una cadena de herramientas de Swift.org,
> `docc` se encuentra en `usr/bin/`,
> relativo a la ruta de instalación de la cadena de herramientas.
> Asegúrate de que la variable de entorno `PATH` de tu shell
> incluya ese directorio.
>
> Si instalaste DocC descargando Xcode,
> ejecuta `xcrun docc preview TSPL.docc` en su lugar.
