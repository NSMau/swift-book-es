# Contribuyendo al libro *The Swift Programming Language*

Al enviar un *pull request*,
declaras que tienes el derecho de licenciar tu contribución
a Apple y a la comunidad,
y aceptas, al enviar tus cambios,
que tus contribuciones están licenciadas bajo
la [licencia Swift](https://swift.org/LICENSE.txt).

Para cambios pequeños,
como correcciones tipográficas y revisiones dentro de unos pocos párrafos,
la discusión de dichos cambios suele ser lo suficientemente mínima
para formar parte del *pull request*.
Para cambios grandes,
como nuevos capítulos y secciones,
inicia un hilo en los [foros Swift][foro]
para discutir tu enfoque e identificar posibles problemas
antes de invertir mucho tiempo escribiendo.
En general,
el grado de discusión en torno a un cambio antes de hacer un *pull request*
corresponde al tamaño de dicho cambio.

El contenido de este libro sigue la [Guía de estilos de Apple][asg]
y [la guía de estilos de este libro][tspl-style].

[asg]: https://help.apple.com/applestyleguide/
[foro]: https://forums.swift.org/c/swift-documentation/92
[tspl-style]: /Style.md

## Trabajando en una rama *feature*

Si esta es tu primera contribución,
empieza por hacer un *fork* del repositorio Git.

En tu *fork*,
crea una nueva rama a partir de `main`,
con un nombre breve y descriptivo.
Los nombres de las ramas son efímeros:
al incorporar (*merge*) un *pull request*,
el *commit* de dicha incorporación no incluye el nombre de tu rama *feature*.

Si necesitas integrar cambios de `main` o resolver un *merge conflict*,
incorpora (*merge*) `main` en tu rama *feature*.
Antes de crear un *pull request*,
puedes *rebase* tu rama *feature* en `main`, si así lo prefieres,
pero no uses *rebase* con *commits* que hacen parte de un *pull request*.

## Escribiendo mensajes de *commits*

Usa el mensaje de *commits* de Git para comunicarte con otros colaboradores:
tanto con las personas que están trabajando en el proyecto ahora
—quienes están revisando tus cambios—,
como con las personas que se unan al proyecto en el futuro,
quienes necesitarán entender qué has cambiado y por qué.

Cada *commit* comienza con un resumen de una frase.
El resumen suele caber en 50 caracteres,
pero está bien exceder esa cantidad de vez en cuando
si reescribirlo por brevedad lo hace demasiado difícil de leer.
Si te resulta difícil escribir un buen resumen,
intenta dividir los cambios en varios *commits* más pequeños.

Si no puedes explicar el *commit* por completo en su resumen,
sáltate una línea y añade información adicional.
Esta información adicional incluye detalles como
las razones del cambio,
el enfoque que adoptaste al realizarlo,
las alternativas que consideraste,
y un resumen de lo que cambiaste.
Aplica un *hard wrap* de 72 caracteres a estas líneas
y deja una línea en blanco entre párrafos.
El cuerpo de un *commit* es texto plano,
no *markdown* como el contenido del libro.

Seguir estas convenciones de formato en tu *commit*
facilita su legibilidad
en lugares como el *output* de `git`
y en correos electrónicos de notificaciones.
La mayoría de los editores de texto
pueden ayudarte a escribir un mensaje para un *commit*
marcando las líneas que son demasiado largas
y aplicando *hard wrap* al texto automáticamente.

## Enviando un *pull request*

Sigue los siguientes pasos al crear un nuevo *pull request*:

1. Comprueba que tus cambios se compilan localmente ejecutando `docc preview TSPL.docc`.
2. Crea un *pull request* en este repositorio.
3. Escribe un breve mensaje en el *pull request* para presentar tu trabajo en contexto.

En unos días
alguien asignará revisores e iniciará una compilación en CI.

Durante la revisión del *pull request*,
añade nuevos *commits* en tu rama para incorporar la retroalimentación,
pero no uses *rebase* o *force push*.
Reescribir la historia de la rama
hace que sea difícil para los revisores ver
qué cambió desde la última vez que revisaron tus cambios.
Si hay *merge conflicts*,
incorpora (*merge*) `main` en tu rama o usa la interfaz web de GitHub
para resolver los conflictos al aceptar el *pull request*.

Una vez que un *pull request* haya sido incorporado (*merged*),
elimina la rama *feature*.
