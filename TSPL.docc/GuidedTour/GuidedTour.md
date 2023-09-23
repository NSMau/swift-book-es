# Un recorrido por Swift

Explora las características y la sintaxis de Swift.

Es costumbre que el primer programa en un nuevo lenguaje
imprima la frase «¡Hola, mundo!» en la pantalla.
En Swift, esto se puede conseguir mediante una sola línea de código:

<!--
  K&R uses “hello, world”.
  It seems worth breaking with tradition to use proper casing.
-->

```swift
print("¡Hola, mundo!")
// Imprime "¡Hola, mundo!"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> print("Hello, world!")
  <- Hello, world!
  ```
-->

Si has desarollado anteriormente en C u Objective-C,
esta sintaxis te resultará familiar;
en Swift, esta línea de código representa un programa completo.
No hace falta importar una biblioteca aparte
para contar con funciones como entrada/salida o manejo de cadenas de texto.
Todo código escrito en el ámbito (*scope*) global se utiliza
como punto de entrada para el programa,
por lo que no necesitamos una función `main()`.
Tampoco hace falta escribir punto y coma
al final de cada declaración.

Esta guía te proporciona suficiente información
para comenzar a desarrollar código en Swift
al enseñarte cómo realizar una variedad de tareas de programación.
No te preocupes si hay algo que no entiendes;
todo lo presentado en esta guía
se explica en detalle en el resto de este libro.

## Valores sencillos

Usa `let` para crear una constante y `var` para crear una variable.
No hace falta saber el valor de una constante a la hora de compilar,
pero tal valor debe asignarse exactamente una única vez.
Esto significa que puedes usar constantes para nombrar un valor
que solo se define una vez, pero que se usa en muchas partes.

```swift
var miVariable = 42
miVariable = 50
let miConstante = 42
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var myVariable = 42
  -> myVariable = 50
  -> let myConstant = 42
  ```
-->

Una constante o variable debe ser del mismo tipo
que el valor que se le quiera asignar.
Sin embargo, no siempre tienes que escribir el tipo explícitamente.
El hecho de proporcionar un valor al crear una variable o constante,
le permite al compilador inferir el tipo de dicha variable o constante.
En el ejemplo anterior,
el compilador infiere que `miVariable` es un entero
porque su valor inicial es un entero.

Si el valor inicial no proporciona suficiente información
(o si no hay un valor inicial),
especifica el tipo escribiéndolo después de la variable,
separado por dos puntos (`:`).

```swift
let enteroImplicito = 70
let doubleImplicito = 70.0
let doubleExplicito: Double = 70
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let implicitInteger = 70
  -> let implicitDouble = 70.0
  -> let explicitDouble: Double = 70
  ```
-->

> Experimento: Crea una constante
> con un tipo explícito de `Float` y un valor de `4`.

Los valores nunca se convierten a un tipo diferente implícitamente.
Si necesitas convertir un valor a un tipo diferente,
debes crear —de manera explícita— una instancia del tipo deseado.

```swift
let etiqueta = "El ancho es "
let ancho = 94
let anchoDeLaEtiqueta = etiqueta + String(ancho)
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let label = "The width is "
  -> let width = 94
  -> let widthLabel = label + String(width)
  >> print(widthLabel)
  << The width is 94
  ```
-->

> Experimento: Intenta removiendo la conversión a `String` de la última línea.
> ¿Cuál error te aparece?

<!--
  TODO: Discuss with Core Writers ---
  are these experiments that make you familiar with errors
  helping you learn something?
-->

