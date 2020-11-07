Creando un paquete de R
=======================

Objetivos a alcanzar:

- Creación de un paquete de R usando RStudio.
- Uso de un sistema de gestión de versiones.
- Sincronización de un paquete con una copia almacenada en la nube.

.. admonition:: Referencias

   `R Packages (Hadley Wickham, Jennifer Bryan) <https://r-pkgs.org/preface
   .html>`_

Inicialización del paquete
--------------------------

El primer paso que tenemos que hacer es crear en Github un repositorio
(público) titulado *SIQ025*.

A continuación, desde RStudioCloud vamos a crear un nuevo proyecto a partir
del repositorio de Github. Para ello, seleccionamos *New Project -> New
Project from Git Repository* y introducimos la url de nuestro
repositorio (*https://github.com/<username>/SIQ025.git*).
Una vez creado, abrimos el proyecto de R.

Antes de pasar a la creación de nuestro paquete, es recomendable instalar el
paquete `devtools <https://www.r-project.org/nosvn/pandoc/devtools.html>`_
para facilitar nuestro desarrollo. Este paquete se puede instalar ejecutando
desde la consola de R el siguiente comando:

.. code-block:: R
   :linenos:

   install.packages("devtools")


Estructura del paquete
----------------------

La estructura más básica de un proyecto de R es la siguiente :

.. code-block:: none

   /
   ├── DESCRIPTION
   ├── NAMESPACE
   └── R/
       └── ...

En nuestro caso, para generar todos estos ficheros simplemente tenemos que
ejecutar la siguiente instrucción desde la consola de R:

.. code-block:: R
   :linenos:

   devtools::create(".")


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

- ``Title``: contiene la descripción en una línea del paquete. Debe ser texto
  sin formato.

- ``Version``: determina la versión actual del paquete.

  .. seealso:: Información sobre como determinar el número de versión:
     `<https://r-pkgs.org/release.html#release-version>`_.

- ``Authors``: muestra información sobre los autores del paquete.


  - El nombre está especificado por los parametros ``given`` y ``family``.
  - La dirección de correo electrónico se encuentra en ``email``.
  - El rol de cada persona en el paquete (autor o creador) está descrito por el
    campo ``rol``.

- ``Description``: contiene una descripción más detallada que el título. Puede
  contener varias oraciones, pero está limitada a un párrafo.

- ``License``: indica la licencia que usa el paquete.


Una vez visto en qué consiste el fichero ``DESCRIPTION``, vamos a actualizarlo
con nuestros datos. Un ejemplo podría ser:

.. code-block:: none

   Package: SIQ025
   Title: Software de modelización de sistemas industriales
   Version: 0.0.0.9000
   Authors@R:
       person(given = "Aleix",
              family = "Alcacer",
              role = c("cre"),
              email = "aalcacer@uji.com"))
   Description: SIQ025 es un paquete de R creado en la asignatura de
       modelización de sistemas industriales. Esta asignatura está incluida
       dentro del máster en Matemática Computacional de la UJI.
   License: use_mit_license()
   Encoding: UTF-8
   LazyData: true
   Roxygen: list(markdown = TRUE)
   RoxygenNote: 7.1.1


Espacio de nombres
++++++++++++++++++

Ficheros de R
+++++++++++++
