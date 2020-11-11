Creando un paquete de R
=======================

.. admonition:: Objetivos

   - Aprender qué es un paquete de R.
   - Conocer las principales partes de un paquete.
   - Crear un paquete de R usando RStudio.


.. admonition:: Referencias

   `R Packages (Hadley Wickham, Jennifer Bryan) <https://r-pkgs.org/preface
   .html>`_

¿Qué es un paquete de R?
------------------------

En R, la unidad fundamental de código que se puede compartir es el paquete.
Un paquete puede agrupar código, datos, documentación y tests, y, además, es
fácil de compartir con otros.

Esta última característica es la que ha situado a R entre los lenguajes de
programación más usados en el mundo. Como actualmente existen más de 14000
paquetes en el `CRAN <https://cran.r-project.org/>`__, la probabilidad de
que alguien haya resuelto nuestra necesidad (o problema) es muy alto. Por lo
tanto, en lugar de implementar nosotros las solución, podemos beneficiarnos del
trabajo de otro descargandonos su paquete.


Estructura de un paquete
------------------------

La estructura más básica de un paquete de R es la siguiente:

.. code-block:: none

   /
   ├── DESCRIPTION
   ├── NAMESPACE
   └── R/
       └── ...


Metadatos
+++++++++

El fichero ``DESCRIPTION`` contiene todos los metadatos que describen el
paquete:


.. code-block:: none

   Package: project
   Title: What the Package Does (One Line, Title Case)
   Version: 0.0.0.9000
   Authors@R:
       person(given = "First",
              family = "Last",
              role = c("aut", "cre"),
              email = "first.last@example.com",
              comment = c(ORCID = "YOUR-ORCID-ID"))
   Description: What the package does (one paragraph).
   License: `use_mit_license()`, `use_gpl3_license()` or friends to
       pick a license
   Encoding: UTF-8
   LazyData: true
   Roxygen: list(markdown = TRUE)
   RoxygenNote: 7.1.1

- ``Package``: indica el nombre del paquete.

- ``Title``: contiene la descripción en una línea del paquete. Debe ser texto
  sin formato.

- ``Version``: determina la versión actual del paquete.

  .. seealso:: Información sobre como determinar el número de versión:
     `<https://r-pkgs.org/release.html#release-version>`_.

- ``Authors``: muestra información sobre los autores del paquete.


  - El nombre está especificado por los parametros ``given`` (nombre) y
    ``family`` (apellidos).
  - La dirección de correo electrónico se encuentra en ``email``.
  - El rol de cada persona en el paquete (autor o creador) está descrito por el
    campo ``rol``.

- ``Description``: contiene una descripción del paquete más detallada que el
  título. Puede contener varias oraciones, pero está limitada a un párrafo.

- ``License``: indica la licencia que usa el paquete. En software de código
  abierto, una de las licencias más permisivas es la `licencia MIT
  <https://opensource.org/licenses/MIT>`__.


Ficheros de R
+++++++++++++

El directorio ``R/``, tal y como su propio nombre indica, contiene todo el
código R que necesita el paquete.

Así, todas las funciones usadas en el paquete van a estar implementadas
en ficheros incluidos en esta carpeta. En concreto, estas funciones de R
deben estar implementadas en scripts de R, es decir, en ficheros con la
extensión ``.R``.


Espacio de nombres
++++++++++++++++++

Finalmente, el fichero ``NAMESPACE`` contiene las funciones que los usuarios
externos del paquete van a poder usar cuando lo importen desde R.

Este fichero se genera de forma automática usando el paquete `roxygen2
<https://cran.r-project.org/web/packages/roxygen2/vignettes/roxygen2.html>`__
(lo veremos en profundidad en la `lección 3 <../03/index.html>`__).

Práctica
--------

Antes de pasar a la creación de nuestro paquete, es recomendable instalar los
paquete `usethis <https://usethis.r-lib.org>`_ y `devtools
<https://www.r-project.org/nosvn/pandoc/devtools.html>`__, ya que nos
van a facilitar todo el desarrollo. Estos paquetes se pueden instalar ejecutando
desde la consola de R los siguientes comandos:

.. code-block:: R

   install.packages("usethis")
   install.packages("devtools")


Creación del paquete
++++++++++++++++++++

En primer lugar abrimos RStudio y en la consola de R ejecutamos el siguiente
comando:

.. code-block:: R

   usethis::create_package("~/SIQ025")

Al ejecutar este comando se nos abrirá otra pantalla de RStudio en el
directorio ``~/SIQ025`` de nuestro ordenador. Como podemos ver, en este
directorio se ha creado de forma automática la estructura básica del paquete
(vista anteriormente).

Ahora, abrimos el fichero ``DESCRITION``, lo rellenamos con los datos
de nuestro paquete y lo guardamos.

.. note::

   Inidcar que se puede copiar este ejemplo o proponer otro.

En mi caso, el fichero quedaría de la siguiente forma:

.. code-block:: none

   Package: SIQ025
   Title: Software de modelización de sistemas industriales
   Version: 0.0.0.9000
   Authors@R:
       person(given = "Aleix",
              family = "Alcacer",
              role = c("cre"),
              email = "aalcacer@uji.com")
   Description: SIQ025 es un paquete de R creado en la asignatura de
       modelización de sistemas industriales. Esta asignatura está incluida
       dentro del máster en Matemática Computacional de la UJI.
   License: use_mit_license()
   Encoding: UTF-8
   LazyData: true
   Roxygen: list(markdown = TRUE)
   RoxygenNote: 7.1.1

Una vez completado el fichero ``DESCRIPTION`` pasamos a crear las funciones
del paquete. Por ahora, solo implementaremos dos funciones: una que calcule la
suma dos números y otra que calcule la diferencia.

Para ello, crearemos dentro del directorio ``R/`` dos ficheros llamados
``suma.R`` y ``resta.R``. En el primero de ellos, insertaremos el siguiente
código:


.. code-block:: R
   :linenos:

   suma <- function(a, b) {
     return(a + b)
   }


y en el otro, insertaremos:

.. code-block:: R
   :linenos:

   resta <- function(a, b) {
     return(a - b)
   }


En este momento, ya hemos implementado nuestro pirmer paquete de R. La
estructura que tenemos ahora tiene que ser:

.. code-block:: none

   /
   ├── DESCRIPTION
   ├── NAMESPACE
   └── R/
       ├── suma.R
       └── resta.R

Finalmente, para poder usar el paquete de R, tenemos que compilar el paquete
e instalarlo. Para ello, tenemos que ejecutar los siguientes comandos desde
la consola de R:

.. code-block:: R

   devtools::build()    # Compila el paquete
   devtools::install()  # Instala el paquete
   .rs.restartR()       # Reinicia la sessión de R


Hecho esto, ya podemos usar nuestro paquete de R desde RStudio:

.. code-block:: R

   > SIQ025:::suma(5, 6)
   [1] 11
   > SIQ025:::resta(7, 11)
   [1] -4