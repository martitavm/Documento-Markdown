# Introducción a GIT

## ¿Qué es un sistema de control de versiones?
Un Sistema de Control de Versiones (SCV) es una aplicación que permite gestionar los cambios que se realizan sobre los elementos de un proyecto o repositorio, guardando así versiones del mismo en todas sus fases de desarrollo.

- Registra cada cambio en el proyecto o repositorio, quién y cuándo lo hace, en una base de datos.
- Permite volver a estados previos del desarrollo.
- Permite gestionar diferentes versiones del proyecto (ramas) para trabajar en paralelo y luego fusionarlas.
- Permite colaborar entre diferentes usuarios en un mismo repositorio, facilitando la resolución de conflictos.
- Se utiliza principalmente en proyectos de desarrollo de software, pero sirve para cualquier otro tipo de proyecto.

## ¿Qué es Git?
Git es un sistema de control de versiones de código abierto ideado por Linus Torvalds (el padre del sistema operativo Linux) y actualmente es el sistema de control de versiones más extendido.

>A diferencia de otros SCV, Git tiene una arquitectura distribuida, lo que significa que en lugar de guardar todos los cambios de un proyecto en un único sitio, cada usuario contiene una copia del repositorio con el historial de cambios completo del proyecto. Esto aumenta significativamente su rendimiento.

## Configuración de Git

| Comando                              | Descripción                                           |
|--------------------------------------|-------------------------------------------------------|
| git config --global user.name     | Establecer el nombre de usuario                      |
| git config --global user.email     | Establecer el correo del usuario                     |
| git config --global color.ui      | Activar el coloreado de la salida                    |
| git config --global merge.conflictstyle | Mostrar el estado original en los conflictos     |
| git config --list                 | Mostrar la configuración         

## Creación de un repositorio nuevo

  - `git init`: Inicializa un nuevo repositorio.
  - `git init <nombre-repositorio>`: Crea un repositorio con el nombre especificado.

## Copia de repositorios

  - `git clone <url-repositorio>`: Clona un repositorio remoto en la ubicación especificada.

## Añadir cambios a un repositorio
Con Git, cualquier cambio que hagamos en un proyecto tiene que pasar por tres estados hasta que guarde definitivamente en el repositorio.

- **Directorio de trabajo**- Es el directorio que contiene una copia de una versión concreta del proyecto en la que se está trabajando. Puede contener ficheros que no pertenecen al repositorio.
- **Zona temporal de intercambio (staging area)**- es una zona donde se guardan los cambios temporalmente desde el directorio de trabajo antes de hacerlos definitivos y registrarlos en el repositorio.
- **Repositorio**- Es donde finalmente se guardan los cambios confirmados desde la zona temporal de intercambio.

## Añadir Cambios a la Zona de Intercambio Temporal

  - `git add <fichero>`: Añade cambios en el fichero especificado a la zona de intercambio temporal.
  - `git add <carpeta>`: Añade cambios en todos los ficheros de la carpeta especificada.
  - `git add .`: Añade todos los cambios no guardados en la zona de intercambio temporal.

## Añadir Cambios al Repositorio
  
  - `git commit -m "mensaje"`: Confirma todos los cambios en la zona de intercambio temporal añadiéndolos al repositorio y creando una nueva versión del proyecto. "mensaje" es un breve mensaje describiendo los cambios realizados que se asociará a la nueva versión del proyecto.
  - `git commit --amend -m "mensaje"`: Cambia el mensaje del último commit.


