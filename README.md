# Guía de estilo para Git

Esta guía de estilo para Git esta inspirada por [*How to Get Your
Change Into the Linux
Kernel*](https://www.kernel.org/doc/documentation/submittingpatches.html),
las páginas del [manual de git](http://git-scm.com/doc) y varias
prácticas ahora actualmente populares dentro de la comunidad.

Traducciones para esta guía están en disponibles en los siguientes
idiomas:

* [Alemán](https://github.com/runjak/git-style-guide)
* [Chino Simplificado](https://github.com/aseaday/git-style-guide)
* [Chino Tradicional](https://github.com/JuanitoFatas/git-style-guide)
* [Coreano](https://github.com/ikaruce/git-style-guide)
* [Francés](https://github.com/pierreroth64/git-style-guide)
* [Griego](https://github.com/grigoria/git-style-guide)
* [Inglés](https://github.com/agis/git-style-guide)
* [Japonés](https://github.com/objectx/git-style-guide)
* [Portugués](https://github.com/guylhermetabosa/git-style-guide)
* [Ruso](https://github.com/alik0211/git-style-guide)
* [Tailandés](https://github.com/zondezatera/git-style-guide)
* [Turco](https://github.com/CnytSntrk/git-style-guide)
* [Ucraniano](https://github.com/denysdovhan/git-style-guide)

Si deseas contribuir, hazle un fork al proyecto e inicia un pull
request.

# Tabla de contenido

0. [Notas del traductor](#notas-del-traductor)
1. [Branches](#branches)
2. [Commits](#commits)
  1. [Mensajes](#mensajes)
3. [Merging](#merging)
4. [Misc.](#misc)

## Notas del traductor
Queridos lectores:

Una dificultad presente al escribir esta guía es la de decidir que
traducción usar para los diversos conceptos y términos usados por Git.
Esto se debe a que autores usan diferentes palabras en español para
referirse al mismo termino en inglés. Por ende, y con el fin de
reducir la posible confusión entre estos diferentes términos, me he
tomado la libertad de mayormente usar ciertos términos específicos en
su inglés originario. Dicho esto, también intento proveer traducciones
al español en una que otra ocasión. Favor, no dudar de escribirme si
alguna palabra en inglés causa confusion innecesaria.

Cordialmente, jeko2000

## Branches

* Usa nombres *cortos* y *descriptivos* para tus ramas o branches:

  ```shell
  # bien
  $ git checkout -b migración_del_api

  # mal - poco descriptivo
  $ git checkout -b arreglo_sencillo
  ```

* Identificadores correspondientes a problemas, tickets, o issues de
  un servicio externo como aquellos de Github pueden ser usados para
  nombrar tus branches. Por ejemplo:

  ```shell
  # Issue de Github #15
  $ git checkout -b issue-15
  ```

* Nombra tus ramas en letra minúscula con la posible excepción de
  identificadores externos. Usa *guiones* para separar palabras.

  ```shell
  $ git checkout -b nueva-característica  # bien
  $ git checkout -b T321-característica   # bien (Identificador T321)
  $ git checkout -b Nueva_Característica  # mal
  ```

* Si existen varias personas trabajando en la *misma* característica,
  puede ser conveniente tener branches *personales* para cada miembro
  del equipo y un branch para el equipo entero. En tales casos, usa la
  siguiente convención:

  ```shell
  $ git checkout -b feature-a/master # Branch del equipo entero
  $ git checkout -b feature-a/maria  # Branch personal de María
  $ git checkout -b feature-a/nick   # Branch personal de Nick
  ```

  Se pueden hacer integraciones o merges desde los branches personales
  al branch del equipo (ver ["Merging"](#merging)). Eventualmente, el
  branch del equipo será integrado a "master".

* Elimina tu branch del repositorio remoto después de haber sido
  integrado a menos que haya una razón especifica de no hacerlo.

  Consejo: Usa el comando a continuación desde "master" para mostrar
  branches integrados:

  ```shell
  $ git branch --merged | grep -v "\*"
  ```

## Commits

* Cada commit debe de estar compuesto por un solo *cambio lógico*. No
debes de tener varios *cambios lógicos* en un commit. Por ejemplo, si
un cambio corrige un error y, a la vez, optimiza el rendimiento de un
aspecto de la aplicación, debes separarlo en dos commits.

  *Consejo: Usa `git add-p` para interactivamente montar/stage partes
  específicas de los archivos modificados.*

* No separes un solo *cambio lógico* en varios commits. Por ejemplo,
  una nueva implementación junto con sus pruebas o tests
  correspondientes deben de estar en el mismo commit.

* Realiza commits *temprano* y *frecuentemente*. Commits que son
  pequeños y autónomos son más fáciles de entender y revertir si algo
  sale mal.

* Los commits deben de ser ordenados *lógicamente*. Por ejemplo, si el
  *commit A* depende de los cambios hechos en *commit B*, entonces, el
  *commit B* debe de realizarse antes del *commit A*.

  Nota: En caso de estar trabajando sólo en un branch local que (no se
  ha integrado*, es totalmente aceptable de usar commits para capturar
  el estado de tu trabajo. Sin embargo, sigue siendo cierto que los
  reglas descritas previamente aplican *antes* de su integración.

### Mensajes

* Usa tu editor y no tu terminal cuando escribes un mensaje para el
  commit.

  ```shell
  # bien
  $ git commit

  # mal
  $ git commit -m "Corrección rápida"
  ```

  Realizar commits desde la terminal fomenta la mentalidad de que es
  necesario hacer que quepa todo en una sola linea lo cual usualmente
  resulta en mensajes ambiguos y poco informativos.

* La línea de resumen, es decir, la primera linea del mensaje de
  commit, debe ser *descriptiva* y al igual *concisa*. Idealmente,
  esta línea no debe de tener más de *50 caracteres*. Debe de ser
  capitalizada y escrita en el imperativo. No es necesario que termine
  en punto final puesto que sirve como el *título* del commit.

  ```shell
  # bien - modo imperativo, usa mayúsculas y tiene menos de 50 caracteres
  Marcar registros como obsoletos tras falla

  # malo
  arreglé ActiveModel::Mensajes de error cuando AR fue usado correctamente fuera de Rails
  ```

* Después del título debe ir una línea en blanco seguida por una
  descripción más completa del commit. Cada línea debe de tener 72
  caracteres o menos y debe de explicar la *razón* por la cual el
  cambio es necesario, *cómo* rectifica el problema y qué *efectos
  secundarios* puede tener.

  También debe proporcionar cualquier recurso relacionado (por
  ejemplo, un enlace al issue correspondiente en el bug tracker):

  ```shell
  Resumen corto de no más de 50 caracteres.

  Texto opcional detallando aspectos del cambio en el commit donde
  cada linea debe tener un máximo de 72 caracteres. En ciertas
  situaciones, la primera linea del mensaje se trata como el asunto de
  un correo electrónico y el resto del mensaje como su cuerpo. La
  línea en blanco que separa el resumen del cuerpo es crítica (a menos
  que se omita el cuerpo en su totalidad), ya que herramientas como
  rebase se pueden llegar a confundir si ambas partes están juntas.
  
  Párrafos adicionales vienen después de líneas en blanco.
  
  - Se pueden crear listas las cuales consisten de un guión o un
  asterisco seguido por un solo espacio y con lineas en blanco entre sí.
  
  Vínculos a recursos relacionados pueden ser agregados al final del
  mensaje:
  
  Corrige: #56, #78
  Véase también: #12, #34

  Fuente http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
  ```

  Al final cuando escribes el mensaje de un commit, piensa sobre qué
  necesitarías saber si te encuentras con este commit después de un
  año.

* Si un *commit A* depende de *commit B*, la dependencia debe de ser
  escrita en el mensaje de *commit A* refiriéndote a *commit B* por su
  respectivo hash de SHA1.

  Del mismo modo, si un *commit A* corrige un error introducido por
  *commit B*, éste también se debe de indicar en el mensaje de *commit
  A*.
  
* Si un commit ha de entrar al proceso de squash con respecto a otro
  commit, usa `--squash` y `--fixup` respectivamente, con el fin que
  la intención sea clara:

  ```shell
  $ git commit --squash f387cab2
  ```

 * (Consejo: Usa `--autosquash` al realizar un rebase. Los commits
   marcados entraran al procesa de squash automáticamente.)*

## Merging

* **No re-escribas el historial ya publicado.** El historial de un
  repositorio es muy valioso ya que muy importante poder saber *qué
  ocurrió exactamente* en un momento dado. Alteraciones al historial
  es una fuente común de errores para todos aquellos trabajando en el
  proyecto.

* Sin embargo, existen casos legítimos en los cuales reescribir el
  historial es aceptable. Estos casos son cuando:

   * Tú eres el único trabajando en el branch y el branch no será
   revisado.
   
   * Tú quieres reorganizar tu branch (p. ej. squash commits) y/o
   hacer un rebase de tu branch con respecto a "master".

   Dicho esto, *nunca re-escribas la historia del branch "master"* o
   de cualquier otro branch especial como aquellos usados en
   producción o en los servidores de control de calidad.

* Mantén el historial *limpio* y *simple*. *Antes de someter tu branch
  a un merge*:
  
    1. Asegúrate que se acomoda a la guía de estilo escogida para el
       proyecto y realiza las acciones necesarias en caso de que no se
       acomode.
    
    2. Haz un rebase con respecto al branch que ha de recibir el
       merge:

       ```shell
       [mi-branch] $ git fetch
       [mi-branch] $ git rebase origin/master
       # Ahora haz el merge
       ```

       Esto resulta en un branch que puede ser directamente aplicado
       al final del branch "master" lo cual simplifica el historial
       del proyecto.

       *(Nota: Esta estrategia es más adecuada para proyectos con
       branches de corta duración. Si no es así, es posible que sea
       mejor ocasionalmente hacer un merge en vez de un rebase con la
       branch "master").*
       
* Si tu branch incluye más de un commit, no hagas un merge con
  fast-forward:

  ```shell
  # bien - asegura que un commit del merge sea creado
  $ git merge --no-ff mi-branch

  # mal
  $ git merge mi-branch
  ```

## Misc.

* Existen varios estilos, flujos de trabajo o workflows y cada uno
  tiene sus fortalezas y debilidades. El hecho de que un workflow
  encaje con un proyecto en específico depende del equipo, de aspectos
  del proyecto en sí y de tus procesos de desarrollo.
  
  Dicho esto, es importante *elegir* y mantener un workflow
  específico.

* *Se consistente.* Esto es relacionado con el workflow pero ha de
  expandirse a cosas como mensajes de commit, nombres de tus branches
  y etiquetas/tags. El tener un estilo constante en el repositorio
  hace que sea fácil entender lo que está pasando a través del log o
  registro.

* *Prueba/haz tests antes del push*. No hagas un push con un trabajo
  no terminado.

* Usa [Tags
 Anotadas](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Etiquetado)
 para marcar lanzamientos/releases u otros puntos importantes en el
 historial.
  
* Usa [Tags
  Ligeras](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Etiquetado)
  para uso personal, como para marcar commits y facilitar su búsqueda
  en el futuro.
  
* Mantén tus repositorios en buenas condiciones al hacerles
  mantenimiento ocasionalmente:

  * [`git-gc(1)`](http://git-scm.com/docs/git-gc)
  * [`git-prune(1)`](http://git-scm.com/docs/git-prune)
  * [`git-fsck(1)`](http://git-scm.com/docs/git-fsck)

# Licencia

![cc license](http://i.creativecommons.org/l/by/4.0/88x31.png)

Este trabajo está licenciado bajo la licencia [Creative Commons
Attribution 4.0 International
license](https://creativecommons.org/licenses/by/4.0/).

# Créditos

Agis Anastasopoulos / [@agisanast](https://twitter.com/agisanast) /
http://agis.io

# Traducción
Johnny Ruiz / [jeko2000](https://github.com/jeko2000)

