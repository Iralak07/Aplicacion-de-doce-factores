# Aplicacion de doce factores

## I. Base de Código
### Definición:

Una base de código es esencialmente el conjunto de archivos fuente que constituyen tu aplicación. Estos archivos están versionados y controlados en sistemas de control de versiones como Git, Mercurial o Subversion. La base de código es única para cada aplicación, aunque esa aplicación puede tener múltiples "implementaciones" (o versiones activas) en diferentes entornos.
Ejemplo:

Imagina que tienes una aplicación web llamada FinApp que obtiene y muestra datos financieros. Esta aplicación tiene una base de código que incluye:

    Archivos Python para el backend.
    Archivos JavaScript para el frontend.
    Archivos de configuración para el entorno de desarrollo.

Todos estos archivos se rastrean en un repositorio de Git que sirve como la "base de código" de la aplicación FinApp.

Una base de código, múltiples implementaciones

Cada aplicación tiene una sola base de código, pero puede haber múltiples implementaciones o instancias de esa aplicación que estén en diferentes entornos, como:

    Desarrollo: Donde los programadores trabajan en nuevas funciones y correcciones.
    Pruebas o Staging: Donde el equipo de control de calidad prueba la aplicación antes de lanzarla al público.
    Producción: El entorno donde los usuarios finales interactúan con la aplicación.

Ejemplo:

Volviendo a FinApp:

    Los desarrolladores pueden trabajar en su entorno local con una copia de la base de código (versión de desarrollo).
    La aplicación puede estar desplegada en un entorno de pruebas donde los testers validan que todo funcione correctamente antes de lanzarla a producción.
    Finalmente, esa misma base de código se despliega en un entorno de producción, donde los usuarios finales pueden acceder a la aplicación en línea.

Aunque hay diferentes versiones activas de la aplicación en desarrollo, pruebas y producción, todas estas instancias comparten la misma base de código.
Una sola aplicación por base de código

    Regla: Si tienes una aplicación, debes tener solo una base de código. Esto significa que cada aplicación debe tener su propio repositorio.
    Violación: Si varias aplicaciones utilizan el mismo código, no estás siguiendo el principio de una base de código por aplicación. Por ejemplo, si una parte del código se comparte entre dos aplicaciones diferentes, ese código debería extraerse a una biblioteca común y manejarse como una dependencia.

Ejemplo de violación:

Imagina que creas otra aplicación llamada UserApp que también utiliza el mismo código para autenticación que FinApp. Si copias el código de autenticación en ambas aplicaciones, estarías violando este principio. En lugar de duplicar el código, lo correcto sería crear una biblioteca común (una librería de autenticación) y que ambas aplicaciones dependan de esa librería.
Versiones de la base de código en diferentes implementaciones

Cada entorno puede tener una versión diferente del código activo:

    Los desarrolladores locales pueden tener algunos cambios que no están en pruebas o producción.
    El entorno de pruebas puede tener algunos cambios que aún no han llegado a producción.
    El entorno de producción puede tener una versión más estable, sin los últimos cambios.

Ejemplo:

En FinApp, podrías tener esta situación:

    Un desarrollador ha realizado cambios para una nueva funcionalidad, pero esos cambios solo están presentes en su entorno local.
    El equipo de control de calidad está probando una versión de la aplicación que tiene algunos cambios que aún no están en producción.
    Los usuarios finales están utilizando la versión en producción, que es estable y no contiene los cambios más recientes que se están probando o desarrollando.



