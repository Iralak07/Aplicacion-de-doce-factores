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


## II. Dependencias

Declarar y aislar dependencias explícitamente 

Esto significa que, en lugar de asumir que las dependencias estarán disponibles en el sistema en el que se ejecuta tu aplicación, debes especificar todas las dependencias que necesita tu aplicación. Esto se hace creando un archivo o "manifiesto" que lista todas las bibliotecas o herramientas externas.

Ejemplo en Python:

En Python, se utiliza un archivo llamado requirements.txt para declarar todas las dependencias de un proyecto. En este archivo, listamos las bibliotecas que el proyecto necesita, junto con las versiones específicas.

requirements.txt:

        Django==3.2.7
        requests==2.26.0
        numpy==1.21.2

Beneficio: Si otro desarrollador o un servidor necesita instalar tu aplicación, lo único que necesita es el archivo requirements.txt y Python. No hay necesidad de adivinar qué bibliotecas adicionales podrían necesitar.

### Aislar las dependencias

El aislamiento de dependencias asegura que tu aplicación no dependa de las bibliotecas instaladas globalmente en el sistema, y que cada proyecto o aplicación tenga su propio conjunto de dependencias. Esto evita conflictos de versiones o dependencias erróneas que puedan estar presentes en el sistema.

Ejemplo en Python:

En Python, una herramienta común para el aislamiento de dependencias es Virtualenv o venv (a partir de Python 3). Con estas herramientas, puedes crear un entorno virtual que actúa como un espacio aislado para las dependencias de tu proyecto.
        
        # Crear un entorno virtual en Python
        python3 -m venv mi_entorno
        
        # Activar el entorno virtual
        source mi_entorno/bin/activate
        
        # Instalar las dependencias dentro del entorno virtual
        pip install -r requirements.txt


## III. configuración

### Almacenar la configuración en el entorno. 

El principio de configuración en las "12 Factor App" establece que la configuración de la aplicación debe almacenarse en el entorno, no en el código fuente. Veamos en detalle qué significa este principio y por qué es importante.
¿Qué es la configuración en una aplicación?

La configuración se refiere a todos los parámetros que pueden variar dependiendo del entorno donde la aplicación se ejecuta. Es decir, los valores que cambian entre desarrollo, pruebas, staging (preproducción) y producción.

Ejemplos de configuración incluyen:

    Credenciales de acceso a servicios externos (API keys, contraseñas de bases de datos, credenciales de AWS o Google Cloud, etc.).
    Identificadores de recursos como la URL de la base de datos, la dirección de un servidor Redis o Memcached.
    Parámetros específicos de la implementación, como el nombre de dominio o puerto donde la aplicación está desplegada.

En la filosofía de las 12 Factor App, la configuración que se refiere a valores que pueden variar entre entornos (como producción, desarrollo, pruebas) debe almacenarse en el entorno del sistema (como variables de entorno), no en archivos de configuración dentro del código o dispersos en diferentes formatos y ubicaciones. Esto asegura la seguridad, consistencia y portabilidad de la aplicación. Ahora, veremos cómo este principio se aplica en frameworks como Django, Flask y FastAPI, y cómo gestionar correctamente la configuración.

Configuración Interna vs. Configuración de Entorno

    Configuración Interna:
        Este tipo de configuración no cambia entre entornos y es parte del funcionamiento de la aplicación. Ejemplos incluyen la configuración de rutas en Rails o cómo se             conectan los módulos de una aplicación en Spring.
        Django: La configuración de rutas (urls.py) o la definición de vistas no varían según el entorno, y deben permanecer en el código.
        Flask y FastAPI: La configuración de rutas y la estructura básica de la aplicación también forman parte del código.

    Configuración de Entorno:
        Se refiere a credenciales, URLs de bases de datos, claves API, y cualquier otro valor que puede cambiar entre los entornos de desarrollo, staging y producción.

