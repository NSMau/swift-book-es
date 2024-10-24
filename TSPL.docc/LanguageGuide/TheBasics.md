# Fundamentos

Trabaja con tipos comunes de datos y escribe sintaxis básica.

Swift es un lenguaje de programación para el desarrollo de aplicaciones
para iOS, macOS, watchOS, y tvOS.
Si tienes experiencia desarrollando en C u Objective-C,
muchas partes de Swift te resultarán familiares.

Swift proporciona sus propias versiones de todos los tipos fundamentales de C y Objective-C,
incluyendo `Int` para enteros, `Double` y `Float` para valores de coma flotante,
`Bool` para valores booleanos y `String` para datos textuales.
Swift también ofrece poderosas versiones
de los tres tipos principales de colecciones: `Array`, `Set`, y `Dictionary`,
como se describe en <doc:CollectionTypes>.

Al igual que C, Swift utiliza variables para almacenar y referenciar valores
mediante un nombre de identificación.
Swift también hace un uso extensivo de variables cuyos valores no pueden ser modificados.
Dichas variables se conocen como constantes
y son mucho más poderosas que las constantes en C.
En Swift, las constantes son utilizadas
para hacer que el código resulte más seguro y más claro en la intención
cuando se trabaja con valores que no necesitan cambiar.

Además de los tipos conocidos,
Swift introduce tipos avanzados que no se encuentran en Objective-C,
como las tuplas.
Las tuplas te permiten crear y pasar conjuntos de valores.
Puedes utilizar una tupla para hacer que una función devuelva varios valores
como un único valor compuesto.

Swift también cuenta con tipos opcionales,
los cuales lidian con la ausencia de un valor.
Los opcionales indican que «*existe* un valor, y es igual a x»
o «*no existe* un valor en lo absoluto».
Usar opcionales es similar a usar `nil` con punteros en Objective-C,
pero funcionan para cualquier tipo, no solo para las clases.
Los opcionales no solo son más seguros y significativos
que los punteros `nil` en Objective-C,
sino que también forman parte esencial de muchas de las funciones más poderosas de Swift.

Swift es un lenguaje con *seguridad de tipos*,
lo que significa que el lenguaje te ayuda a tener claridad
con respecto a los tipos de valores con los que puede trabajar tu código.
Si una parte de tu código requiere un `String`,
la seguridad de tipos te impedirá pasar un `Int` por error.
Del mismo modo, la seguridad de tipos evitará que pases, accidentalmente,
un `String` opcional a un fragmento de código que requiere un `String` no opcional.
La seguridad de tipos te ayuda a detectar y corregir errores lo antes posible
en el proceso de desarrollo.

## Constantes y variables

Las constantes y variables asocian un nombre
(como `numeroMaximoDeIntentosDeInicioDeSesion` o `mensajeDeBienvenida`)
con un valor de un tipo particular
(como el número `10` o la cadena `"Hola"`).
El valor de una *constante* no se puede cambiar una vez que se asigna,
mientras que a una *variable* puede asignársele un valor diferente más adelante.

### Declaración de constantes y variables

Las constantes y variables deben ser declararadas antes de ser utilizadas.
Para declarar constantes, se usa la palabra clave `let`,
mientras que las variables se declaran con la palabra clave `var`.
Acá tenemos un ejemplo de cómo se pueden utilizar las constantes y variables
para hacer seguimiento del número de intentos de inicio de sesión que ha realizado un usuario:

```swift
let numeroMaximoDeIntentosDeInicioDeSesion = 10
var intentoActualDeInicioDeSesion = 0
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> let maximumNumberOfLoginAttempts = 10
  -> var currentLoginAttempt = 0
  ```
-->

Este código puede leerse como:

«Declara una nueva constante llamada `numeroMaximoDeIntentosDeInicioDeSesion`,
y asígnale un valor de `10`.
Luego, declara una nueva variable llamada `intentoActualDeInicioDeSesion`,
y asígnale un valor inicial de `0`.»

En este ejemplo,
el número máximo de intentos de inicio de sesión permitidos se declara como una constante,
porque el valor máximo nunca cambia.
El contador actual de intentos de inicio de sesión se declara como una variable,
porque este valor debe incrementarse después de cada intento de inicio de sesión fallido.

Puedes declarar múltiples constantes o variables en una sola línea,
separadas por comas:

```swift
var x = 0.0, y = 0.0, z = 0.0
```

<!--
  - test: `multipleDeclarations`

  ```swifttest
  -> var x = 0.0, y = 0.0, z = 0.0
  >> print(x, y, z)
  << 0.0 0.0 0.0
  ```
-->

> Nota: Si un valor almacenado en tu código nunca cambia,
> siempre debes declararlo como una constante usando la palabra clave `let`.
> Utiliza variables solo para almacenar valores que puedan cambiar.

### Anotaciones de tipo

Al declarar una constante o variable, puedes proveer una *anotación de tipo*
para especificar el tipo de valores que dicha constante o variable puede almacenar.
Escribe una anotación de tipo colocando dos puntos (`:`)
después del nombre de la constante o variable,
seguido de un espacio, seguido del nombre del tipo a especificar.

En este ejemplo se agrega una anotación de tipo para una variable llamada `mensajeDeBienvenida`,
para indicar que la variable puede almacenar valores de tipo `String`:

```swift
var mensajeDeBienvenida: String
```

<!--
  - test: `typeAnnotations`

  ```swifttest
  -> var welcomeMessage: String
  ```
-->

Los dos puntos en la declaración significan *«…de tipo…»*,
por lo que el código anterior se puede leer como:

«Declara una variable llamada `mensajeDeBienvenida` que sea de tipo `String`.»

La frase *«de tipo `String`»* significa «puede almacenar cualquier valor de tipo `String`».
Piensa en ello como *«el tipo de cosa»* (o *«la clase de cosa»*) que se puede almacenar.

Ahora, a la variable `mensajeDeBienvenida` se le puede asignar cualquier cadena como valor
sin ningún problema:

```swift
mensajeDeBienvenida = "Hola"
```

<!--
  - test: `typeAnnotations`

  ```swifttest
  -> welcomeMessage = "Hello"
  >> print(welcomeMessage)
  << Hello
  ```
-->

Puedes definir múltiples variables del mismo tipo en una sola línea,
separadas por comas, con una única definición de tipo después del nombre de la última variable:

```swift
var rojo, verde, azul: Double
```

<!--
  - test: `typeAnnotations`

  ```swifttest
  -> var red, green, blue: Double
  ```
-->

> Nota: En la práctica, resulta inusual la necesidad de escribir anotaciones de tipo.
> Si al definir una constante o variable, proporcionas un valor inicial para la misma,
> Swift casi siempre podrá inferir el tipo que se utilizará para esa constante o variable,
> como se describe en <doc:TheBasics#Seguridad-de-tipos-e-inferencia-de-tipos>.
> En el ejemplo anterior, no se provee ningún valor inicial,
> por lo que el tipo de la variable `mensajeDeBienvenida`
> se especifica con una anotación de tipo en lugar de inferirse de un valor inicial.

### Nombrar constantes y variables

Los nombres de constantes y variables pueden incluir casi cualquier caracter, incluyendo caracteres Unicode:

```swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "perrogato"
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> let π = 3.14159
  -> let 你好 = "你好世界"
  -> let 🐶🐮 = "dogcow"
  ```
-->

Los nombres de constantes y variables no pueden
contener caracteres de espacio en blanco, símbolos matemáticos, flechas,
valores escalares Unicode de uso privado ni caracteres de dibujo de líneas y recuadros.
Tampoco pueden comenzar con un número, aunque estos se pueden incluir en otras partes del nombre.

Una vez que has declarado una constante o variable de cierto tipo,
no podrás volver a declararla con el mismo nombre
ni cambiarla para almacenar valores de un tipo diferente.
Tampoco es posible convertir una constante en una variable
o una variable en una constante.