![Imagen Cambios al Repositorio](https://tecadmin.net/wp-content/uploads/2023/05/explained-git-staging-area.png)

## Registro de cambios
Para guardar los cambios en un repositorio Git utiliza una estructura de **tres niveles**:

- **Commit**: Contiene información sobre el autor, el momento y el mensaje de los cambios.
- **Árbol (tree)**: Cada commit contiene además un árbol donde se registran los nombres y rutas de los ficheros en el repositorio cuando se hizo el commit.
- **Blob (binary file object)**: Para cada uno de los ficheros listados en el árbol hay un blob, que contiene una instantánea comprimida del contenido del fichero cuando se hizo el commit.

Si un fichero del repositorio no ha cambiado en el commit, el árbol apunta al blob del fichero del último commit donde el fichero cambió.

## Referenciar un commit
Cada commit tiene asociado un **código hash** de 40 caracteres hexadecimales que lo identifica de manera única. Hay dos formas de referirse a un commit:

- **Nombre absoluto:** Se utiliza su código hash (basta indicar los 4 o 5 primeros dígitos).
- **Nombre relativo:** Se utiliza la palabra **HEAD** para referirse siempre al último commit. 
  
  Para referirse al penúltimo commit se utiliza **HEAD~1**, al antepenúltimo **HEAD~2**, etc.

![Imagen Referenciar un commit](https://marklodato.github.io/visual-git-guide/basic-usage.svg)  

## Mostrar el estado de un repositorio
 
- `git status`: Muestra el estado de los cambios en el repositorio desde la última versión guardada. En particular, muestra los ficheros con cambios en el directorio de trabajo que no se han añadido a la zona de intercambio temporal y los ficheros en la zona de intercambio temporal que no se han añadido al repositorio.

## Mostrar el historial de versiones de un repositorio

- `git log`: Muestra el historial de commits de un repositorio ordenado cronológicamente.  
Para cada commit muestra su código hash, el autor, la fecha, la hora y el mensaje asociado.

Este comando es muy versátil y muestra la historia del repositorio en distintos formatos dependiendo de los parámetros que se le den. 

Los más comunes son:
- **--oneline:** Muestra cada commit en una línea produciendo una salida más compacta.
- **--graph:** Muestra la historia en forma de grafo.

## Mostrar los datos de un commit

- `git show`: Muestra el usuario, el día, la hora y el mensaje del último commit, así como las diferencias con el anterior.

- `git show<commit>`: Muestra el usuario, el día, la hora y el mensaje del commit indicado, así como las diferencias con el anterior.

## Mostrar el historial de cambios de un fichero

- `git annotate`: Muestra el contenido de un fichero anotando cada línea con información del commit en el que se introdujo.
  
Cada línea de la salida contiene los **8 primeros dígitos** del **código hash** del commit correspondiente al cambio, el autor de los cambio, la fecha, el número de línea del fichero y el contenido de la línea.

## Mostrar las diferencias entre versiones

- `git diff`: Muestra las diferencias entre el directorio de trabajo y la zona de intercambio temporal.

- `git diff --cached`: Muestra las diferencias entre la zona de intercambio temporal y el último commit.

- `git diff HEAD`: Muestra la diferencia entre el directorio de trabajo y el último commit.

## Eliminar cambios del directorio de trabajo o volver a una versión anterior

- `git checkout <commit> -- <file>`: Actualiza el fichero `<file>` a la versión correspondiente al commit `<commit>`.

Suele utilizarse para eliminar los cambios en un fichero que no han sido guardados aún en la zona de intercambio temporal, mediante el comando `git checkout HEAD -- <file>`.

## Eliminar cambios de la zona de intercambio temporal

- `git reset <fichero>`: Elimina los cambios del fichero `<fichero>` de la zona de intercambio temporal, pero preserva los cambios en el directorio de trabajo.

Para eliminar por completo los cambios de un fichero que han sido guardados en la zona de intercambio temporal hay que aplicar este comando y después `git checkout HEAD -- <fichero>`.

## Eliminar cambios de un commit

`git reset --hard <commit>`: Elimina todos los cambios desde el commit `<commit>` y actualiza el HEAD este commit.

>¡Ojo! Usar con cuidado este comando pues los cambios posteriores al commit indicado se pierden por completo.

Suele usarse para eliminar todos los cambios en el directorio de trabajo desde el último commit mediante el comando `git reset --hard HEAD`.

`git reset <commit>`: Actualiza el HEAD al commit `<commit>`, es decir, elimina todos los commits posteriores a este commit, pero no elimina los cambios del directorio de trabajo.

## Ramas

Inicialmente, cualquier repositorio tiene una única rama llamada **master (main)**, donde se van sucediendo todos los commits de manera lineal.

Una de las características más útiles de Git es que permite la creación de ramas para trabajar en distintas versiones de un proyecto a la vez, lo que facilita el desarrollo simultáneo de nuevas funcionalidades, correcciones de errores o experimentos sin interferir con el flujo de trabajo principal.

Esto es especialmente útil si se quieren añadir nuevas funcionalidades al proyecto sin que interfieran con lo desarrollado hasta ahora, permitiendo un desarrollo más organizado y controlado.

Una vez que se termina el desarrollo de las nuevas funcionalidades en una rama, estas se pueden fusionar con la rama principal **(generalmente master)** para incorporar los cambios al proyecto principal de manera ordenada y controlada, manteniendo así la integridad del código y facilitando la colaboración entre los miembros del equipo.

## Creación de ramas

`git branch <rama>`: Crea una nueva rama con el nombre `<rama>` en el repositorio a partir del último commit, es decir, donde apunte HEAD.

Al crear una rama a partir de un commit, el flujo de commits se bifurca en dos de manera que se pueden desarrollar dos versiones del proyecto en paralelo.

![Imagen Creación de ramas](https://snyk.io/_next/image/?url=https%3A%2F%2Fres.cloudinary.com%2Fsnyk%2Fimage%2Fupload%2Fv1615821731%2Fwordpress-sync%2Fimage1-11.png&w=2560&q=75)  

## Desarrollo en ramas diferentes

![Imagen Desarrollo en ramas diferentes](https://miro.medium.com/v2/resize:fit:720/format:webp/1*Q8MmK6j-P8Wb6T2zz0crJw.png)  

## Listado de ramas

`git log`: Muestra las ramas activas de un repositorio indicando con * la rama activa en ese momento.

`git log --graph --oneline`: Muestra la historia del repositorio en forma de grafo **(--graph)** incluyendo todas las ramas **(--all)**.

## Cambio de ramas

`git checkout <rama>`: Actualiza los ficheros del directorio de trabajo a la última versión del repositorio correspondiente a la rama `<rama>`, y la activa, es decir, HEAD pasa a apuntar al último commit de esta rama.

`git checkout -b <rama>`: Crea una nueva rama con el nombre `<rama>` y la activa, es decir, HEAD pasa a apuntar al último commit de esta rama. 

Este comando es equivalente aplicar los comandos `git branch <rama>` y después `git checkout <rama>`.

## Fusión de ramas

`git merge <rama>`: Integra los cambios de la rama `<rama>` en la rama actual a la que apunta HEAD.

![Imagen Fusión de ramas](https://cdn-media-1.freecodecamp.org/images/VonhijTBQgjwtRXz31wLzF7iWDnDFk2o8EWi) 

## Resolución de conflictos
Para fusionar dos ramas es necesario que **no haya conflictos** entre los cambios realizados a las dos versiones del proyecto.

Si en ambas versiones se han hecho cambios sobre la misma parte de un fichero, entonces se produce un conflicto y es necesario resolverlo antes de poder fusionar las ramas.

La resolución debe hacerse manualmente observando los cambios que interfieren y decidiendo cuales deben prevalecer, aunque existen herramientas como KDif3 o meld que facilitan el proceso.

## Reorganización de ramas

`git rebase <rama-1> <rama-2>`: Replica los cambios de la rama `<rama-2>` en la rama `<rama-1>` partiendo del ancestro común de ambas ramas. 

El resultado es el mismo que la fusión de las dos ramas pero la bifurcación de la `<rama-2>` desaparece ya que sus commits pasan a estar en la `<rama-1>`.

## Eliminación de ramas

`git branch -d <rama>`: Elimina la rama de nombre `<rama>` siempre y cuando haya sido fusionada previamente.

`git branch -D <rama>`: Elimina la rama de nombre `<rama>` incluso si no ha sido fusionada. Si la rama no ha sido fusionada previamente se perderán todos los cambios de esa rama.

## Repositorios remotos

Además de facilitar la colaboración entre distintos usuarios en un proyecto mediante la gestión de ramas, Git permite la creación de **repositorios remotos**, lo que amplía aún más las posibilidades de trabajo colaborativo y la distribución del código.

Git posibilita la creación de una copia del repositorio en un servidor git en internet, lo que se conoce como un **repositorio remoto**. La principal ventaja de tener una copia remota del repositorio es que sirve como una copia de seguridad externa, lo que garantiza la integridad y disponibilidad del código en caso de pérdida o daño en el repositorio local.

Además de su función como copia de seguridad, los repositorios remotos permiten que otros usuarios accedan a él y realicen cambios en el código. 
>Esto facilita la colaboración entre equipos distribuidos geográficamente, ya que cada miembro del equipo puede trabajar en su propia copia del repositorio y luego sincronizar los cambios con el repositorio remoto.

Aunque existen varios proveedores de alojamiento para repositorios Git, el más popular y ampliamente utilizado es **GitHub**, que ofrece una plataforma robusta y completa para la gestión de proyectos de desarrollo de software.