Hay una manera incluso más sencilla de insertar valores en una cadena de texto —
escribe el valor en paréntesis,
y agrega una barra invertida (`\`) antes de los paréntesis.
Por ejemplo:

```swift
let manzanas = 3
let naranjas = 5
let totalManzanas = "Tengo \(manzanas) manzanas."
let totalFrutas = "Tengo \(manzanas + naranjas) frutas."
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let apples = 3
  -> let oranges = 5
  -> let appleSummary = "I have \(apples) apples."
  >> print(appleSummary)
  << I have 3 apples.
  -> let fruitSummary = "I have \(apples + oranges) pieces of fruit."
  >> print(fruitSummary)
  << I have 8 pieces of fruit.
  ```
-->

> Experimento: Usa `\()` para
> incluir un operación con números de coma flotante en una cadena de texto
> y para incluir el nombre de alguien en un saludo.

Usa tres comillas dobles (`"""`) para cadenas de texto
que ocupan más de una línea.
La sangría (*indentation*) al inicio de cada línea de la cadena es removida
siempre y cuando concuerde con la sangría de las comillas de cierre.
Por ejemplo:

```swift
let cita = """
        Aun cuando hay espacios en blanco a la izquierda,
        las líneas como tal no llevan sangría.
            Excepto por esta línea.
        Las comillas dobles (") pueden aparecer sin escaparlas.

        Todavía tengo \(manzanas + naranjas) frutas.
        """
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let quotation = """
     I said "I have \(apples) apples."
     And then I said "I have \(apples + oranges) pieces of fruit."
     """
  ```
-->

<!--
  Can't show an example of indentation in the triple-quoted string above.
  <rdar://problem/49129068> Swift code formatting damages indentation
-->

Crea arreglos y diccionarios usando corchetes (`[]`),
y accede a sus elementos referenciando
su índice o llave en corchetes.
Está permitido agregar una coma después del último elemento.

<!--
  REFERENCE
  The list of fruits comes from the colors that the original iMac came in,
  following the initial launch of the iMac in Bondi Blue, ordered by SKU --
  which also lines up with the order they appeared in ads:

       M7389LL/A (266 MHz Strawberry)
       M7392LL/A (266 MHz Lime)
       M7391LL/A (266 MHz Tangerine)
       M7390LL/A (266 MHz Grape)
       M7345LL/A (266 MHz Blueberry)

       M7441LL/A (333 MHz Strawberry)
       M7444LL/A (333 MHz Lime)
       M7443LL/A (333 MHz Tangerine)
       M7442LL/A (333 MHz Grape)
       M7440LL/A (333 MHz Blueberry)
-->

<!--
  REFERENCE
  Occupations is a reference to Firefly,
  specifically to Mal's joke about Jayne's job on the ship.

  Can't find the specific episode,
  but it shows up in several lists of Firefly "best of" quotes:

  Mal: Jayne, you will keep a civil tongue in that mouth, or I will sew it shut.
       Is there an understanding between us?
  Jayne: You don't pay me to talk pretty. [...]
  Mal: Walk away from this table. Right now.
  [Jayne loads his plate with food and leaves]
  Simon: What *do* you pay him for?
  Mal: What?
  Simon: I was just wondering what his job is - on the ship.
  Mal: Public relations.
-->

```swift
var frutas = ["fresas", "limas", "mandarinas"]
frutas[1] = "uvas"

var ocupaciones = [
    "Malcolm": "Capitán",
    "Kaylee": "Mecánica",
 ]
ocupaciones["Jayne"] = "Relaciones Públicas"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var fruits = ["strawberries", "limes", "tangerines"]
  -> fruits[1] = "grapes"
  ---
  -> var occupations = [
         "Malcolm": "Captain",
         "Kaylee": "Mechanic",
      ]
  -> occupations["Jayne"] = "Public Relations"
  ```
-->

<!-- Apple Books screenshot begins here. -->

Los arreglos crecen automáticamente a medida que agregas elementos.

```swift
frutas.append("moras")
print(frutas)
// Imprime "["fresas", "uvas", "mandarinas", "moras"]"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> fruits.append("blueberries")
  -> print(fruits)
  <- ["strawberries", "grapes", "tangerines", "blueberries"]
  ```
-->

También puedes usar corchetes para crear un arreglo o un diccionario vacíos.
Para un arreglo, usa `[]`
y, para un diccionario, usa `[:]`.

```swift
frutas = []
ocupaciones = [:]
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> fruits = []
  -> occupations = [:]
  ```
-->

Si asignas un arreglo o un diccionario vacíos a una nueva variable,
o a algún otro lugar donde no hay ninguna información sobre el tipo,
tendrás que especificarlo.

```swift
let arregloVacio: [String] = []
let diccionarioVacio: [String: Float] = [:]
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let emptyArray: [String] = []
  -> let emptyDictionary: [String: Float] = [:]
  ---
  -> let anotherEmptyArray = [String]()
  -> let emptyDictionary = [String: Float]()
  ```
-->

## Flujo de control

Usa `if` y `switch` para crear condicionales,
y usa `for-in`, `while`, y `repeat-while`
para crear ciclos.
El uso de paréntesis alrededor de la condición
o de la variable del ciclo es opcional.
El uso de llaves alrededor del cuerpo del ciclo es obligatorio.

```swift
let puntajesIndividuales = [75, 43, 103, 87, 12]
var puntajeDelEquipo = 0

for puntaje in puntajesIndividuales {
    if puntaje > 50 {
        puntajeDelEquipo += 3
    } else {
        puntajeDelEquipo += 1
    }
}

print(puntajeDelEquipo)
// Imprime "11"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let individualScores = [75, 43, 103, 87, 12]
  -> var teamScore = 0
  -> for score in individualScores {
         if score > 50 {
             teamScore += 3
         } else {
             teamScore += 1
         }
     }
  -> print(teamScore)
  <- 11
  ```
-->

<!--
  REFERENCE
  Jelly babies are a candy/sweet that was closely associated
  with past incarnations of the Doctor in Dr. Who.
-->

<!--
  -> let haveJellyBabies = true
  -> if haveJellyBabies {
     }
  << Would you like a jelly baby?
-->

En una instrucción `if`,
el condicional debe ser una expresión booleana;
esto significa, que una instrucción tipo `if puntaje { ... }` es un error,
pues no se hace una comparación explícita con cero.

Puede escribir `if` o `switch`
después del signo igual (`=`) de una asignación
o después de `return`,
para elegir un valor en función de la condición.

```swift
let decoracionDelPuntaje = if puntajeDelEquipo > 10 {
    "🎉"
} else {
    ""
}
print("Puntaje:", puntajeDelEquipo, decoracionDelPuntaje)
// Imprime "Puntaje: 11 🎉"
```

Puedes usar `if` y `let` en conjunto
para lidiar con valores que podrían no existir.
Estos valores son representados como opcionales.
Un valor opcional puede contener o un valor
o `nil`, para indicar la ausencia de un valor.
Agrega un signo de interrogación (`?`) después del tipo de un valor
para marcar dicho valor como opcional.

<!-- Apple Books screenshot ends here. -->

<!--
  REFERENCE
  John Appleseed is a stock Apple fake name,
  going back at least to the contacts database
  that ships with the SDK in the simulator.
-->

```swift
var cadenaOpcional: String? = "Hola"
print(cadenaOpcional == nil)
// Imprime "false"

var nombreOpcional: String? = "John Appleseed"
var saludo = "¡Hola!"

if let nombre = nombreOpcional {
    saludo = "¡Hola, \(nombre)!"
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var optionalString: String? = "Hello"
  -> print(optionalString == nil)
  <- false
  ---
  -> var optionalName: String? = "John Appleseed"
  -> var greeting = "Hello!"
  -> if let name = optionalName {
         greeting = "Hello, \(name)"
     }
  >> print(greeting)
  << Hello, John Appleseed
  ```
-->

> Experimento: Cambia el valor de `nombreOpcional` por `nil`.
> ¿Cuál saludo obtienes?
> Agrega una cláusula `else` que defina un saludo diferente
> si `nombreOpcional` es `nil`.

Si el valor opcional es `nil`,
el condicional resulta ser `false` y el código en las llaves es ignorado.
En caso contrario, se extrae el valor opcional y se le asigna
a la constante que le sigue a `let`,
lo cual hace que el valor extraído esté disponible
dentro del bloque de código.

Otra forma de manejar valores opcionales
es proporcionar un valor predeterminado mediante el uso del operador `??`.
Si el valor opcional no existe,
se usará el valor predeterminado en su lugar.

```swift
let alias: String? = nil
let nombreCompleto: String = "John Appleseed"
let saludoInformal = "Hola, \(alias ?? nombreCompleto)"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let nickname: String? = nil
  -> let fullName: String = "John Appleseed"
  -> let informalGreeting = "Hi \(nickname ?? fullName)"
  >> print(informalGreeting)
  << Hi John Appleseed
  ```
-->

Puedes usar una sintaxis más concisa para extraer un valor,
usando el mismo nombre para dicho valor extraído.

```swift
if let alias {
    print("Hey, \(alias)")
}
// No imprime nada porque alias es nil.
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> if let nickname {
         print("Hey, \(nickname)")
     }
  ```
-->

Los ciclos `switch` soportan cualquier tipo de datos
al igual que una gran variedad de operaciones comparativas;
estos no se limitan a enteros
y comprobaciones de igualdad.

<!--
  REFERENCE
  The vegetables and foods made from vegetables
  were just a convenient choice for a switch statement.
  They have various properties
  and fit with the apples & oranges used in an earlier example.
-->

```swift
let vegetal = "pimiento rojo"
switch vegetal {
case "apio":
    print("Un par de vegetales más y tendrás un buen jugo verde.")
case "pepino", "cebolla":
    print("Útil para una buena ensalada.")
case let x where x.hasSuffix("pimiento"):
    print("¿Es un \(x) picante?")
default:
    print("Todo sabe bien en una sopa.")
}
// Imprime "¿Es un pimiento rojo picante?"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let vegetable = "red pepper"
  -> switch vegetable {
         case "celery":
             print("Add some raisins and make ants on a log.")
         case "cucumber", "watercress":
             print("That would make a good tea sandwich.")
         case let x where x.hasSuffix("pepper"):
             print("Is it a spicy \(x)?")
         default:
             print("Everything tastes good in soup.")
     }
  <- Is it a spicy red pepper?
  ```
-->

> Experimento: Remueve el caso `default`.
> ¿Cuál es el error que aparece?

Observa cómo es posible usar `let` con un patrón
para asignar, a una constante,
el valor que concuerde con dicho patrón.

Una vez ejecutado el código dentro del caso que concuerda,
el programa abandona la sentencia `switch`.
La ejecución no continúa al siguiente caso,
por lo que no tienes que indicar, explícitamente, la salida del ciclo
al final del código de cada caso.

<!--
  Omitting mention of "fallthrough" keyword.
  It's in the guide/reference if you need it.
-->

Puedes usar `for`-`in` para iterar sobre los elementos de un diccionario,
proporcionando un par de nombres a usar
para cada par llave-valor.
Los diccionarios son colecciones sin un orden particular,
por lo que se itera sobre sus llaves y valores
de manera arbitraria.

<!--
  REFERENCE
  Prime, square, and Fibonacci numbers
  are just convenient sets of numbers
  that many developers are already familiar with
  that we can use for some simple math.
-->

```swift
let numerosInteresantes = [
    "Primos": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Cuadrados": [1, 4, 9, 16, 25],
]
var numeroMayor = 0

for (_, numeros) in numerosInteresantes {
    for numero in numeros {
        if numero > numeroMayor {
            numeroMayor = numero
        }
    }
}

print(numeroMayor)
// Imprime "25"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let interestingNumbers = [
         "Prime": [2, 3, 5, 7, 11, 13],
         "Fibonacci": [1, 1, 2, 3, 5, 8],
         "Square": [1, 4, 9, 16, 25],
     ]
  -> var largest = 0
  -> for (_, numbers) in interestingNumbers {
         for number in numbers {
             if number > largest {
                 largest = number
             }
         }
     }
  -> print(largest)
  <- 25
  ```
-->

> Experimento: Reemplaza `_` por el nombre de una variable
> y hazle seguimiento al tipo de número que resultó ser el mayor.

Usa `while` para repetir un bloque de código hasta que una condición cambie.
La condición de un ciclo puede ir al final, para asegurar que este se ejecute al menos una vez.

<!--
  REFERENCE
  This example is rather skeletal -- m and n are pretty boring.
  I couldn't come up with anything suitably interesting at the time though,
  so I just went ahead and used this.
-->

```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Imprime "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Imprime "128"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var n = 2
  -> while n < 100 {
         n *= 2
     }
  -> print(n)
  <- 128
  ---
  -> var m = 2
  -> repeat {
         m *= 2
     } while m < 100
  -> print(m)
  <- 128
  ```
-->

> Experimento:
> Cambia la condición de `m < 100` a `m < 0`
> para ver cómo `while` y `repeat`-`while` se comportan diferente
> cuando la condición del ciclo es verdadera desde un inicio.

Es posible tener índices en un ciclo,
mediante el uso de `..<` para crear un rango de índices.

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Imprime "6"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var total = 0
  -> for i in 0..<4 {
         total += i
     }
  -> print(total)
  <- 6
  ```
-->

Usa `..<` para crear un rango que omita el valor superior,
y usa `...` para crear uno que incluya ambos valores.

## Funciones y clausuras

Usa `func` para declarar una función.
Para llamar una función,
escribe una lista de argumentos en paréntesis después de su nombre.
Usa `->` para separar el nombre de los parámetros y sus tipos
del tipo que devuelve la función.

<!--
  REFERENCE
  Bob is used as just a generic name,
  but also a callout to Alex's dad.
  Tuesday is used on the assumption that lots of folks would be reading
  on the Tuesday after the WWDC keynote.
-->

```swift
func saludar(persona: String, dia: String) -> String {
    return "Hola, \(persona), hoy es \(dia)."
}
saludar(persona: "Bob", dia: "martes")
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func greet(person: String, day: String) -> String {
         return "Hello \(person), today is \(day)."
     }
  >> let greetBob =
  -> greet(person: "Bob", day: "Tuesday")
  >> print(greetBob)
  << Hello Bob, today is Tuesday.
  ```
-->

> Experimento: Remueve el parámetro `dia`.
> Agrega un parámetro que incluya el almuerzo especial de hoy en el saludo.

Por defecto,
las funciones usan los nombres de sus parámetros
como etiquetas para sus argumentos.
Crea tu propia etiqueta de argumento anteponiéndola al nombre del parámetro,
o agrega `_` para no usar una etiqueta de argumento.

```swift
func saludar(_ persona: String, el dia: String) -> String {
    return "Hola, \(persona), hoy es \(dia)."
}
saludar("John", el: "miércoles")
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func greet(_ person: String, on day: String) -> String {
         return "Hello \(person), today is \(day)."
     }
  >> let greetJohn =
  -> greet("John", on: "Wednesday")
  >> print(greetJohn)
  << Hello John, today is Wednesday.
  ```
-->

Usa una tupla para crear un valor compuesto;
por ejemplo, para devolver múltiples valores desde una función.
Los elementos de una tupla se pueden referenciar
bien sea por nombre o por número.

<!--
  REFERENCE
  Min, max, and sum are convenient for this example
  because they're all simple operations
  that are performed on the same kind of data.
  This gives the function a reason to return a tuple.
-->

```swift
func calcularEstadisticas(puntajes: [Int]) -> (min: Int, max: Int, suma: Int) {
    var min = puntajes[0]
    var max = puntajes[0]
    var suma = 0

    for puntaje in puntajes {
        if puntaje > max {
            max = puntaje
        } else if puntaje < min {
            min = puntaje
        }
        suma += puntaje
    }

    return (min, max, suma)
}
let estadisticas = calcularEstadisticas(puntajes: [5, 3, 100, 3, 9])
print(estadisticas.suma)
// Imprime "120"
print(estadisticas.2)
// Imprime "120"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
         var min = scores[0]
         var max = scores[0]
         var sum = 0

         for score in scores {
             if score > max {
                 max = score
             } else if score < min {
                 min = score
             }
             sum += score
         }

         return (min, max, sum)
     }
  -> let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
  >> print(statistics)
  << (min: 3, max: 100, sum: 120)
  -> print(statistics.sum)
  <- 120
  -> print(statistics.2)
  <- 120
  ```
-->

Las funciones pueden anidarse.
Las funciones anidadas tienen acceso a variables
que hayan sido declaradas en la función externa.
Puedes usar funciones anidadas
para organizar el código de una función
que es larga o compleja.

```swift
func devolverQuince() -> Int {
    var y = 10
    func agregar() {
        y += 5
    }
    agregar()
    return y
}
devolverQuince()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func returnFifteen() -> Int {
         var y = 10
         func add() {
             y += 5
         }
         add()
         return y
     }
  >> let fifteen =
  -> returnFifteen()
  >> print(fifteen)
  << 15
  ```
-->

Las funciones son un tipo de primera clase.
Esto quiere decir que una función puede devolver otra función como su valor.

```swift
func crearIncrementador() -> ((Int) -> Int) {
    func agregarUno(numero: Int) -> Int {
        return 1 + numero
    }
    return agregarUno
}
var incrementar = crearIncrementador()
incrementar(7)
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func makeIncrementer() -> ((Int) -> Int) {
         func addOne(number: Int) -> Int {
             return 1 + number
         }
         return addOne
     }
  -> var increment = makeIncrementer()
  >> let incrementResult =
  -> increment(7)
  >> print(incrementResult)
  << 8
  ```
-->

Una función puede tomar a otra función como uno de sus argumentos.

```swift
func coincideAlguno(lista: [Int], condicion: (Int) -> Bool) -> Bool {
    for elemento in lista {
        if condicion(elemento) {
            return true
        }
    }
    return false
}
func menorQueDiez(numero: Int) -> Bool {
    return numero < 10
}
var numeros = [20, 19, 7, 12]
coincideAlguno(lista: numeros, condicion: menorQueDiez)
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
         for item in list {
             if condition(item) {
                 return true
             }
         }
         return false
     }
  -> func lessThanTen(number: Int) -> Bool {
         return number < 10
     }
  -> var numbers = [20, 19, 7, 12]
  >> let anyMatches =
  -> hasAnyMatches(list: numbers, condition: lessThanTen)
  >> print(anyMatches)
  << true
  ```
-->

Las funciones son, en realidad, un caso especial de las clausuras:
bloques de código que pueden ser llamados más tarde.
El código en una clausura tiene acceso a elementos como variables y funciones
que están disponibles en el ámbito en el cual se creó la clausura,
incluso si la clausura se encuentra en un ámbito diferente al ejecutarse;
ya has visto un ejemplo de esto con las funciones anidadas.
Puedes crear una clausura anónima
al encerrar el código en llaves (`{}`).
Usa `in` para separar los argumentos y el tipo devuelto por la función
del cuerpo de la función.

```swift
numeros.map({ (numero: Int) -> Int in
    let resultado = 3 * numero
    return resultado
})
```

<!--
  - test: `guided-tour`

  ```swifttest
  >> let numbersMap =
  -> numbers.map({ (number: Int) -> Int in
         let result = 3 * number
         return result
     })
  >> print(numbersMap)
  << [60, 57, 21, 36]
  ```
-->

> Experimento: Reescribe la clausura de manera que devuelva cero
> para todos los números impares.

Existen muchas maneras de crear una clausura de forma más concisa.
Cuando se conoce el tipo de una clausura,
como en el caso de un *callback* para un delegado,
puedes omitir el tipo de sus parámetros,
el tipo devuelto, o ambos.
Las clausuras de una sola sentencia devuelven el valor
de su única sentencia de manera implícita.

```swift
let numerosMapeados = numeros.map({ numero in 3 * numero })
print(numerosMapeados)
// Imprime "[60, 57, 21, 36]"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let mappedNumbers = numbers.map({ number in 3 * number })
  -> print(mappedNumbers)
  <- [60, 57, 21, 36]
  ```
-->

Puedes referenciar parámetros por número en vez de nombre;
este enfoque es, especialmente, útil para clausuras muy concisas.
Una clausura que se pasa como el último argumento de una función
puede aparecer inmediatamente después de los paréntesis.
Cuando una clausura es el único argumento de una función,
puedes omitir los paréntesis por completo.

```swift
let numerosOrdenados = numeros.sorted { $0 > $1 }
print(numerosOrdenados)
// Imprime "[20, 19, 12, 7]"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let sortedNumbers = numbers.sorted { $0 > $1 }
  -> print(sortedNumbers)
  <- [20, 19, 12, 7]
  ```
-->

<!--
  Called sorted() on a variable rather than a literal to work around an issue in Xcode.  See <rdar://17540974>.
-->

<!--
  Omitted sort(foo, <) because it often causes a spurious warning in Xcode.  See <rdar://17047529>.
-->

<!--
  Omitted custom operators as "advanced" topics.
-->

## Objetos y clases

Usa `class` seguido del nombre de la clase para crear una clase.
La declaración de una propiedad en una clase, se escribe igual
que la declaración de una constante o variable,
excepto que esta existiría en el contexto de una clase.
Similarmente, la declaración de métodos y funciones se hace de la misma forma.

<!--
  REFERENCE
  Shapes are used as the example object
  because they're familiar and they have a sense of properties
  and a sense of inheritance/subcategorization.
  They're not a perfect fit --
  they might be better off modeled as structures --
  but that wouldn't let them inherit behavior.
-->

```swift
class Figura {
    var numeroDeLados = 0
    func descripcionBasica() -> String {
        return "Una figura con \(numeroDeLados) lados."
    }
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class Shape {
         var numberOfSides = 0
         func simpleDescription() -> String {
             return "A shape with \(numberOfSides) sides."
         }
     }
  >> print(Shape().simpleDescription())
  << A shape with 0 sides.
  ```
-->

> Experimento: Agrega una propiedad constante con `let`
> y otro método que tome un argumento.

Crea una instancia de una clase
al poner paréntesis después del nombre de la clase.
Usa la sintaxis de punto para acceder
a las propiedades y métodos de la instancia.

```swift
var figura = Figura()
figura.numeroDeLados = 7
var descripcionDeLaFigura = figura.descripcionBasica()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var shape = Shape()
  -> shape.numberOfSides = 7
  -> var shapeDescription = shape.simpleDescription()
  >> print(shapeDescription)
  << A shape with 7 sides.
  ```
-->

A esta versión de la clase `Figura` le hace falta algo importante:
un inicializador que configure la clase al crear una instancia.
Usa `init` para crear uno.

```swift
class FiguraConNombre {
    var numeroDeLados: Int = 0
    var nombre: String

    init(nombre: String) {
       self.nombre = nombre
    }

    func descripcionBasica() -> String {
       return "Una figura con \(numeroDeLados) lados."
    }
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class NamedShape {
         var numberOfSides: Int = 0
         var name: String
  ---
         init(name: String) {
            self.name = name
         }
  ---
         func simpleDescription() -> String {
            return "A shape with \(numberOfSides) sides."
         }
     }
  >> print(NamedShape(name: "test name").name)
  << test name
  >> print(NamedShape(name: "test name").simpleDescription())
  << A shape with 0 sides.
  ```
-->

Observa cómo se usa `self` para diferenciar la propiedad `nombre`
del argumento (del inicializador) `nombre`.
Al crear una instancia de una clase,
los argumentos del inicializador se pasan como cuando se llama una función.
Cada propiedad requiere que se le asigne un valor,
bien sea al declararla (como con `numeroDeLados`)
o en el inicializador (como con `nombre`).

Usa `deinit` para crear un «desinicializador» (*deinitializer*)
si necesitas llevar a cabo alguna limpieza
antes de que el objeto sea «desasignado» (*deallocated*).

Las subclases incluyen el nombre de su súperclase
después de su propio nombre,
separados por una coma.
No es requerimiento para las clases *subclasificar* ninguna clase base estándar,
por lo que puedes incluir u omitir una súperclase si así lo requieres.

Los métodos de una subclase que sustituyen la implementación de una súperclase
se marcan con `override`;
sustituir un método por accidente, sin usar `override`,
es detectado por el compilador como un error.
El compilador también detecta métodos con `override`
que no sustituyen ningún método de la súperclase.

```swift
class Cuadrado: FiguraConNombre {
    var longitudDeLosLados: Double

    init(longitudDeLosLados: Double, nombre: String) {
        self.longitudDeLosLados = longitudDeLosLados
        super.init(nombre: nombre)
        numeroDeLados = 4
    }

    func area() -> Double {
        return longitudDeLosLados * longitudDeLosLados
    }

    override func descripcionBasica() -> String {
        return "Un cuadrado con lados de longitud \(longitudDeLosLados)."
    }
}
let prueba = Cuadrado(longitudDeLosLados: 5.2, name: "mi cuadrado de prueba")
prueba.area()
prueba.descripcionBasica()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class Square: NamedShape {
         var sideLength: Double
  ---
         init(sideLength: Double, name: String) {
             self.sideLength = sideLength
             super.init(name: name)
             numberOfSides = 4
         }
  ---
         func area() -> Double {
             return sideLength * sideLength
         }
  ---
         override func simpleDescription() -> String {
             return "A square with sides of length \(sideLength)."
         }
     }
  -> let test = Square(sideLength: 5.2, name: "my test square")
  >> let testArea =
  -> test.area()
  >> print(testArea)
  << 27.040000000000003
  >> let testDesc =
  -> test.simpleDescription()
  >> print(testDesc)
  << A square with sides of length 5.2.
  ```
-->

> Experimento: Crea otra subclase de `FiguraConNombre`
> llamada `Circulo`,
> que tome un radio y un nombre
> como argumentos para su inicializador.
> Implementa los métodos `area()` y `descripcionBasica()`
> en la clase `Circulo`.

Aparte de ser simples propiedades que se pueden almacenar,
las propiedades pueden tener un *getter* y un *setter*.

```swift
class TrianguloEquilatero: FiguraConNombre {
    var longitudDeLosLados: Double = 0.0

    init(longitudDeLosLados: Double, nombre: String) {
        self.longitudDeLosLados = longitudDeLosLados
        super.init(nombre: nombre)
        numeroDeLados = 3
    }

    var perimetro: Double {
        get {
             return 3.0 * longitudDeLosLados
        }
        set {
            longitudDeLosLados = newValue / 3.0
        }
    }

    override func descripcionBasica() -> String {
        return "Un triángulo equilátero con lados de longitud \(longitudDeLosLados)."
    }
}
var triangulo = TrianguloEquilatero(longitudDeLosLados: 3.1, nombre: "un triángulo")
print(triangulo.perimetro)
// Imprime "9.3"
triangulo.perimetro = 9.9
print(triangulo.longitudDeLosLados)
// Imprime "3.3000000000000003"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class EquilateralTriangle: NamedShape {
         var sideLength: Double = 0.0
  ---
         init(sideLength: Double, name: String) {
             self.sideLength = sideLength
             super.init(name: name)
             numberOfSides = 3
         }
  ---
         var perimeter: Double {
             get {
                  return 3.0 * sideLength
             }
             set {
                 sideLength = newValue / 3.0
             }
         }
  ---
         override func simpleDescription() -> String {
             return "An equilateral triangle with sides of length \(sideLength)."
         }
     }
  -> var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
  -> print(triangle.perimeter)
  <- 9.3
  -> triangle.perimeter = 9.9
  -> print(triangle.sideLength)
  <- 3.3000000000000003
  ```
-->

En el *setter* de `perimetro`,
el nuevo valor tiene el nombre implícito de `newValue`.
Puedes proporcionar un nombre explícito en paréntesis después de `set`.

Observa que el inicializador de la clase `TrianguloEquilatero`
tiene tres pasos diferentes:

1. Establecer el valor de las propiedades declaradas por la subclase.
2. Llamar al inicializador de la súperclase.
3. Cambiar el valor de las propiedades definidas por la súperclase.
   Cualquier otra configuración adicional que use métodos, *getters*, o *setters*
   también puede llevarse a cabo en este punto.

Si no necesitas calcular la propiedad,
pero igual necesitas proporcionar código
para ejecutar antes y después de establecer un nuevo valor,
usa `willSet` y `didSet`.
El código que proporciones se ejecutará
cada vez que el valor cambie fuera del inicializador.
Por ejemplo, la clase a continuación se asegura
de que la longitud de los lados de su triángulo
siempre sea la misma que la longitud de los lados de su cuadrado.

<!--
  This triangle + square example could use improvement.
  The goal is to show why you would want to use willSet,
  but it was constrained by the fact that
  we're working in the context of geometric shapes.
-->

```swift
class TrianguloYCuadrado {
    var triangulo: TrianguloEquilatero {
        willSet {
            cuadrado.longitudDeLosLados = newValue.longitudDeLosLados
        }
    }
    var cuadrado: Cuadrado {
        willSet {
            triangulo.longitudDeLosLados = newValue.longitudDeLosLados
        }
    }
    init(tamano: Double, nombre: String) {
        cuadrado = Cuadrado(longitudDeLosLados: tamano, nombre: nombre)
        triangulo = TrianguloEquilatero(longitudDeLosLados: tamano, nombre: nombre)
    }
}
var trianguloYCuadrado = TrianguloYCuadrado(tamano: 10, nombre: "otra figura de prueba")
print(trianguloYCuadrado.cuadrado.longitudDeLosLados)
// Imprime "10.0"
print(trianguloYCuadrado.triangulo.longitudDeLosLados)
// Imprime "10.0"
trianguloYCuadrado.cuadrado = Cuadrado(longitudDeLosLados: 50, nombre: "cuadrado más grande")
print(trianguloYCuadrado.triangulo.longitudDeLosLados)
// Imprime "50.0"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class TriangleAndSquare {
         var triangle: EquilateralTriangle {
             willSet {
                 square.sideLength = newValue.sideLength
             }
         }
         var square: Square {
             willSet {
                 triangle.sideLength = newValue.sideLength
             }
         }
         init(size: Double, name: String) {
             square = Square(sideLength: size, name: name)
             triangle = EquilateralTriangle(sideLength: size, name: name)
         }
     }
  -> var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
  -> print(triangleAndSquare.square.sideLength)
  <- 10.0
  -> print(triangleAndSquare.triangle.sideLength)
  <- 10.0
  -> triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
  -> print(triangleAndSquare.triangle.sideLength)
  <- 50.0
  ```
-->

<!--
  Grammatically, these clauses are general to variables.
  Not sure what it would look like
  (or if it's even allowed)
  to use them outside a class or a struct.
-->

Al trabajar con valores opcionales,
puedes escribir `?` antes de operaciones como métodos, propiedades, y *subscripting*.
Si el valor antes de `?` es `nil`,
todo lo que sigue a `?` es ignorado
y el valor de toda la expresión es `nil`.
En caso contrario, se extrae el valor opcional
y todo lo que sigue a `?` opera sobre el valor extraído.
En ambos casos,
el valor de toda la expresión es un valor opcional.

```swift
let cuadradoOpcional: Cuadrado? = Cuadrado(longitudDeLosLados: 2.5, nombre: "cuadrado opcional")
let longitudDeLosLados = cuadradoOpcional?.longitudDeLosLados
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
  -> let sideLength = optionalSquare?.sideLength
  ```
-->

## Enumeraciones y estructuras

Usa `enum` para crear una enumeración.
Al igual que las clases y todos los demás tipos con nombre,
las enumeraciones pueden tener métodos asociados con ellas.

<!--
  REFERENCE
  Playing cards work pretty well to demonstrate enumerations
  because they have two aspects, suit and rank,
  both of which come from a small finite set.
  The deck used here is probably the most common,
  at least through most of Europe and the Americas,
  but there are many other regional variations.
-->

```swift
enum Escala: Int {
    case _as = 1
    case dos, tres, cuatro, cinco, seis, siete, ocho, nueve, diez
    case jack, reina, rey

    func descripcionBasica() -> String {
        switch self {
        case ._as:
            return "as"
        case .jack:
            return "jack"
        case .reina:
            return "reina"
        case .rey:
            return "rey"
        default:
            return String(self.rawValue)
        }
    }
}
let _as = Escala._as
let valorBrutoDeAs = _as.rawValue
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> enum Rank: Int {
         case ace = 1
         case two, three, four, five, six, seven, eight, nine, ten
         case jack, queen, king
  ---
         func simpleDescription() -> String {
             switch self {
                 case .ace:
                     return "ace"
                 case .jack:
                     return "jack"
                 case .queen:
                     return "queen"
                 case .king:
                     return "king"
                 default:
                     return String(self.rawValue)
             }
         }
     }
  -> let ace = Rank.ace
  -> let aceRawValue = ace.rawValue
  >> print(aceRawValue)
  << 1
  ```
-->

> Experimento: Crea una función que compare dos valores de tipo `Escala`
> comparando sus valores brutos.

De manera predeterminada, Swift asigna los valores brutos comenzando por cero
y aumentando en uno cada vez,
pero puedes cambiar dicho comportamiento al especificar valores explícitamente.
En el ejemplo anterior, `_as` recibe, explícitamente, un valor bruto de `1`
y el resto de los valores brutos se asignan en orden.
También puedes usar cadenas de texto o números de coma flotante
como el tipo bruto de una enumeración.
Usa la propiedad `rawValue` para acceder al valor bruto del caso de una enumeración.

Utiliza el inicializador `init?(rawValue:)`
para crear una instancia de una enumeración a partir de un valor bruto.
Este inicializador devuelve el caso (de la enumeración)
que coincida con el valor bruto
o `nil` si no existe una enumeración `Escala`.

```swift
if let escalaTransformada = Escala(rawValue: 3) {
    let descripcionDelTres = escalaTransformada.descripcionBasica()
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> if let convertedRank = Rank(rawValue: 3) {
         let threeDescription = convertedRank.simpleDescription()
  >> print(threeDescription)
  << 3
  -> }
  ```
-->

Los valores de los casos de una enumeración son valores reales,
y no solo otra forma de escribir sus valores brutos.
De hecho,
en los casos en los que no existe un valor bruto significativo,
no es necesario que proporciones uno.

```swift
enum Palo {
    case picas, corazones, diamantes, treboles

    func descripcionBasica() -> String {
        switch self {
        case .picas:
            return "picas"
        case .corazones:
            return "corazones"
        case .diamantes:
            return "diamantes"
        case .treboles:
            return "treboles"
        }
    }
}
let corazones = Palo.corazones
let descripcionDeCorazones = corazones.descripcionBasica()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> enum Suit {
         case spades, hearts, diamonds, clubs
  ---
         func simpleDescription() -> String {
             switch self {
                 case .spades:
                     return "spades"
                 case .hearts:
                     return "hearts"
                 case .diamonds:
                     return "diamonds"
                 case .clubs:
                     return "clubs"
             }
         }
     }
  -> let hearts = Suit.hearts
  -> let heartsDescription = hearts.simpleDescription()
  >> print(heartsDescription)
  << hearts
  ```
-->

> Experimento: Crea un método `color()` para la enumeración `Palo`
> que devuelva “negro” para picas y tréboles, y “rojo” para corazones y diamantes.

<!--
  Suits are in Bridge order, which matches Unicode order.
  In other games, orders differ.
  Wikipedia lists a good half dozen orders.
-->

Fíjate en las dos formas en las que se hizo referencia
al caso `corazones` de la enumeración:
al asignar un valor a la constante `corazones`,
el caso `Palo.corazones` se referencia por su nombre completo
porque no se especificó un tipo explícito para la constante.
Dentro del ciclo `switch`,
el caso se referencia mediante la forma abreviada `.corazones`
porque ya sabemos que el valor de `self` es un tipo de palo.
Puedes utilizar la forma abreviada
cada vez que conozcas el tipo del valor por anticipado.

Si una enumeración tiene valores brutos,
se establece que dicho valores forman parte de la declaración,
lo que significa que cada instancia de un caso de enumeración en particular
siempre tendrá el mismo valor bruto.
Otra opción para los casos de enumeraciones
es tener valores asociados con el caso;
estos valores se determinan al crear la instancia
y pueden ser diferentes para cada instancia de un caso de enumeración.
Puedes ver a los valores asociados
como valores que se comportan de manera similar a las propiedades almacenadas
de la instancia del caso de enumeración.
Por ejemplo,
considera el caso en el que se le pide a un servidor
las horas de salida y puesta del sol.
El servidor responderá con la información solicitada
o responderá con una descripción de lo que haya salido mal.

<!--
  REFERENCE
  The server response is a simple way to essentially re-implement Optional
  while sidestepping the fact that I'm doing so.

  "Out of cheese" is a reference to a Terry Pratchet book,
  which features a computer named Hex.
  Hex's other error messages include:

       - Out of Cheese Error. Redo From Start.
       - Mr. Jelly! Mr. Jelly! Error at Address Number 6, Treacle Mine Road.
       - Melon melon melon
       - +++ Wahhhhhhh! Mine! +++
       - +++ Divide By Cucumber Error. Please Reinstall Universe And Reboot +++
       - +++Whoops! Here comes the cheese! +++

  These messages themselves are references to BASIC interpreters
  (REDO FROM START) and old Hayes-compatible modems (+++).

  The "out of cheese error" may be a reference to a military computer
  although I can't find the source of this story anymore.
  As the story goes, during the course of a rather wild party,
  one of the computer's vacuum tube cabinets
  was opened to provide heat to a cold room in the winter.
  Through great coincidence,
  when a cheese tray got bashed into it during the celebration,
  the computer kept on working even though some of the tubes were broken
  and had cheese splattered & melted all over them.
  Tech were dispatched to make sure the computer was ok
  and told add more cheese if necessary --
  the officer in charge said that he didn't want
  an "out of cheese error" interrupting the calculation.
-->

```swift
enum RespuestaDelServidor {
    case resultado(String, String)
    case falla(String)
}

let exito = RespuestaDelServidor.resultado("6:00 am", "6:30 pm")
let error = RespuestaDelServidor.falla("Se ha agotado el queso.")

switch exito {
case let .resultado(amanecer, atardecer):
    print("El amanecer es a las \(amanecer) y el atardecer es a las \(atardecer).")
case let .falla(mensaje):
    print("Error... \(mensaje)")
}
// Imprime "El amanecer es a las 6:00 am y el atardecer es a las 6:30 pm."
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> enum ServerResponse {
         case result(String, String)
         case failure(String)
     }
  ---
  -> let success = ServerResponse.result("6:00 am", "8:09 pm")
  -> let failure = ServerResponse.failure("Out of cheese.")
  ---
  -> switch success {
         case let .result(sunrise, sunset):
             print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
         case let .failure(message):
             print("Failure...  \(message)")
     }
  <- Sunrise is at 6:00 am and sunset is at 8:09 pm.
  ```
-->

> Experimento: Agrega un tercer caso a `RespuestaDelServidor` y al ciclo `switch`.

Observa cómo las horas del amanecer y del atardecer
se extraen del valor `RespuestaDelServidor`
como parte de la comparación del valor con los casos del ciclo `switch`.

Usa `struct` para crear una estructura.
Las estructuras soportan muchos de los mismos comportamientos que las clases,
incluyendo métodos e inicializadores.
Una de las diferencias más importantes
entre las estructuras y las clases es que
las estructuras siempre se copian cuando se pasan en el código,
mientras que las clases se pasan por referencia.

```swift
struct Carta {
    var escala: Escala
    var palo: Palo
    func descripcionBasica() -> String {
        return "El \(escala.descripcionBasica()) de \(palo.descripcionBasica())"
    }
}
let tresDePicas = Carta(escala: .tres, palo: .picas)
let descripcionDelTresDePicas = tresDePicas.descripcionBasica()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> struct Card {
         var rank: Rank
         var suit: Suit
         func simpleDescription() -> String {
             return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
         }
     }
  -> let threeOfSpades = Card(rank: .three, suit: .spades)
  -> let threeOfSpadesDescription = threeOfSpades.simpleDescription()
  >> print(threeOfSpadesDescription)
  << The 3 of spades
  ```
-->

> Experimento: Crea una función que devuelva un arreglo que contenga
> una baraja completa de cartas,
> con una carta de cada combinación de escala y palo.

## Concurrencia

Usa `async` para marcar una función que se ejecuta de manera asíncrona:

```swift
func buscarIDDeUsuario(en servidor: String) async -> Int {
    if servidor == "principal" {
        return 97
    }
    return 501
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func fetchUserID(from server: String) async -> Int {
         if server == "primary" {
             return 97
         }
         return 501
     }
  ```
-->

Para marcar el llamado a una función asíncrona,
agrega la palabra clave `await` antes de la invocación de la función:

```swift
func buscarNombreDeUsuario(en servidor: String) async -> String {
    let idDeUsuario = await buscarIDDeUsuario(en: servidor)
    if idDeUsuario == 501 {
        return "John Appleseed"
    }
    return "Visitante"
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func fetchUsername(from server: String) async -> String {
         let userID = await fetchUserID(from: server)
         if userID == 501 {
             return "John Appleseed"
         }
         return "Guest"
     }
  ```
-->

Usa `async let` para llamar a una función asíncrona
permitiéndole ejecutarse en paralelo con otro código asíncrono.
Si necesitas usar el valor que devuelve, utiliza `await`:

```swift
func conectarUsuario(a servidor: String) async {
    async let idDeUsuario = buscarIDDeUsuario(en: servidor)
    async let nombreDeUsuario = buscarNombreDeUsuario(en: servidor)
    let saludo = await "Hola, \(nombreDeUsuario), ID de usuario \(idDeUsuario)"
    print(greeting)
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func connectUser(to server: String) async {
         async let userID = fetchUserID(from: server)
         async let username = fetchUsername(from: server)
         let greeting = await "Hello \(username), user ID \(userID)"
         print(greeting)
     }
  ```
-->

Usa `Task` para invocar funciones asíncronas desde código sincrónico,
sin tener que esperar a que estas devuelvan su valor.

```swift
Task {
    await conectarUsuario(a: "primario")
}
// Imprime "Hola, Visitante, ID de usuario 97"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> Task {
         await connectUser(to: "primary")
     }
  >> import Darwin; sleep(1)  // Pause for task to run
  <- Hello Guest, user ID 97
  ```
-->

Usa grupos de tareas para estructurar código concurrente.

```swift
let idsDeUsuarios = await withTaskGroup(of: Int.self) { taskGroup in
    for servidor in ["primario", "secundario", "desarrollo"] {
        taskGroup.addTask {
            return await buscarIDDeusuario(en: servidor)
        }
    }

    var resultados: [Int] = []
    for await resultado in taskGroup {
        resultados.append(resultado)
    }
    return resultados
}
```

Los actoreis son similares a las clases,
excepto que estos aseguran que diferentes funciones asíncronas
puedan interactuar de manera segura con una instancia del mismo actor al mismo tiempo.

```swift
actor ConexionAlServidor {
    var servidor: String = "primario"
    private var usuariosActivos: [Int] = []
    func conectar() async -> Int {
        let idDeUsuario = await buscarIDDeUsuario(en: servidor)
        // ... Comunicación con el servidor ...
        usuariosActivos.append(idDeUsuario)
        return idDeUsuario
    }
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> actor Oven {
         var contents: [String] = []
         func bake(_ food: String) -> String {
             contents.append(food)
             // ... wait for food to bake ...
             return contents.removeLast()
         }
     }
  ```
-->

Cuando llamas a un método de un actor o accedes a una de sus propiedades,
marcas dicho código con `await`
para indicar que podría tener que esperar a que otro código
que ya se está ejecutando en el actor termine.

```swift
let servidor = ConexionAlServidor()
let idDeUsuario = await servidor.conectar()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let oven = Oven()
  -> let biscuits = await oven.bake("biscuits")
  ```
-->

## Protocolos y extensiones

Usa `protocol` para declarar un protocolo.

```swift
protocol EjemploDeProtocolo {
     var descripcionBasica: String { get }
     mutating func ajustar()
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> protocol ExampleProtocol {
          var simpleDescription: String { get }
          mutating func adjust()
     }
  ```
-->

Las clases, enumeraciones, y estructuras pueden adoptar protocolos.

<!--
  REFERENCE
  The use of adjust() is totally a placeholder
  for some more interesting operation.
  Likewise for the struct and classes -- placeholders
  for some more interesting data structure.
-->

```swift
class ClaseBasica: EjemploDeProtocolo {
     var descripcionBasica: String = "Una clase muy básica."
     var otraPropiedad: Int = 69105
     func ajustar() {
          descripcionBasica += " Ahora 100% ajustada."
     }
}
var a = ClaseBasica()
a.ajustar()
let descripcionDeA = a.descripcionBasica

struct EstructuraBasica: EjemploDeProtocolo {
     var descripcionBasica: String = "Una estructura básica"
     mutating func ajustar() {
          descripcionBasica += " (ajustada)"
     }
}
var b = EstructuraBasica()
b.ajustar()
let descripcionDeB = b.descripcionBasica
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class SimpleClass: ExampleProtocol {
          var simpleDescription: String = "A very simple class."
          var anotherProperty: Int = 69105
          func adjust() {
               simpleDescription += "  Now 100% adjusted."
          }
     }
  -> var a = SimpleClass()
  -> a.adjust()
  -> let aDescription = a.simpleDescription
  >> print(aDescription)
  << A very simple class.  Now 100% adjusted.
  ---
  -> struct SimpleStructure: ExampleProtocol {
          var simpleDescription: String = "A simple structure"
          mutating func adjust() {
               simpleDescription += " (adjusted)"
          }
     }
  -> var b = SimpleStructure()
  -> b.adjust()
  -> let bDescription = b.simpleDescription
  >> print(bDescription)
  << A simple structure (adjusted)
  ```
-->

> Experimento: Agrega otro requerimiento a `EjemploDeProtocolo`.
> ¿Qué cambios debes hacer en
> `ClaseBasica` y `EstructuraBasica`
> de manera que estas sigan estando en conformidad con el protocolo?

Observa el uso de la palabra clave `mutating`
en la declaración de `EstructuraBasica`
para marcar un método que modifica la estructura.
La declaración de `ClaseBasica` no requiere
que ninguno de sus métodos esté marcado como mutante
ya que los métodos de una clase siempre pueden modificar la clase misma.

Utiliza `extension` para agregar funcionalidad a un tipo existente,
como nuevos métodos y propiedades calculadas.
Puedes usar una extensión para hacer que un tipo se ajuste a un protocolo,
bien sea un tipo que se declara en otro lugar,
o incluso un tipo que importas desde una biblioteca o *framework*.

```swift
extension Int: EjemploDeProtocolo {
    var descripcionBasica: String {
        return "El número \(self)"
    }
    mutating func ajustar() {
        self += 42
    }
 }
print(7.descripcionBasica)
// Imprime "El número 7"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> extension Int: ExampleProtocol {
         var simpleDescription: String {
             return "The number \(self)"
         }
         mutating func adjust() {
             self += 42
         }
      }
  -> print(7.simpleDescription)
  <- The number 7
  ```
-->

> Experimento: Crea una extensión para el tipo `Double`
> que agregue la propiedad `valorAbsoluto`.

Puedes usar el nombre de un protocolo como cualquier otro tipo con nombre;
por ejemplo, para crear una colección de objetos
que tiene tipos diferentes,
pero que todos se ajusten a un solo protocolo.
Al trabajar con valores cuyo tipo es un tipo de protocolo,
los métodos externos a la definición del protocolo no estarán disponibles.

```swift
let valorProtocolo: any EjemploDeProtocolo = a
print(valorProtocolo.descripcionBasica)
// Imprime "Una clase muy básica. Ahora 100% ajustada."
// print(valorProtocolo.otraPropiedad)  // Habilita esta línea para ver el error
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let protocolValue: ExampleProtocol = a
  -> print(protocolValue.simpleDescription)
  <- A very simple class.  Now 100% adjusted.
  // print(protocolValue.anotherProperty)  // Uncomment to see the error
  ```
-->

Aun cuando el tipo de runtime de la variable `valorProtocolo`
es del tipo `ClaseBasica`,
el compilador la trata como el tipo dado de `EjemploDeProtocolo`.
Esto significa que no puedes acceder, de manera accidental,
a métodos o propiedades que la clase implementa
además de su conformidad con el protocolo.

## Manejo de errores

Para representar errores, usa cualquier tipo que adopte el protocolo `Error`.

<!--
  REFERENCE
  PrinterError.OnFire is a reference to the Unix printing system's "lp0 on
  fire" error message, used when the kernel can't identify the specific error.
  The names of printers used in the examples in this section are names of
  people who were important in the development of printing.

  Bi Sheng is credited with inventing the first movable type out of porcelain
  in China in the 1040s.  It was a mixed success, in large part because of the
  vast number of characters needed to write Chinese, and failed to replace
  wood block printing.  Johannes Gutenberg is credited as the first European
  to use movable type in the 1440s --- his metal type enabled the printing
  revolution.  Ottmar Mergenthaler invented the Linotype machine in the 1884,
  which dramatically increased the speed of setting type for printing compared
  to the previous manual typesetting.  It set an entire line of type (hence
  the name) at a time, and was controlled by a keyboard.  The Monotype
  machine, invented in 1885 by Tolbert Lanston, performed similar work.
-->

```swift
enum ErrorDeLaImpresora: Error {
    case sinPapel
    case sinToner
    case enLlamas
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> enum PrinterError: Error {
         case outOfPaper
         case noToner
         case onFire
     }
  ```
-->

Usa `throw` para arrojar un error
y `throws` para marcar una función que puede arrojar un error.
Si arrojas un error en una función,
la función se interrumpe inmediatamente y el código que llamó a la función
se encargará de manejar el error.

```swift
func enviar(tarea: Int, impresoraDestino nombreDeImpresora: String) throws -> String {
    if nombreDeImpresora == "Nunca Tiene Toner" {
        throw ErrorDeLaImpresora.sinToner
    }
    return "Tarea enviada"
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func send(job: Int, toPrinter printerName: String) throws -> String {
         if printerName == "Never Has Toner" {
             throw PrinterError.noToner
         }
         return "Job sent"
     }
  ```
-->

Hay muchas maneras de manejar los errores.
Una de ellas es usar `do`-`catch`.
Dentro del bloque `do`,
marcas todo código que pueda arrojar un error,
agregando `try` delante del mismo.
Dentro del bloque `catch`,
al error se le asigna automáticamente el nombre `error`,
a menos que le asignes un nombre diferente.

```swift
do {
    let respuestaDeImpresora = try enviar(tarea: 1040, impresoraDestino: "Bi Sheng")
    print(respuestaDeImpresora)
} catch {
    print(error)
}
// Imprime "Tarea enviada"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> do {
         let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
         print(printerResponse)
     } catch {
         print(error)
     }
  <- Job sent
  ```
-->

> Experimento: Cambia el nombre de la impresora a `“Nunca Tiene Toner”`,
> de manera que la función `enviar(tarea:impresoraDestino:)` arroje un error.

<!--
  Assertion tests the change that the Experiment box instructs you to make.
-->

<!--
  - test: `guided-tour`

  ```swifttest
  >> do {
         let printerResponse = try send(job: 500, toPrinter: "Never Has Toner")
         print(printerResponse)
     } catch {
         print(error)
     }
  <- noToner
  ```
-->

Puedes usar múltiples bloques `catch`
que manejen errores específicos.
Para ello, escribe un patrón después de `catch` al igual que harías
después de `case` en un ciclo `switch`.

<!--
  REFERENCE
  The "rest of the fire" quote comes from The IT Crowd, season 1 episode 2.
-->

```swift
do {
    let respuestaDeImpresora = try enviar(tarea: 1440, impresoraDestino: "Gutenberg")
    print(respuestaDeImpresora)
} catch ErrorDeLaImpresora.enLlamas {
    print("Dejaré esto por aquí, con el resto del fuego.")
} catch let errorDeLaImpresora as ErrorDeLaImpresora {
    print("Error de la impresora: \(errorDeLaImpresora).")
} catch {
    print(error)
}
// Imprime "Tarea enviada"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> do {
         let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
         print(printerResponse)
     } catch PrinterError.onFire {
         print("I'll just put this over here, with the rest of the fire.")
     } catch let printerError as PrinterError {
         print("Printer error: \(printerError).")
     } catch {
         print(error)
     }
  <- Job sent
  ```
-->

> Experimento: Añade código para arrojar un error dentro del bloque `do`.
> ¿Qué tipo de error es necesario arrojar
> para que este sea manejado por el primer bloque `catch`?
> ¿Qué tal con los bloques segundo y tercero?

Otra forma de manejar los errores
es usar `try?` para convertir el resultado en un opcional.
Si la función arroja un error,
el error específico es descartado y el resultado es `nil`.
En caso contrario, el resultado es un opcional
que contiene el valor devuelto por la función.

```swift
let exitoImpresora = try? enviar(tarea: 1884, impresoraDestino: "Mergenthaler")
let fallaImpresora = try? enviar(tarea: 1885, impresoraDestino: "Nunca Tiene Toner")
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
  >> print(printerSuccess as Any)
  << Optional("Job sent")
  -> let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
  >> print(printerFailure as Any)
  << nil
  ```
-->

Usa `defer` para crear un bloque de código
que se ejecute después de todo el código de una función,
justo antes de que la función devuelva su valor.
El código se ejecuta sin importar que la función arroje un error.
Puedes utilizar `defer` para escribir códigos de configuración y limpieza,
uno al lado del otro,
aun cuando estos deban ejecutarse en momentos diferentes.

```swift
var elRefrigeradorEstaAbierto = false
let contenidoDelRefrigerador = ["leche", "huevos", "sobras"]

func elRefrigeradorContiene(_ alimento: String) -> Bool {
    elRefrigeradorEstaAbierto = true
    defer {
        elRefrigeradorEstaAbierto = false
    }

    let resultado = contenidoDelRefrigerador.contains(alimento)
    return resultado
}
if elRefrigeradorContiene("banano") {
    print("Hay un banano")
}
print(elRefrigeradorEstaAbierto)
// Imprime "false"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var fridgeIsOpen = false
  -> let fridgeContent = ["milk", "eggs", "leftovers"]
  ---
  -> func fridgeContains(_ food: String) -> Bool {
         fridgeIsOpen = true
         defer {
             fridgeIsOpen = false
         }
  ---
         let result = fridgeContent.contains(food)
         return result
     }
  >> let containsBanana =
  -> fridgeContains("banana")
  >> print(containsBanana)
  << false
  -> print(fridgeIsOpen)
  <- false
  ```
-->

## Genéricos

Escribe un nombre entre paréntesis angulares (`<>`)
para crear una función o tipo genéricos.

<!--
  REFERENCE
  The four knocks is a reference to Dr Who series 4,
  in which knocking four times is a running aspect
  of the season's plot.
-->

```swift
func crearArreglo<Item>(repitiendo item: Item, numeroDeVeces: Int) -> [Item] {
    var resultado: [Item] = []
    for _ in 0..<numeroDeVeces {
         resultado.append(item)
    }
    return resultado
}
crearArreglo(repitiendo: "toc", numeroDeVeces: 4)
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
         var result: [Item] = []
         for _ in 0..<numberOfTimes {
              result.append(item)
         }
         return result
     }
  >> let fourKnocks =
  -> makeArray(repeating: "knock", numberOfTimes: 4)
  >> print(fourKnocks)
  << ["knock", "knock", "knock", "knock"]
  ```
-->

También puedes crear formas genéricas de funciones y métodos,
como también de clases, enumeraciones, y estructuras.

```swift
// Reimplementa el tipo opcional de la librería estándar de Swift
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var posibleEntero: OptionalValue<Int> = .none
posibleEntero = .some(100)
```

<!--
  - test: `guided-tour`

  ```swifttest
  // Reimplement the Swift standard library's optional type
  -> enum OptionalValue<Wrapped> {
         case none
         case some(Wrapped)
     }
  -> var possibleInteger: OptionalValue<Int> = .none
  -> possibleInteger = .some(100)
  ```
-->

Utiliza `where` justo antes del cuerpo de la función
para especificar una lista de requerimientos;
por ejemplo,
para requerir el tipo para implementar un protocolo,
para requerir que dos tipos sean el mismo,
o para requerir que una clase tenga una súperclase en particular.

```swift
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
    where T.Element: Equatable, T.Element == U.Element
{
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
   return false
}
anyCommonElements([1, 2, 3], [3])
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
         where T.Element: Equatable, T.Element == U.Element
     {
         for lhsItem in lhs {
             for rhsItem in rhs {
                 if lhsItem == rhsItem {
                     return true
                 }
             }
         }
        return false
     }
  >> let hasAnyCommon =
  -> anyCommonElements([1, 2, 3], [3])
  >> print(hasAnyCommon)
  << true
  ```
-->

> Experimento: Modifica la función `anyCommonElements(_:_:)`
> para crear una función que devuelva un arreglo
> de los elementos que dos secuencias cualesquiera tienen en común.

Escribir `<T: Equatable>`
es lo mismo que escribir `<T> ... where T: Equatable`.

<!--
This source file is part of the Swift.org open source project

Copyright (c) 2014 - 2023 Apple Inc. and the Swift project authors
Licensed under Apache License v2.0 with Runtime Library Exception

See https://swift.org/LICENSE.txt for license information
See https://swift.org/CONTRIBUTORS.txt for the list of Swift project authors
-->