> Nota: Si necesitas darle a una constante o variable el mismo nombre
> que una palabra clave reservada de Swift,
> encierra la palabra clave con comillas invertidas (`` ` ``)
> al usarla como nombre de una variable o constante.
> Sin embargo, evita usar palabras clave como nombres
> a menos que no tengas ninguna otra opción en lo absoluto.

Puedes cambiar el valor de una variable existente a otro valor de un tipo compatible.
En este ejemplo, el valor de `recepcionAmigable` cambia de `"¡Hola!"` a `"Bonjour!"`:

```swift
var recepcionAmigable = "¡Hola!"
recepcionAmigable = "Bonjour!"
// Ahora, recepcionAmigable es "Bonjour!"
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> var friendlyWelcome = "Hello!"
  -> friendlyWelcome = "Bonjour!"
  /> friendlyWelcome is now \"\(friendlyWelcome)\"
  </ friendlyWelcome is now "Bonjour!"
  ```
-->

A diferencia de una variable,
el valor de una constante no se puede cambiar después de haber sido asignado.
Intentar cambiarlo, resultará en un error al momento de compilar el código:

```swift
let nombreDelLenguaje = "Swift"
nombreDelLenguaje = "Swift++"
// Esto reporta un error al compilar: nombreDelLenguaje is a 'let' constant
```

<!--
  - test: `constantsAndVariables_err`

  ```swifttest
  -> let languageName = "Swift"
  -> languageName = "Swift++"
  // This is a compile-time error: languageName cannot be changed.
  !$ error: cannot assign to value: 'languageName' is a 'let' constant
  !! languageName = "Swift++"
  !! ^~~~~~~~~~~~
  !! /tmp/swifttest.swift:1:1: note: change 'let' to 'var' to make it mutable
  !! let languageName = "Swift"
  !! ^~~
  !! var
  ```
-->

### Impresión de Constantes y Variables

Puedes imprimir el valor actual de una constante o variable mediante la función `print(_:separator:terminator:)`:

```swift
print(recepcionAmigable)
// Imprime "Bonjour!"
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> print(friendlyWelcome)
  <- Bonjour!
  ```
-->

La función `print(_:separator:terminator:)`
es una función global que imprime uno o más valores
a una salida apropiada.
En Xcode, por ejemplo,
la función `print(_:separator:terminator:)` imprime su salida en el panel de consola de Xcode.
Los parámetros `separator` y `terminator` tienen valores predeterminados,
por lo que puedes omitirlos al llamar esta función.
Por defecto, la función termina la línea que imprime agregando un salto de línea.
Para imprimir un valor sin un salto de línea después del mismo,
pasa una cadena vacía como `terminator`.
Por ejemplo, `print(someValue, terminator: "")`.
Para más información sobre parámetros con valores predeterminados,
consulta <doc:Functions#Parámetros-con-valores-predeterminados>.

<!--
  - test: `printingWithoutNewline`

  ```swifttest
  >> let someValue = 10
  -> print(someValue, terminator: "")
  -> print(someValue)
  << 1010
  ```
-->

<!--
  QUESTION: have I referred to Xcode's console correctly here?
  Should I mention other output streams, such as the REPL / playgrounds?
-->

<!--
  NOTE: this is a deliberately simplistic description of what you can do with print().
  It will be expanded later on.
-->

Usa *interpolación de cadenas* para insertar el nombre de una constante o variable
a manera de *placeholder* en una cadena más larga
y solicitarle a Swift que le reemplace con el valor actual de esa constante o variable.
Encierra el nombre entre paréntesis y precédelo con una barra inclinada invertida (`\`)
para indicar que es un *placeholder*:

```swift
print("¡El valor actual de recepcionAmigable es \(recepcionAmigable)!")
// Imprime "¡El valor actual de recepcionAmigable es Bonjour!"
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> print("The current value of friendlyWelcome is \(friendlyWelcome)")
  <- The current value of friendlyWelcome is Bonjour!
  ```
-->

> Nota: Todas las opciones que se pueden utilizar con la interpolación de cadenas,
> se describen en <doc:StringsAndCharacters#Interpolación-de-cadenas>.

## Comentarios

Usa comentarios para incluir texto no ejecutable en tu código,
como una nota o un recordatorio personal.
El compilador de Swift ignora los comentarios al momento de compilar el código.

Los comentarios en Swift son muy similares a los comentarios en C.
Los comentarios de una sola línea comienzan con dos barras inclinadas (`//`):

```swift
// Esto es un comentario.
```

<!--
  - test: `comments`

  ```swifttest
  -> // This is a comment.
  ```
-->

Los comentarios de varias líneas comienzan con una barra inclinada seguida de un asterisco (`/*`)
y terminan con un asterisco seguido de una barra inclinada (`*/`):

```swift
/* Esto también es un comentario,
pero está escrito en varias líneas. */
```

<!--
  - test: `comments`

  ```swifttest
  -> /* This is also a comment
     but is written over multiple lines. */
  ```
-->

A diferencia de los comentarios de varias líneas en C,
los comentarios de varias líneas en Swift se pueden anidar
dentro de otros comentarios de varias líneas.
Puedes escribir comentarios anidados iniciando un bloque de comentarios de varias líneas
y luego iniciando un segundo comentario de varias líneas dentro del primer bloque.
A continuación, se cierra el segundo bloque, seguido del primer bloque:

```swift
/* Este es el comienzo del primer comentario de varias líneas.
    /* Este es el segundo comentario de varias líneas (anidado). /*
Este es el final del primer comentario de varias líneas. */
```

<!--
  - test: `comments`

  ```swifttest
  -> /* This is the start of the first multiline comment.
        /* This is the second, nested multiline comment. */
     This is the end of the first multiline comment. */
  ```
-->

Los comentarios anidados de varias líneas te permiten comentar grandes bloques de código
de forma rápida y sencilla,
incluso si el código ya contiene comentarios de varias líneas.

## Punto y coma

A diferencia de muchos otros lenguajes,
Swift *no* requiere que escribas un punto y coma (`;`) después de cada sentencia en tu código,
aunque puedes hacerlo si así lo deseas.
Sin embargo, *sí* se requiere si quisieras escribir múltiples declaraciones en una sola línea:

```swift
let gato = "🐱"; print(gato)
// Imprime "🐱"
```

<!--
  - test: `semiColons`

  ```swifttest
  -> let cat = "🐱"; print(cat)
  <- 🐱
  ```
-->

## Enteros

Los *enteros* son números completos sin componente fraccionario,
como `42` y `-23`.
Los números enteros pueden tener signo (positivo, cero, o negativo)
o no tenerlo (positivo o cero).

Swift proporciona enteros con y sin signo en diversos formatos: 8, 16, 32, y 64 bits.
Estos enteros siguen una convención de nomenclatura similar a la de C,
de manera que un entero sin signo, de 8 bits es de tipo `UInt8`
y un entero con signo, de 32 bits es de tipo `Int32`.
Como todos los tipos en Swift, estos tipos enteros tienen nombres en mayúscula.

### Límites de enteros

Puedes acceder a los valores mínimo y máximo de cada tipo de entero
mediante las propiedades `min` y `max`:

```swift
let valorMinimo = UInt8.min  // valorMinimo es igual a 0 y es de tipo UInt8
let valorMaximo = UInt8.max  // valorMaximo es igual a 255 y es de tipo UInt8
```

<!--
  - test: `integerBounds`

  ```swifttest
  -> let minValue = UInt8.min  // minValue is equal to 0, and is of type UInt8
  -> let maxValue = UInt8.max  // maxValue is equal to 255, and is of type UInt8
  >> print(minValue, maxValue)
  << 0 255
  ```
-->

Los valores de estas propiedades son del tipo numérico de longitud correcta
(como `UInt8` en el ejemplo anterior)
y, por lo tanto, pueden ser usados en expresiones junto con otros valores del mismo tipo.

### Int

En la mayoría de los casos,
no necesitas elegir un tamaño específico de entero para utilizar en tu código.
Swift proporciona un tipo entero adicional, `Int`,
el cual tiene el mismo tamaño
que el tamaño nativo de una palabra en la plataforma en la que se ejecuta el código:

- En una plataforma de 32 bits, `Int` tiene el mismo tamaño que `Int32`.
- En una plataforma de 64 bits, `Int` tiene el mismo tamaño que `Int64`.

A menos que tengas que trabajar con un tamaño específico de entero,
usa siempre `Int` para valores enteros en tu código.
Esto ayuda con la coherencia e interoperabilidad del código.
Incluso en plataformas de 32 bits, `Int` puede almacenar cualquier valor entre `-2,147,483,648` y `2,147,483,647`,
y es lo suficientemente grande para muchos rangos de enteros.

### UInt

Swift también proporciona un tipo de número entero sin signo, `UInt`,
el cual tiene el mismo tamaño
que el tamaño nativo de una palabra en la plataforma en la que se ejecuta el código:

- En una plataforma de 32 bits, `UInt` tiene el mismo tamaño que `UInt32`.
- En una plataforma de 64 bits, `UInt` tiene el mismo tamaño que `UInt64`.

> Nota: Usa `UInt` sólo cuando necesites, específicamente,
> un tipo de entero sin signo con el mismo tamaño
> que el tamaño nativo de una palabra en la plataforma en la que se ejecuta el código.
> Si este no es el caso, es preferible usar `Int`,
> incluso cuando se sabe que los valores que se almacenarán no son negativos.
> Un uso consistente de `Int` para valores enteros ayuda con la interoperabilidad del código,
> evita la necesidad de convertir entre diferentes tipos de números,
> y coincide con la inferencia de tipo enteros, como se describe en
> <doc:TheBasics#Seguridad-de-tipos-e-inferencia-de-tipos>.

## Números de punto flotante

Los *números de punto flotante* son números con un componente fraccionario,
como `3.14159`, `0.1`, y `-273.15`.

Los tipos de punto flotante pueden representar un rango de valores mucho más amplio
que los tipos enteros
y pueden almacenar números mucho más grandes o más pequeños
que los que se pueden almacenar en un `Int`.
Swift proporciona dos tipos de números de punto flotante con signo:

- `Double` representa un número de punto flotante de 64 bits.
- `Float` representa un número de punto flotante de 32 bits.

> Nota: `Double` tiene una precisión de al menos 15 dígitos decimales,
> mientras que la precisión de `Float` puede ser de tan solo 6 dígitos decimales.
> El tipo de punto flotante apropiado a utilizar depende de la naturaleza y el rango de
> valores con los que necesites trabajar en tu código.
> En situaciones en las que cualquiera de los dos tipos sea apropiado, es preferible usar `Double`.

<!--
  TODO: Explicitly mention situations where Float is appropriate,
  such as when optimizing for storage size of collections?
-->

<!--
  TODO: mention infinity, -infinity etc.
-->

## Seguridad de tipos e inferencia de tipos

Swift es un lenguaje con seguridad de tipos.
Un lenguaje con seguridad de tipos te incita a ser claro con respecto a
los tipos de valores con los que puede trabajar tu código.
Si parte de tu código requiere un `String`, no podrás pasarle un `Int` por error.

Dado que cuenta con seguridad de tipos,
Swift realiza *verificaciones de tipos* (*type checks*) al compilar tu código
y marca como error cualquier tipo que no coincida.
Esto te permite detectar y corregir errores lo antes posible en el proceso de desarrollo.

La verificación de tipos te ayuda a evitar errores al trabajar con diferentes tipos de valores.
Sin embargo, esto no quiere decir que tengas que especificar el tipo
de cada constante y variable que declares.
Si no especificas el tipo de valor que necesitas,
Swift usa la *inferencia de tipos* para determinar el tipo apropiado.
La inferencia de tipos le permite a un compilador deducir,
de manera automática, el tipo de una expresión en particular al compilar tu código,
simplemente examinando los valores que proporcionas.

Debido a la inferencia de tipos, Swift requiere muchas menos declaraciones de tipos
que lenguajes como C u Objective-C.
Las constantes y las variables siguen teniendo un tipo explícito,
pero tú llevas a cabo gran parte del trabajo de especificar dicho tipo.

La inferencia de tipos es particularmente útil
al declarar una constante o variable con un valor inicial.
Esto, a menudo, se hace asignando un *valor literal* (o *literal*)
a la constante o variable en el momento en que se declara.
(Un valor literal es un valor que aparece directamente en tu código fuente,
como `42` y `3.14159` en los ejemplos siguientes).

Por ejemplo, si asignas un valor literal de `42` a una nueva constante,
sin especificar de qué tipo es,
Swift infiere que quieres que la constante sea de tipo `Int`,
porque la has inicializado con un número que parece un entero:

```swift
let significadoDeLaVida = 42
// Se infiere que significadoDeLaVida es de tipo Int
```

<!--
  - test: `typeInference`

  ```swifttest
  -> let meaningOfLife = 42
  // meaningOfLife is inferred to be of type Int
  >> print(type(of: meaningOfLife))
  << Int
  ```
-->

Del mismo modo, si no especificas un tipo para un literal de punto flotante,
Swift infiere que quieres crear un `Double`:

```swift
let pi = 3.14159
// Se infiere que pi es de tipo Double
```

<!--
  - test: `typeInference`

  ```swifttest
  -> let pi = 3.14159
  // pi is inferred to be of type Double
  >> print(type(of: pi))
  << Double
  ```
-->

Swift siempre escoge `Double` (en lugar de `Float`)
al momento de inferir el tipo de números de punto flotante.

Si combinas literales enteros y de punto flotante en una expresión,
se inferirá un tipo `Double` a partir del contexto:

```swift
let otroPi = 3 + 0.14159
// Se infiere que otroPi también es de tipo Double
```

<!--
  - test: `typeInference`

  ```swifttest
  -> let anotherPi = 3 + 0.14159
  // anotherPi is also inferred to be of type Double
  >> print(type(of: anotherPi))
  << Double
  ```
-->

El valor literal de `3` no tiene un tipo explícito en sí mismo,
por lo que se infiere un tipo de salida adecuado `Double`
a partir de la presencia de un literal de punto flotante como parte de la suma.

## Literales numéricos

Los literales enteros se pueden escribir como:

- Un número *decimal*, sin prefijo
- Un número *binario*, con el prefijo `0b`
- Un número *octal*, con el prefijo `0o`
- Un número *hexadecimal*, con el prefijo `0x`

Todos estos literales enteros tienen un valor decimal de `17`:

```swift
let enteroDecimal = 17
let enteroBinario = 0b10001       // 17 en notación binaria
let enteroOctal = 0o21            // 17 en notación octal
let enteroHexadecimal = 0x11      // 17 en notación hexadecimal
```

<!--
  - test: `numberLiterals`

  ```swifttest
  -> let decimalInteger = 17
  -> let binaryInteger = 0b10001       // 17 in binary notation
  -> let octalInteger = 0o21           // 17 in octal notation
  -> let hexadecimalInteger = 0x11     // 17 in hexadecimal notation
  >> print(binaryInteger, octalInteger, hexadecimalInteger)
  << 17 17 17
  ```
-->

Los literales de punto flotante pueden ser decimales (sin prefijo)
o hexadecimales (con el prefijo `0x`).
Siempre deben tener un número (o número hexadecimal) a ambos lados del punto decimal.
Los flotantes decimales también pueden tener un *exponente* opcional,
representado por una `e` mayúscula o minúscula;
los flotantes hexadecimales deben tener un exponente,
representado por una `p` mayúscula o minúscula.

<!--
  - test: `float-required-vs-optional-exponent-err`

  ```swifttest
  -> let hexWithout = 0x1.5
  !$ error: hexadecimal floating point literal must end with an exponent
  !! let hexWithout = 0x1.5
  !!                       ^
  ```
-->

<!--
  - test: `float-required-vs-optional-exponent`

  ```swifttest
  -> let hexWith = 0x1.5p7
  -> let decimalWithout = 0.5
  -> let decimalWith = 0.5e7
  ```
-->

Para números decimales con un exponente `x`,
se multiplica el número base por 10ˣ:

- `1.25e2` significa 1.25 x 10², o `125.0`.
- `1.25e-2` significa 1.25 x 10⁻², o `0.0125`.

Para números hexadecimales con un exponente `x`,
se multiplica el número base por 2ˣ:

- `0xFp2` significa 15 x 2², o `60.0`.
- `0xFp-2` significa 15 x 2⁻², o `3.75`.

Todos estos literales de punto flotante tienen un valor decimal de `12.1875`:

```swift
let doubleDecimal = 12.1875
let doubleExponente = 1.21875e1
let doubleHexadecimal = 0xC.3p0
```

<!--
  - test: `numberLiterals`

  ```swifttest
  -> let decimalDouble = 12.1875
  -> let exponentDouble = 1.21875e1
  -> let hexadecimalDouble = 0xC.3p0
  ```
-->

Los literales numéricos pueden contener formato adicional para que sean más fáciles de leer.
Tanto los números enteros como los flotantes se pueden rellenar con ceros adicionales
y pueden contener guiones bajos para facilitar la lectura.
Ningún tipo de formato afecta el valor subyacente del literal:

```swift
let doubleDecorado = 000123.456
let unMillon = 1_000_000
let pocoMasDeUnMillon = 1_000_000.000_000_1
```

<!--
  - test: `numberLiterals`

  ```swifttest
  -> let paddedDouble = 000123.456
  -> let oneMillion = 1_000_000
  -> let justOverOneMillion = 1_000_000.000_000_1
  ```
-->

## Conversión de tipos numéricos

Usa el tipo `Int` para todas las variables y constantes enteras de propósito general en tu código,
incluso si se sabe que no son negativas.
Usar el tipo entero predeterminado en situaciones cotidianas significa que
las constantes y variables enteras sean inmediatamente interoperables en tu código y
coincidan con el tipo inferido para los valores literales enteros.

Utiliza los otros tipos de enteros solo cuando se requieran, específicamente,
para una tarea en particular,
debido a datos de tamaño explícito de una fuente externa,
o para la optimización necesaria de rendimiento, uso de memoria u otra.
El uso de tipos de tamaño explícito en estas situaciones
ayuda a detectar cualquier desbordamiento accidental de valores
y documenta, implícitamente, la naturaleza de los datos que se utilizan.

### Conversión de enteros

El rango de números que se pueden almacenar en una constante o variable entera
es diferente para cada tipo numérico.
Una constante o variable de tipo `Int8` puede almacenar números entre `-128` y `127`,
mientras que una constante o variable de tipo `UInt8` puede almacenar números entre `0` y `255`.
Un número que no encaja en una constante o variable de tipo entero de tamaño fijo
es reportado como un error al momento de compilar tu código:

```swift
let noPuedeSerNegativo: UInt8 = -1
// UInt8 no puede almacenar números negativos, por lo que esto reporta un error al compilar
let muyGrande: Int8 = Int8.max + 1
// Int8 no puede almacenar un número mayor que su valor máximo,
// por lo que esto también reporta un error al compilar
```

<!--
  - test: `constantsAndVariablesOverflowError`

  ```swifttest
  -> let cannotBeNegative: UInt8 = -1
  // UInt8 can't store negative numbers, and so this will report an error
  -> let tooBig: Int8 = Int8.max + 1
  // Int8 can't store a number larger than its maximum value,
  // and so this will also report an error
  !! /tmp/swifttest.swift:2:29: error: arithmetic operation '127 + 1' (on type 'Int8') results in an overflow
  !! let tooBig: Int8 = Int8.max + 1
  !!                    ~~~~~~~~ ^ ~
  !! /tmp/swifttest.swift:1:31: error: negative integer '-1' overflows when stored into unsigned type 'UInt8'
  !! let cannotBeNegative: UInt8 = -1
  !!                                ^
  ```
-->

Dado que cada tipo numérico puede almacenar un rango diferente de valores,
debes optar por una conversión de tipo numérico caso por caso.
Mediante este enfoque, se evitan errores de conversión ocultos
y ayuda a que las intenciones de conversión de tipos sean explícitas en tu código.

Para convertir un tipo de número específico a otro,
inicializa un nuevo número del tipo deseado con el valor existente.
En el siguiente ejemplo, la constante `dosMil` es de tipo `UInt16`,
mientras que la constante `uno` es de tipo `UInt8`.
No se pueden sumar directamente,
porque no son del mismo tipo.
En cambio, en este ejemplo se llama a `UInt16(uno)` para crear
un nuevo `UInt16` inicializado con el valor de `uno`,
y se usa este valor en lugar del original:

```swift
let dosMil: UInt16 = 2_000
let uno: UInt8 = 1
let dosMilUno = dosMil + UInt16(uno)
```

<!--
  - test: `typeConversion`

  ```swifttest
  -> let twoThousand: UInt16 = 2_000
  -> let one: UInt8 = 1
  -> let twoThousandAndOne = twoThousand + UInt16(one)
  >> print(twoThousandAndOne)
  << 2001
  ```
-->

Debido a que ambos lados de la adición ahora son del tipo `UInt16`,
la adición es permitida.
Se infiere que la constante de salida (`dosMilUno`) es del tipo `UInt16`,
porque es la suma de dos valores `UInt16`.

`AlgunTipo(conValorInicial)` es la forma predeterminada de llamar al inicializador de un tipo Swift
y pasar un valor inicial.
Detrás de cámaras, `UInt16` tiene un inicializador que acepta un valor de tipo `UInt8`,
por lo que este inicializador se usa para crear un nuevo `UInt16` a partir de un `UInt8` existente.
Sin embargo, no le puedes pasar *cualquier* tipo;
tiene que ser un tipo para el cual `UInt16` proporcione un inicializador.
La extensión de los tipos existentes para proporcionar inicializadores que acepten nuevos tipos
(incluidas tus propias definiciones de tipo)
se trata en <doc:Extensions>.

### Conversión de números enteros y de punto flotante

Toda conversión entre tipos numéricos enteros y de punto flotante debe hacerse de manera explícita:

```swift
let tres = 3
let puntoUnoCuatroUnoCincoNueve = 0.14159
let pi = Double(tres) + puntoUnoCuatroUnoCincoNueve
// pi es igual a 3.14159 y se infiere que es de tipo Double
```

<!--
  - test: `typeConversion`

  ```swifttest
  -> let three = 3
  -> let pointOneFourOneFiveNine = 0.14159
  -> let pi = Double(three) + pointOneFourOneFiveNine
  /> pi equals \(pi), and is inferred to be of type Double
  </ pi equals 3.14159, and is inferred to be of type Double
  ```
-->

Acá, el valor de la constante `tres` se usa para crear un nuevo valor de tipo `Double`,
de modo que ambos lados de la suma sean del mismo tipo.
Sin esta conversión en su lugar, no se permitiría la suma.

La conversión de punto flotante a entero también debe hacerse de manera explícita.
Un tipo entero se puede inicializar con un valor de tipo `Double` o `Float`:

```swift
let piEntero = Int(pi)
// piEntero es igual a 3 y se infiere que es de tipo Int
```

<!--
  - test: `typeConversion`

  ```swifttest
  -> let integerPi = Int(pi)
  /> integerPi equals \(integerPi), and is inferred to be of type Int
  </ integerPi equals 3, and is inferred to be of type Int
  ```
-->

Los valores de punto flotante siempre resultan truncados al usarse
para inicializar un nuevo valor entero de esta manera.
Esto significa que `4.75` se convierte en `4` y `-3.9` se convierte en `-3`.

> Nota: Las reglas para combinar variables y constantes numéricas son diferentes de
> las reglas para los literales numéricos.
> El valor literal `3` se puede agregar directamente al valor literal `0.14159`,
> porque los números literales no tienen un tipo explícito por sí mismos.
> Su tipo se infiere solo al momento en que son evaluados por el compilador.

<!--
  NOTE: this section on explicit conversions could be included in the Operators section.
  I think it's more appropriate here, however,
  and helps to reinforce the “just use Int” message.
-->

## Alias de tipos

Los “alias de tipos” (*type aliases*) definen un nombre alternativo para un tipo existente.
Los alias de tipos se definen con la palabra clave `typealias`.

Los alias de tipos son útiles cuando deseas referirte a un tipo existente
con un nombre que sea —contextualmente— más apropiado,
como cuando se trabaja con datos de un tamaño específico de una fuente externa:

```swift
typealias MuestraDeAudio = UInt16
```

<!--
  - test: `typeAliases`

  ```swifttest
  -> typealias AudioSample = UInt16
  ```
-->

Una vez que definas un alias de tipo,
puedes usar el alias en cualquier lugar donde pueda usarse el nombre original:

```swift
var maximaAmplitudHallada = MuestraDeAudio.min
// maximaAmplitudHallada ahora es 0
```

<!--
  - test: `typeAliases`

  ```swifttest
  -> var maxAmplitudeFound = AudioSample.min
  /> maxAmplitudeFound is now \(maxAmplitudeFound)
  </ maxAmplitudeFound is now 0
  ```
-->

Aquí, `MuestraDeAudio` se define como un alias para `UInt16`.
Debido a que es un alias,
el llamado a `MuestraDeAudio.min` en realidad llama a `UInt16.min`,
el cual proporciona un valor inicial de `0` para la variable `maximaAmplitudHallada`.

## Booleanos

Swift tiene un tipo *booleano* básico, llamado `Bool`.
Los valores booleanos se les conoce como *lógicos*
porque solo pueden ser verdaderos o falsos.
Swift proporciona dos valores constantes booleanos
— `true` y `false`:

```swift
let lasNaranjasSonAnaranjadas = true
let lasVerdurasSonDeliciosas = false
```

<!--
  - test: `booleans`

  ```swifttest
  -> let orangesAreOrange = true
  -> let turnipsAreDelicious = false
  ```
-->

Los tipos de `lasNaranjasSonAnaranjadas` y `lasVerdurasSonDeliciosas`
han sido inferidos como `Bool` por el hecho de que
se inicializaron con valores literales booleanos.
Al igual que con `Int` y `Double` anteriormente,
no tienes que declarar constantes o variables como `Bool`
si les asignas `true` o `false` al momento de crearlas.
La inferencia de tipo hace que un código en Swift sea más conciso y legible
al inicializar constantes o variables con otros valores cuyo tipo ya se conoce.

Los valores booleanos son particularmente útiles al trabajar con instrucciones condicionales,
como es el caso de la instrucción `if`:

```swift
if lasVerdurasSonDeliciosas {
    print("¡Mmm, deliciosas verduras!")
} else {
    print("No, las verduras son horribles.")
}
// Imprime "No, las verduras son horribles."
```

<!--
  - test: `booleans`

  ```swifttest
  -> if turnipsAreDelicious {
        print("Mmm, tasty turnips!")
     } else {
        print("Eww, turnips are horrible.")
     }
  <- Eww, turnips are horrible.
  ```
-->

Las instrucciones condicionales, como la instrucción `if`,
se tratan con más detalle en <doc:ControlFlow>.

La seguridad de tipo de Swift previene que valores no booleanos se sustituyan por `Bool`.
El siguiente ejemplo resulta en un error al momento de compilar:

```swift
let i = 1

if i {
    // Este ejemplo no se compilará y reportará un error
}
```

<!--
  - test: `booleansNotBoolean`

  ```swifttest
  -> let i = 1
  -> if i {
        // this example will not compile, and will report an error
     }
  !$ error: type 'Int' cannot be used as a boolean; test for '!= 0' instead
  !! if i {
  !!   ^
  !! ( != 0)
  ```
-->

Sin embargo, el siguiente ejemplo alternativo es válido:

```swift
let i = 1

if i == 1 {
    // Este ejemplo se compilará sin problemas
}
```

<!--
  - test: `booleansIsBoolean`

  ```swifttest
  -> let i = 1
  -> if i == 1 {
        // this example will compile successfully
     }
  ```
-->

El resultado de la comparación `i == 1` es de tipo `Bool`,
por lo que este segundo ejemplo pasa la verificación de tipos.
Comparaciones como `i == 1` se analizan en <doc:BasicOperators>.

Al igual que con otros ejemplos de seguridad de tipo en Swift,
este enfoque evita errores accidentales
y garantiza que la intención de una sección particular del código sea siempre clara.

## Tuplas

Las *tuplas* agrupan múltiples valores en un solo valor compuesto.
Los valores dentro de una tupla pueden ser de cualquier tipo
y no tienen que ser del mismo tipo entre sí.

En este ejemplo, `(404, "Not Found")` es una tupla que describe un *código de estado HTTP*.
Un código de estado HTTP es un valor especial devuelto por un servidor web
cada vez que se le solicita una página web.
El código de estado `404 Not Found` es devuelto si se solicita una página web que no existe.

```swift
let errorHTTP404 = (404, "Not Found")
// errorHTTP404 es de tipo (Int, String) y es igual a (404, "Not Found")
```

<!--
  - test: `tuples`

  ```swifttest
  -> let http404Error = (404, "Not Found")
  /> http404Error is of type (Int, String), and equals (\(http404Error.0), \"\(http404Error.1)\")
  </ http404Error is of type (Int, String), and equals (404, "Not Found")
  ```
-->

La tupla `(404, "Not Found")` agrupa un `Int` y un `String`
para dar al código de estado HTTP dos valores separados:
un número y una descripción legible por humanos.
Se puede describir como “una tupla de tipo `(Int, String)`”.

Puedes crear tuplas a partir de cualquier permutación de tipos
y estas pueden contener tantos tipos diferentes como lo desees.
No hay nada que te impida tener
una tupla de tipo `(Int, Int, Int)` o `(String, Bool)`,
o cualquier otra permutación que necesites.

Puedes «descomponer» (*decompose*) el contenido de una tupla en constantes o variables separadas,
a las que luego podrás acceder como de costumbre:

```swift
let (codigoDeEstado, mensajeDeEstado) = errorHTTP404

print("El código de estado es \(codigoDeEstado)")
// Imprime "El código de estado es 404"

print("El mensaje de estado es \(mensajeDeEstado)")
// Imprime "El mensaje de estado es Not Found"
```

<!--
  - test: `tuples`

  ```swifttest
  -> let (statusCode, statusMessage) = http404Error
  -> print("The status code is \(statusCode)")
  <- The status code is 404
  -> print("The status message is \(statusMessage)")
  <- The status message is Not Found
  ```
-->

Si solo necesitas algunos de los valores de la tupla,
ignora miembros de la tupla usando un guión bajo (`_`)
al descomponerla:

```swift
let (soloElCodigoDeEstado, _) = errorHTTP404

print("El código de estado es \(soloElCodigoDeEstado)")
// Imprime "El código de estado es 404"
```

<!--
  - test: `tuples`

  ```swifttest
  -> let (justTheStatusCode, _) = http404Error
  -> print("The status code is \(justTheStatusCode)")
  <- The status code is 404
  ```
-->

Alternativamente,
accede a los valores de los elementos individuales de una tupla mediante números de índices,
iniciando desde cero:

```swift
print("El código de estado es \(errorHTTP404.0)")
// Imprime "El código de estado es 404"

print("El mensaje de estado es \(errorHTTP404.1)")
// Imprime "El mensaje de estado es Not Found"
```

<!--
  - test: `tuples`

  ```swifttest
  -> print("The status code is \(http404Error.0)")
  <- The status code is 404
  -> print("The status message is \(http404Error.1)")
  <- The status message is Not Found
  ```
-->

Puedes nombrar los elementos individuales en una tupla al momento de definirla:

```swift
let respuestaHTTP200 = (codigoDeEstado: 200, descripcion: "OK")
```

<!--
  - test: `tuples`

  ```swifttest
  -> let http200Status = (statusCode: 200, description: "OK")
  ```
-->

Si nombras los elementos de una tupla,
podrás utilizar los nombres de los elementos para acceder a los valores de dichos elementos:

```swift
print("El código de estado es \(respuestaHTTP200.codigoDeEstado)")
// Imprime "El código de estado es 200"

print("El mensaje de estado es \(respuestaHTTP200.descripcion)")
// Imprime "El mensaje de estado es OK"
```

<!--
  - test: `tuples`

  ```swifttest
  -> print("The status code is \(http200Status.statusCode)")
  <- The status code is 200
  -> print("The status message is \(http200Status.description)")
  <- The status message is OK
  ```
-->

Las tuplas son particularmente útiles como valores devueltos por una función.
Una función que solicita una página web puede devolver una tupla de tipo `(Int, String)`
para describir el éxito o fracaso de dicha solicitud.
Al devolver una tupla con dos valores distintos,
—cada uno de un tipo diferente—
la función proporciona información más útil sobre su resultado
que si solo pudiera devolver un único valor de un único tipo.
Para obtener más información, consulta <doc:Functions#Funciones-que-devuelven-múltiples-valores>.

> Nota: Las tuplas son útiles para grupos simples de valores relacionados.
> Estas no son adecuadas para la creación de estructuras de datos complejas.
> Si es probable que tu estructura de datos sea más compleja,
> modélala como una clase o estructura, en lugar de una tupla.
> Para obtener más información, consulta <doc:ClassesAndStructures>.

## Opcionales

Los *opcionales* se utilizan en situaciones en las que un valor puede no existir.
Un opcional representa dos posibilidades:
*existe* un valor, y es posible extraer dicho valor del opcional,
o *no existe* ningún valor en lo absoluto.

> Nota: El concepto de opcionales no existe en C ni en Objective-C.
> Lo más cercano en Objective-C es
> la capacidad de devolver `nil` de un método que de otra manera devolvería un objeto,
> donde `nil` representa “la ausencia de un objeto válido”.
> Sin embargo, esto solo funciona para objetos;
> no funciona para estructuras, tipos básicos de C, o valores de enumeraciones.
> Para estos tipos,
> los métodos en Objective-C suelen devolver un valor especial (como `NSNotFound`)
> para indicar la ausencia de un valor.
> Este mecanismo asume que quien invoca al método sabe que hay
> un valor especial contra el cual testear y recuerda verificarlo.
> Los opcionales en Swift te permiten indicar la ausencia de un valor para *cualquier tipo*,
> sin la necesidad de constantes especiales.

Aquí hay un ejemplo de cómo se pueden usar opcionales para lidiar con la ausencia de un valor.
El tipo `Int` de Swift tiene un inicializador
que intenta convertir un valor `String` en un valor `Int`.
Sin embargo, no todas las cadenas pueden ser convertidas en enteros.
La cadena `"123"` puede convertirse en el valor numérico `123`,
pero la cadena `"Hola, mundo."` no tiene un valor numérico obvio en el cual convertirse.

El siguiente ejemplo utiliza el inicializador para intentar convertir un `String` en un `Int`:

```swift
let posibleNumero = "123"
let numeroConvertido = Int(posibleNumero)
// Se infiere que numeroConvertido es de tipo "Int?" (o "Int opcional")
```

<!--
  - test: `optionals`

  ```swifttest
  -> let possibleNumber = "123"
  -> let convertedNumber = Int(possibleNumber)
  // convertedNumber is inferred to be of type "Int?", or "optional Int"
  >> print(type(of: convertedNumber))
  << Optional<Int>
  ```
-->

Dado que el inicializador podría fallar,
este devuelve un `Int` *opcional*, en lugar de un `Int`.
Un `Int` opcional se escribe `Int?`, no `Int`.
El signo de interrogación indica que el valor que contiene es opcional,
lo que significa que puede contener *algún* valor `Int`,
o puede no contener *ningún valor en absoluto*.
(No puede contener nada más, como un valor `Bool` o un valor `String`.
O es un `Int`, o no es nada en absoluto).

### nil

You set an optional variable to a valueless state
by assigning it the special value `nil`:

```swift
var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value
```

<!--
  - test: `optionals`

  ```swifttest
  -> var serverResponseCode: Int? = 404
  /> serverResponseCode contains an actual Int value of \(serverResponseCode!)
  </ serverResponseCode contains an actual Int value of 404
  -> serverResponseCode = nil
  // serverResponseCode now contains no value
  ```
-->

> Note: You can't use `nil` with non-optional constants and variables.
> If a constant or variable in your code needs to work with
> the absence of a value under certain conditions,
> always declare it as an optional value of the appropriate type.

If you define an optional variable without providing a default value,
the variable is automatically set to `nil` for you:

```swift
var surveyAnswer: String?
// surveyAnswer is automatically set to nil
```

<!--
  - test: `optionals`

  ```swifttest
  -> var surveyAnswer: String?
  // surveyAnswer is automatically set to nil
  ```
-->

> Note: Swift's `nil` isn't the same as `nil` in Objective-C.
> In Objective-C, `nil` is a pointer to a nonexistent object.
> In Swift, `nil` isn't a pointer --- it's the absence of a value of a certain type.
> Optionals of *any* type can be set to `nil`, not just object types.

### Sentencias if y extracción forzada

You can use an `if` statement to find out whether an optional contains a value
by comparing the optional against `nil`.
You perform this comparison with the “equal to” operator (`==`)
or the “not equal to” operator (`!=`).

If an optional has a value, it's considered to be “not equal to” `nil`:

```swift
if convertedNumber != nil {
    print("convertedNumber contains some integer value.")
}
// Prints "convertedNumber contains some integer value."
```

<!--
  - test: `optionals`

  ```swifttest
  -> if convertedNumber != nil {
        print("convertedNumber contains some integer value.")
     }
  <- convertedNumber contains some integer value.
  ```
-->

Once you're sure that the optional *does* contain a value,
you can access its underlying value
by adding an exclamation point (`!`) to the end of the optional's name.
The exclamation point effectively says,
“I know that this optional definitely has a value; please use it.”
This is known as *forced unwrapping* of the optional's value:

```swift
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber!).")
}
// Prints "convertedNumber has an integer value of 123."
```

<!--
  - test: `optionals`

  ```swifttest
  -> if convertedNumber != nil {
        print("convertedNumber has an integer value of \(convertedNumber!).")
     }
  <- convertedNumber has an integer value of 123.
  ```
-->

For more about the `if` statement, see <doc:ControlFlow>.

> Note: Trying to use `!` to access a nonexistent optional value triggers
> a runtime error.
> Always make sure that an optional contains a non-`nil` value
> before using `!` to force-unwrap its value.

### Vinculación opcional

You use *optional binding* to find out whether an optional contains a value,
and if so, to make that value available as a temporary constant or variable.
Optional binding can be used with `if` and `while` statements
to check for a value inside an optional,
and to extract that value into a constant or variable,
as part of a single action.
`if` and `while` statements are described in more detail in <doc:ControlFlow>.

Write an optional binding for an `if` statement as follows:

```swift
if let <#constantName#> = <#someOptional#> {
   <#statements#>
}
```

You can rewrite the `possibleNumber` example from
the <doc:TheBasics#Opcionales> section
to use optional binding rather than forced unwrapping:

```swift
if let actualNumber = Int(possibleNumber) {
    print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("The string \"\(possibleNumber)\" couldn't be converted to an integer")
}
// Prints "The string "123" has an integer value of 123"
```

<!--
  - test: `optionals`

  ```swifttest
  -> if let actualNumber = Int(possibleNumber) {
        print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
     } else {
        print("The string \"\(possibleNumber)\" couldn't be converted to an integer")
     }
  <- The string "123" has an integer value of 123
  ```
-->

This code can be read as:

“If the optional `Int` returned by `Int(possibleNumber)` contains a value,
set a new constant called `actualNumber` to the value contained in the optional.”

If the conversion is successful,
the `actualNumber` constant becomes available for use within
the first branch of the `if` statement.
It has already been initialized with the value contained *within* the optional,
and so you don't use the `!` suffix to access its value.
In this example, `actualNumber` is simply used to print the result of the conversion.

If you don't need to refer to the original, optional constant or variable
after accessing the value it contains,
you can use the same name for the new constant or variable:

```swift
let myNumber = Int(possibleNumber)
// Here, myNumber is an optional integer
if let myNumber = myNumber {
    // Here, myNumber is a non-optional integer
    print("My number is \(myNumber)")
}
// Prints "My number is 123"
```

<!--
  - test: `optionals`

  ```swifttest
  -> let myNumber = Int(possibleNumber)
  // Here, myNumber is an optional integer
  -> if let myNumber = myNumber {
         // Here, myNumber is a non-optional integer
         print("My number is \(myNumber)")
     }
  <- My number is 123
  ```
-->

This code starts by checking whether `myNumber` contains a value,
just like the code in the previous example.
If `myNumber` has a value,
the value of a new constant named `myNumber` is set to that value.
Inside the body of the `if` statement,
writing `myNumber` refers to that new non-optional constant.
Before the beginning of the `if` statement and after its end,
writing `myNumber` refers to the optional integer constant.

Because this kind of code is so common,
you can use a shorter spelling to unwrap an optional value:
write just the name of the constant or variable that you're unwrapping.
The new, unwrapped constant or variable
implicitly uses the same name as the optional value.

```swift
if let myNumber {
    print("My number is \(myNumber)")
}
// Prints "My number is 123"
```

<!--
  - test: `optionals`

  ```swifttest
  -> if let myNumber {
         print("My number is \(myNumber)")
     }
  <- My number is 123
  ```
-->

You can use both constants and variables with optional binding.
If you wanted to manipulate the value of `myNumber`
within the first branch of the `if` statement,
you could write `if var myNumber` instead,
and the value contained within the optional
would be made available as a variable rather than a constant.
Changes you make to `myNumber` inside the body of the `if` statement
apply only to that local variable,
*not* to the original, optional constant or variable that you unwrapped.

You can include as many optional bindings and Boolean conditions
in a single `if` statement as you need to,
separated by commas.
If any of the values in the optional bindings are `nil`
or any Boolean condition evaluates to `false`,
the whole `if` statement's condition
is considered to be `false`.
The following `if` statements are equivalent:

```swift
if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
    print("\(firstNumber) < \(secondNumber) < 100")
}
// Prints "4 < 42 < 100"

if let firstNumber = Int("4") {
    if let secondNumber = Int("42") {
        if firstNumber < secondNumber && secondNumber < 100 {
            print("\(firstNumber) < \(secondNumber) < 100")
        }
    }
}
// Prints "4 < 42 < 100"
```

<!--
  - test: `multipleOptionalBindings`

  ```swifttest
  -> if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
        print("\(firstNumber) < \(secondNumber) < 100")
     }
  <- 4 < 42 < 100
  ---
  -> if let firstNumber = Int("4") {
         if let secondNumber = Int("42") {
             if firstNumber < secondNumber && secondNumber < 100 {
                 print("\(firstNumber) < \(secondNumber) < 100")
             }
         }
     }
  <- 4 < 42 < 100
  ```
-->

<!--
  The example above uses multiple optional bindings
  to show that you can have more than one
  and to show the short-circuiting behavior.
  It has multiple Boolean conditions
  to show that you should join logically related conditions
  using the && operator instead of a comma.
-->

> Note: Constants and variables created with optional binding in an `if` statement
> are available only within the body of the `if` statement.
> In contrast, the constants and variables created with a `guard` statement
> are available in the lines of code that follow the `guard` statement,
> as described in <doc:ControlFlow#Salida-temprana>.

### Opcionales extraídos implícitamente

As described above,
optionals indicate that a constant or variable is allowed to have “no value”.
Optionals can be checked with an `if` statement to see if a value exists,
and can be conditionally unwrapped with optional binding
to access the optional's value if it does exist.

Sometimes it's clear from a program's structure that an optional will *always* have a value,
after that value is first set.
In these cases, it's useful to remove the need
to check and unwrap the optional's value every time it's accessed,
because it can be safely assumed to have a value all of the time.

These kinds of optionals are defined as *implicitly unwrapped optionals*.
You write an implicitly unwrapped optional by placing an exclamation point (`String!`)
rather than a question mark (`String?`) after the type that you want to make optional.
Rather than placing an exclamation point after the optional's name when you use it,
you place an exclamation point after the optional's type when you declare it.

Implicitly unwrapped optionals are useful when
an optional's value is confirmed to exist immediately after the optional is first defined
and can definitely be assumed to exist at every point thereafter.
The primary use of implicitly unwrapped optionals in Swift is during class initialization,
as described in <doc:AutomaticReferenceCounting#Referencias-unowned-y-propiedades-opcionales-extraídas-de-forma-implícita>.

An implicitly unwrapped optional is a normal optional behind the scenes,
but can also be used like a non-optional value,
without the need to unwrap the optional value each time it's accessed.
The following example shows the difference in behavior between
an optional string and an implicitly unwrapped optional string
when accessing their wrapped value as an explicit `String`:

```swift
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // requires an exclamation point

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // no need for an exclamation point
```

<!--
  - test: `implicitlyUnwrappedOptionals`

  ```swifttest
  -> let possibleString: String? = "An optional string."
  -> let forcedString: String = possibleString! // requires an exclamation point
  ---
  -> let assumedString: String! = "An implicitly unwrapped optional string."
  -> let implicitString: String = assumedString // no need for an exclamation point
  ```
-->

You can think of an implicitly unwrapped optional as
giving permission for the optional to be force-unwrapped if needed.
When you use an implicitly unwrapped optional value,
Swift first tries to use it as an ordinary optional value;
if it can't be used as an optional, Swift force-unwraps the value.
In the code above,
the optional value `assumedString` is force-unwrapped
before assigning its value to `implicitString`
because `implicitString` has an explicit, non-optional type of `String`.
In code below,
`optionalString` doesn't have an explicit type
so it's an ordinary optional.

```swift
let optionalString = assumedString
// The type of optionalString is "String?" and assumedString isn't force-unwrapped.
```

<!--
  - test: `implicitlyUnwrappedOptionals`

  ```swifttest
  -> let optionalString = assumedString
  // The type of optionalString is "String?" and assumedString isn't force-unwrapped.
  >> print(type(of: optionalString))
  << Optional<String>
  ```
-->

If an implicitly unwrapped optional is `nil` and you try to access its wrapped value,
you'll trigger a runtime error.
The result is exactly the same as if you place an exclamation point
after a normal optional that doesn't contain a value.

You can check whether an implicitly unwrapped optional is `nil`
the same way you check a normal optional:

```swift
if assumedString != nil {
    print(assumedString!)
}
// Prints "An implicitly unwrapped optional string."
```

<!--
  - test: `implicitlyUnwrappedOptionals`

  ```swifttest
  -> if assumedString != nil {
        print(assumedString!)
     }
  <- An implicitly unwrapped optional string.
  ```
-->

You can also use an implicitly unwrapped optional with optional binding,
to check and unwrap its value in a single statement:

```swift
if let definiteString = assumedString {
    print(definiteString)
}
// Prints "An implicitly unwrapped optional string."
```

<!--
  - test: `implicitlyUnwrappedOptionals`

  ```swifttest
  -> if let definiteString = assumedString {
        print(definiteString)
     }
  <- An implicitly unwrapped optional string.
  ```
-->

> Note: Don't use an implicitly unwrapped optional when there's a possibility of
> a variable becoming `nil` at a later point.
> Always use a normal optional type if you need to check for a `nil` value
> during the lifetime of a variable.

## Manejo de errores

You use *error handling* to respond to error conditions
your program may encounter during execution.

In contrast to optionals,
which can use the presence or absence of a value
to communicate success or failure of a function,
error handling allows you to determine the underlying cause of failure,
and, if necessary, propagate the error to another part of your program.

When a function encounters an error condition, it *throws* an error.
That function's caller can then *catch* the error and respond appropriately.

```swift
func canThrowAnError() throws {
    // this function may or may not throw an error
}
```

<!--
  - test: `errorHandling`

  ```swifttest
  >> enum SimpleError: Error {
  >>    case someError
  >> }
  >> let condition = true
  -> func canThrowAnError() throws {
        // this function may or may not throw an error
  >>    if condition {
  >>       throw SimpleError.someError
  >>    }
     }
  ```
-->

A function indicates that it can throw an error
by including the `throws` keyword in its declaration.
When you call a function that can throw an error,
you prepend the `try` keyword to the expression.

Swift automatically propagates errors out of their current scope
until they're handled by a `catch` clause.

```swift
do {
    try canThrowAnError()
    // no error was thrown
} catch {
    // an error was thrown
}
```

<!--
  - test: `errorHandling`

  ```swifttest
  -> do {
  ->    try canThrowAnError()
  >>    print("No Error")
  ->    // no error was thrown
  -> } catch {
  >>    print("Error")
  ->    // an error was thrown
  -> }
  << Error
  ```
-->

A `do` statement creates a new containing scope,
which allows errors to be propagated to one or more `catch` clauses.

Here's an example of how error handling can be used
to respond to different error conditions:

```swift
func makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
```

<!--
  - test: `errorHandlingTwo`

  ```swifttest
  >> enum SandwichError: Error {
  >>     case outOfCleanDishes
  >>     case missingIngredients([String])
  >> }
  >> func washDishes() { print("Wash dishes") }
  >> func buyGroceries(_ shoppingList: [String]) { print("Buy \(shoppingList)") }
  -> func makeASandwich() throws {
         // ...
     }
  >> func eatASandwich() {}
  ---
  -> do {
         try makeASandwich()
         eatASandwich()
     } catch SandwichError.outOfCleanDishes {
         washDishes()
     } catch SandwichError.missingIngredients(let ingredients) {
         buyGroceries(ingredients)
     }
  ```
-->

In this example, the `makeASandwich()` function will throw an error
if no clean dishes are available
or if any ingredients are missing.
Because `makeASandwich()` can throw an error,
the function call is wrapped in a `try` expression.
By wrapping the function call in a `do` statement,
any errors that are thrown will be propagated
to the provided `catch` clauses.

If no error is thrown, the `eatASandwich()` function is called.
If an error is thrown and it matches the `SandwichError.outOfCleanDishes` case,
then the `washDishes()` function will be called.
If an error is thrown and it matches the `SandwichError.missingIngredients` case,
then the `buyGroceries(_:)` function is called
with the associated `[String]` value captured by the `catch` pattern.

Throwing, catching, and propagating errors is covered in greater detail in
<doc:ErrorHandling>.

## Aserciones y precondiciones

*Assertions* and *preconditions*
are checks that happen at runtime.
You use them to make sure an essential condition is satisfied
before executing any further code.
If the Boolean condition in the assertion or precondition
evaluates to `true`,
code execution continues as usual.
If the condition evaluates to `false`,
the current state of the program is invalid;
code execution ends, and your app is terminated.

You use assertions and preconditions
to express the assumptions you make
and the expectations you have
while coding,
so you can include them as part of your code.
Assertions help you find mistakes and incorrect assumptions during development,
and preconditions help you detect issues in production.

In addition to verifying your expectations at runtime,
assertions and preconditions also become a useful form of documentation
within the code.
Unlike the error conditions discussed in <doc:TheBasics#Manejo-de-errores> above,
assertions and preconditions aren't used
for recoverable or expected errors.
Because a failed assertion or precondition
indicates an invalid program state,
there's no way to catch a failed assertion.

Using assertions and preconditions
isn't a substitute for designing your code in such a way
that invalid conditions are unlikely to arise.
However,
using them to enforce valid data and state
causes your app to terminate more predictably
if an invalid state occurs,
and helps make the problem easier to debug.
Stopping execution as soon as an invalid state is detected
also helps limit the damage caused by that invalid state.

The difference between assertions and preconditions is in when they're checked:
Assertions are checked only in debug builds,
but preconditions are checked in both debug and production builds.
In production builds,
the condition inside an assertion isn't evaluated.
This means you can use as many assertions as you want
during your development process,
without impacting performance in production.

### Depuración con aserciones

<!--
  If your code triggers an assertion while running in a debug environment,
  such as when you build and run an app in Xcode,
  you can see exactly where the invalid state occurred
  and query the state of your app at the time that the assertion was triggered.
  An assertion also lets you provide a suitable debug message as to the nature of the assert.
-->

You write an assertion by calling the
[`assert(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1541112-assert) function
from the Swift standard library.
You pass this function an expression that evaluates to `true` or `false`
and a message to display if the result of the condition is `false`.
For example:

```swift
let age = -3
assert(age >= 0, "A person's age can't be less than zero.")
// This assertion fails because -3 isn't >= 0.
```

<!--
  - test: `assertions-1`

  ```swifttest
  -> let age = -3
  -> assert(age >= 0, "A person's age can't be less than zero.")
  xx assert
  // This assertion fails because -3 isn't >= 0.
  ```
-->

In this example, code execution continues if `age >= 0` evaluates to `true`,
that is, if the value of `age` is nonnegative.
If the value of `age` is negative, as in the code above,
then `age >= 0` evaluates to `false`,
and the assertion fails, terminating the application.

You can omit the assertion message ---
for example, when it would just repeat the condition as prose.

```swift
assert(age >= 0)
```

<!--
  - test: `assertions-2`

  ```swifttest
  >> let age = -3
  -> assert(age >= 0)
  xx assert
  ```
-->

<!--
  - test: `assertionsCanUseStringInterpolation`

  ```swifttest
  -> let age = -3
  -> assert(age >= 0, "A person's age can't be less than zero, but value is \(age).")
  xx assert
  ```
-->

If the code already checks the condition,
you use the
[`assertionFailure(_:file:line:)`](https://developer.apple.com/documentation/swift/1539616-assertionfailure) function
to indicate that an assertion has failed.
For example:

```swift
if age > 10 {
    print("You can ride the roller-coaster or the ferris wheel.")
} else if age >= 0 {
    print("You can ride the ferris wheel.")
} else {
    assertionFailure("A person's age can't be less than zero.")
}
```

<!--
  - test: `assertions-3`

  ```swifttest
  >> let age = -3
  -> if age > 10 {
         print("You can ride the roller-coaster or the ferris wheel.")
     } else if age >= 0 {
         print("You can ride the ferris wheel.")
     } else {
         assertionFailure("A person's age can't be less than zero.")
     }
  xx assert
  ```
-->

### Imposición de precondiciones

Use a precondition whenever a condition has the potential to be false,
but must *definitely* be true for your code to continue execution.
For example, use a precondition to check that a subscript isn't out of bounds,
or to check that a function has been passed a valid value.

You write a precondition by calling the
[`precondition(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1540960-precondition) function.
You pass this function an expression that evaluates to `true` or `false`
and a message to display if the result of the condition is `false`.
For example:

```swift
// In the implementation of a subscript...
precondition(index > 0, "Index must be greater than zero.")
```

<!--
  - test: `preconditions`

  ```swifttest
  >> let index = -1
  // In the implementation of a subscript...
  -> precondition(index > 0, "Index must be greater than zero.")
  xx assert
  ```
-->

You can also call the
[`preconditionFailure(_:file:line:)`](https://developer.apple.com/documentation/swift/1539374-preconditionfailure) function
to indicate that a failure has occurred ---
for example, if the default case of a switch was taken,
but all valid input data should have been handled
by one of the switch's other cases.

> Note: If you compile in unchecked mode (`-Ounchecked`),
> preconditions aren't checked.
> The compiler assumes that preconditions are always true,
> and it optimizes your code accordingly.
> However, the `fatalError(_:file:line:)` function always halts execution,
> regardless of optimization settings.
>
> You can use the `fatalError(_:file:line:)` function
> during prototyping and early development
> to create stubs for functionality that hasn't been implemented yet,
> by writing `fatalError("Unimplemented")` as the stub implementation.
> Because fatal errors are never optimized out,
> unlike assertions or preconditions,
> you can be sure that execution always halts
> if it encounters a stub implementation.

<!--
  "\ " in the first cell below lets it be empty.
  Otherwise RST treats the row as a continuation.

  ============ =====  ==========  ===============================
  \            Debug  Production  Production with ``-Ounchecked``
  ============ =====  ==========  ===============================
  Assertion    Yes    No          No
  ------------ -----  ----------  -------------------------------
  Precondition Yes    Yes         No
  ------------ -----  ----------  -------------------------------
  Fatal Error  Yes    Yes         Yes
  ============ =====  ==========  ===============================
-->

<!--
  TODO: In Xcode, can you set a breakpoint on assertion/precondition failure?
  If so, mention that fact and give a link to a guide that shows you how.
  In LLDB, 'breakpoint set -E swift' catches when errors are thrown,
  but doesn't stop at assertions.
-->

> Software Beta:
>
> Esta documentación contiene información preliminar sobre una API o tecnología en desarrollo. Esta información está sujeta a cambios, y todo software implementado en conformidad con esta documentación debe ser testeado con el software final del sistema operativo.
>
> Conoce más acerca del uso del [software beta de Apple](https://developer.apple.com/es/support/beta-software/).

<!--
This source file is part of the Swift.org open source project

Copyright (c) 2014 - 2023 Apple Inc. and the Swift project authors
Licensed under Apache License v2.0 with Runtime Library Exception

See https://swift.org/LICENSE.txt for license information
See https://swift.org/CONTRIBUTORS.txt for the list of Swift project authors
-->
