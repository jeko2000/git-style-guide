# Guía de estilo para Git

Esta guía de estilo para Git esta inspirada por [*How to Get Your Change 
Into the Linux Kernel*](https://www.kernel.org/doc/documentation/submittingpatches.html),
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
* [Japonés](https://github.com/objectx/git-style-guide)
* [Portugués](https://github.com/guylhermetabosa/git-style-guide)
* [Ruso](https://github.com/alik0211/git-style-guide)
* [Tailandés](https://github.com/zondezatera/git-style-guide)
* [Turco](https://github.com/CnytSntrk/git-style-guide)
* [Ucraniano](https://github.com/denysdovhan/git-style-guide)

Si deseas contribuir, hazle un fork al proyecto e inicia un pull 
request.

# Tabla de contenido

1. [Branches](#branches)
2. [Commits](#commits)
  1. [Mensajes](#mensajes)
3. [Merging](#merging)
4. [Misc.](#misc)

## Branches

* Usa nombres *cortos* y *descriptivos* para tus ramas o branches:

  ```shell
  # bien
  $ git checkout -b migracion_de_api

  # mal - poco descriptivo
  $ git checkout -b simple_arreglo
  ```

* Identificadores correspondientes a problemas, tickets, o issues de un 
servicio externo como aquellos de Github pueden ser usados para nombrar
tus branches. Por ejemplo:

  ```shell
  # GitHub Issue #15
  $ git checkout -b issue-15
  ```

* Usa *guiones* para separar palabras.

* Si existen varias personas trabajando en la misma parte, 
  característica o feature del proyecto, puede ser conveniente tener un 
  branch para todo el equipo y otros branches *personales* para cada 
  persona.

  ```shell
  $ git checkout -b feature-a/master # Branch del equipo entero
  $ git checkout -b feature-a/maria  # Branch personal de María
  $ git checkout -b feature-a/nick   # Branch personal de Nick
  ```

  Se pueden hacer integraciones o merges desde las ramas/branches 
  personales al branch del equipo (ver ["Merging"](#merging)).
  Eventualmente, el branch del equipo será integrado a "master".

* Elimina tu branch del repositorio remoto después de haber sido 
  integrado a menos que sea necesario guardarlo.

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
  *Consejo: Usa `git add-p` para interactivamente montar/stage 
  partes específicas de los archivos modificados.*

* No separes un solo *cambio lógico* en varios commits. Por ejemplo, una 
nueva implementación junto con sus pruebas o tests correspondientes 
deben de estar en el mismo commit.

* Realiza commits *temprano* y *frecuentemente*. Commits que son 
pequeños y autónomos son más fáciles de entender y revertir si algo sale
mal.

* Los commits deben de ser ordenados *lógicamente*. Por ejemplo, 
si el *commit A* depende de los cambios hechos en *commit B*, entonces, 
el *commit B* debe de realizarse antes del *commit A*.

### Mensajes

* Usa tu editor y no tu terminal cuando escribes un mensaje para el 
  commit. Realizar commits desde la terminal te hace pensar que es 
  necesario hacer que quepa todo en una sola linea lo cual usualmente 
  resulta en mensajes ambiguos y poco informativos.

  ```shell
  # bien
  $ git commit

  # mal
  $ git commit -m "Correción rápida"
  ```

* La línea de resumen, es decir, la primera linea del mensaje de commit,
  debe ser *descriptiva* y al igual *concisa*. Idealmente, esta línea 
  no debe de tener más de *50 caracteres*. Debe de hacer uso correcto de
  mayúsculas y también debe ser escrita en el imperativo. No es 
  necesario que termine en punto final puesto que sirve como el *título*
  del commit.

  ```shell
  # bien - modo imperativo, usa mayúsculas y tiene menos de 50 caracteres
  Marcar registros como obsoletos tras falla

  # malo
  arreglé ActiveModel::Mensajes de error cuando AR fue usado correctamente fuera de Rails
  ```

* Después del título debe ir una línea en blanco seguida por una 
descripción más a fondo del commit. Cada línea debe de tener 72 
caracteres o menos y debe de explicar la *razón* por la cual el cambio 
era necesario. Preguntas acerca de cómo el cambio tomó lugar son 
respondidas por el cambio en sí y sus efectos. El mensaje también debe 
de vincular otros recursos relacionados como el número de un issue
correspondiente:

  ```shell
  Resumen corto de no más de 50 caracteres.
  
  Texto opcional detallando aspectors del cambio en el commit donde
  cada linea debe tener un máximo de 72 caracteres.

  Recuerda que si decides incluír texto despues del título, la linea 
  en blanco entre el título y el cuerpo es necesaria. Esto es debido
  a que herramientas como rebase se pueden confundir si juntas el
  título de un commit con su cuerpo.
  
  En ciertas situaciones, la primera linea del mensaje se 
  trata como el asunto de un correo electrónico y el resto del mensaje 
  como su cuerpo.
  
  Párrafos adicionaes vienen despues de líneas en blanco.
  
  - Se pueden crear listas con guiones o asteriscos.
  
  * Esta lista empieza con un asterisco y un espacio y espera líneas
  en blanco entre artículos de la lista.
  
  Vínculos a recursos relacionados pueden ser agregados al final del
  mensaje:
  
  Corrige: #56, #78
  Véase también: #12, #34

  Fuente http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
  ```

  Al final cuando escribes el mensaje de un commit, piensa sobre qué 
  necesitarías saber si te encuentras con este commit después de un año.

* Si un *commit A* depende de *commit B*, la dependencia debe de ser
  escrita en el mensaje de *commit A* refiriéndote a *commit B* por su 
  respectivo hash.

  Similarmente, si un *commit A* corrige un problema introducido por 
  *commit B*, éste también debe ser escrito en el mensaje de *commit A*.
  
* Si un commit ha de entrar al proceso de squash con respecto a otro,
debe ser escrito como tal para hacer la intención clara:

  ```shell
  $ git commit --squash f387cab2
  ```

 *(Consejo: Usa `--autosquash` al realizar un rebase. Los commits 
 marcados entraran al procesa de squash automáticamente.)*

## Merging

* **No re-escribas el historial ya publicado.** El historial de un 
repositorio es muy valioso ya que muy importante poder saber 
*qué ocurrió exactamente* en un momento dado. Alteraciones al historial
es una fuente común de errores en muchos proyectos.

* Sin embargo, existen casos legítimos en los cuales reescribir el
historial es aceptable. Estos casos son cuando:

   * Tú eres el único trabajando en el branch y el branch no será
   revisado.
   
   * Tú quieres reorganizar tu branch (p. ej. squash commits) y/o 
   hacer un rebase de tu branch con respecto a "master".

   Con esto dicho, *nunca re-escribas la historia del branch "master"*
   o de cualquier otro branch especial como aquellos usados en 
   producción o en los servidores.

* Mantén el historial *limpio* y *simple*. *Antes de someter tu branch 
  a un merge*:
  
    1. Asegúrate que se acomoda a la guía de estilo escogida para el
    proyecto.
    
    2. Haz un rebase con respecto al branch que ha de recibir el merge:

       ```shell
       [mi-branch] $ git fetch
       [mi-branch] $ git rebase origin/master
       # Ahora haz el merge
       ```

       Esto resulta en un branch que puede ser directamente aplicado al 
       final del branch "master" lo cual simplifica el historial del 
       proyecto.

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

* Existen varios estilos, flujos de trabajo o workflows y cada uno tiene
  sus ventajas y desventajas. El hecho de que un flujo encaje con un
  proyecto en específico depende del equipo, de aspectos del proyecto 
  en sí y de sus procesos de desarrollo. *Lo que es importante es poder 
  escoger un estilo y usarlo a través del proyecto.*
  
* *Sé consistente.* Esto es relacionado con el estilo pero ha de 
  expandirse a cosas como mensajes de commit, nombres de tus branches y 
  etiquetas/tags. El tener un estilo constante en el repositorio 
  facilita su entendimiento a través del log y de los mensajes de 
  sus commits.

* *Prueba/haz tests antes del push*. No hagas un push con un trabajo no 
  terminado.

* Usa [Tags Anotadas](http://git-scm.com/book/en/v2/Git-Basics-Tagging#Annotated-Tags) 
 para marcar lanzamientos/releases u otros puntos importantes en el 
 historial.
  
* Usa [Tags Ligeras](http://git-scm.com/book/en/v2/Git-Basics-Tagging#Lightweight-Tags) 
  para uso personal, como para marcar commits y facilitar su búsqueda 
  en el futuro.
  
* Mantén tus repositorios en buenas condiciones al hacerles 
  mantenimiento ocasionalmente:

  * [`git-gc(1)`](http://git-scm.com/docs/git-gc)
  * [`git-prune(1)`](http://git-scm.com/docs/git-prune)
  * [`git-fsck(1)`](http://git-scm.com/docs/git-fsck)

# Licencia

![cc license](http://i.creativecommons.org/l/by/4.0/88x31.png)

Este trabajo está licenciado bajo la licencia [Creative Commons Attribution 4.0
International license](https://creativecommons.org/licenses/by/4.0/).

# Créditos

Agis Anastasopoulos / [@agisanast](https://twitter.com/agisanast) / http://agis.io

# Traducción
Johnny Ruiz / [jeko2000](https://github.com/jeko2000)

