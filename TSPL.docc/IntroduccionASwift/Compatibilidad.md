# Compatibilidad de versiones

Aprende cuáles funcionalidades están disponibles en versiones anteriores del lenguaje.

Este libro describe Swift 5.9,
la versión predeterminada de Swift que se incluye en Xcode 15.
Puedes usar Xcode 15 para compilar *targets*
que han sido desarrollados en Swift 5.9, Swift 4.2, o Swift 4.

<!--
  - test: `swift-version`

  ```swifttest
  >> #if swift(>=5.9.1)
  >>     print("Too new")
  >> #elseif swift(>=5.9)
  >>     print("Just right")
  >> #else
  >>     print("Too old")
  >> #endif
  << Just right
  ```
-->

Al usar Xcode 15 para compilar código Swift 4 y Swift 4.2,
la mayoría de las funcionalidades de Swift 5.9 estarán disponibles.
Dicho esto,
los siguientes cambios solo están disponibles
para código desarrollado en Swift 5.9 o posterior:

- Las funciones que devuelven un tipo opaco requieren el runtime de Swift 5.1.
- La expresión `try?` no introduce un nivel adicional de opcionalidad en las
  expresiones que ya devuelven opcionales.
- Se infiere que las expresiones de inicialización de enteros literales
  grandes son del tipo de entero correcto.
  Por ejemplo, `UInt64(0xffff_ffff_ffff_ffff)` resulta en el valor correcto
  en lugar de desbordarse.

La concurrencia requiere Swift 5.9 o posterior,
y una versión de la biblioteca estándar de Swift
que proporcione los tipos de concurrencia correspondientes.
En las plataformas de Apple,
fija un objetivo de implementación (*deployment target*)
de —por lo menos— iOS 13, macOS 10.15, tvOS 13, o watchOS 6.

Un *target* escrito en Swift 5.9 puede depender
de uno escrito en Swift 4.2 o Swift 4,
y viceversa.
Esto significa que si tienes un proyecto grande
que está dividido en varios *frameworks*,
podrás migrar tu código de Swift 4 a Swift 5.9
un *framework* a la vez.

> Software Beta:
>
> Esta documentación contiene información preliminar sobre una API o tecnología en desarrollo. Esta información está sujeta a cambios, y todo software implementado en conformidad con esta documentación debe ser testeado con el software final del sistema operativo.
>
> Conoce más acerca del uso del [software beta de Apple](https://developer.apple.com/es/support/beta-software/).

<!--
Este archivo fuente es parte del proyecto de código abierto Swift.org

Copyright (c) 2014 - 2023 Apple Inc. y los autores del proyecto Swift
Licenciado bajo la Licencia Apache v2.0 con Runtime Library Exception

Consulta https://swift.org/LICENSE.txt para información sobre la licencia
Consulta https://swift.org/CONTRIBUTING.txt para ver la lista de autores del proyecto Swift
-->
