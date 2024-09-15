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



## IV. Servicios de respaldo

### Trate los servicios de respaldo como recursos adjuntos 

La idea central es que cualquier servicio que una aplicación utilice (como bases de datos, sistemas de mensajería, almacenamiento de archivos, servicios de correo, etc.) se debe tratar de manera uniforme, ya sea que esté alojado localmente o sea proporcionado por un tercero. Estos servicios son denominados servicios de respaldo o recursos adjuntos.

 ¿Qué es un servicio de respaldo?

Un servicio de respaldo es cualquier recurso que la aplicación necesita para funcionar correctamente y que se consume a través de la red. Estos servicios pueden ser:

    Bases de datos: Como MySQL, PostgreSQL, MongoDB, etc.
    Sistemas de mensajería/colas: Como RabbitMQ, Kafka.
    Servicios SMTP: Para el envío de correos electrónicos, como Postfix, SendGrid.
    Sistemas de almacenamiento en caché: Como Redis, Memcached.
    Servicios externos: Como Amazon S3 (para almacenamiento de archivos), servicios de API como Google Maps o Twitter.

Estos servicios pueden estar alojados localmente (es decir, en la misma infraestructura donde se ejecuta la aplicación) o administrados por terceros (como un servicio en la nube o API externa).

Igual tratamiento para servicios locales y de terceros

Uno de los principios clave de las 12 Factor App es que la aplicación no debe distinguir entre los servicios locales y los de terceros. Esto significa que para la aplicación, no importa si la base de datos está en tu propio servidor o si la administra un proveedor en la nube (como Amazon RDS). Lo único que importa es la URL o credenciales que se usan para acceder a ese servicio, las cuales se almacenan en variables de entorno y no en el código de la aplicación.
Ejemplo práctico:

Imagina que tu aplicación usa una base de datos MySQL para almacenar datos. Esta base de datos puede estar en dos lugares:

    Localmente en tu servidor propio (usando MySQL instalado en el servidor de la empresa).
    En la nube con un proveedor como Amazon RDS.

Si sigues las buenas prácticas de las 12 Factor App, tu código no debería tener ninguna referencia directa a si la base de datos está local o en la nube. En lugar de ello, simplemente usas una variable de entorno que almacena la URL o credenciales de la base de datos.

Ejemplo:

import os
    
    # Obtenemos la URL de la base de datos desde una variable de entorno
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': os.getenv('DB_NAME'),
            'USER': os.getenv('DB_USER'),
            'PASSWORD': os.getenv('DB_PASSWORD'),
            'HOST': os.getenv('DB_HOST'),  # Puede ser localhost o una URL externa
            'PORT': os.getenv('DB_PORT', '3306'),
        }
    }

Resumen:

- Los servicios de respaldo son recursos que tu aplicación necesita para funcionar, como bases de datos, sistemas de mensajería, o servicios de almacenamiento.

- La aplicación no debe distinguir entre servicios locales y servicios de terceros. Todos los servicios deben considerarse recursos adjuntos, accedidos a través de URLs o credenciales almacenadas en variables de entorno.

- Intercambiar servicios (por ejemplo, cambiar una base de datos local por una administrada en la nube) no debería requerir cambios en el código, solo cambios en la configuración (variables de entorno).

- Cada servicio es un recurso independiente, y tu aplicación debe tratarlo como tal, asegurando que no haya acoplamiento fuerte entre el código y los recursos externos. Esto permite mayor flexibilidad y escalabilidad a largo plazo.


## V. Construir, lanzar, ejecutar

### Etapas de construcción y ejecución estrictamente separadas 

Una base de código se transforma en una implementación (sin desarrollo) a través de tres etapas: 

#### Etapa de compilación (Build Stage)

La compilación es la primera etapa del proceso de implementación. Aquí, el código fuente de la aplicación se transforma en algo que puede ser ejecutado, conocido como una compilación o build. Durante esta etapa, se descargan todas las dependencias de la aplicación y se genera el código necesario para que la aplicación pueda ejecutarse.
Pasos clave en la etapa de compilación:

    Obtener el código: La etapa de compilación toma una versión específica del código desde un repositorio (por ejemplo, una confirmación o "commit" en Git).
    Instalar dependencias: Se instalan todas las dependencias del proyecto (bibliotecas o paquetes externos).
    Compilar activos: Si tu aplicación tiene activos que necesitan ser procesados, como imágenes, archivos CSS o JavaScript, estos son compilados en esta etapa.

Ejemplo con Python y Django:

Imagina que tienes una aplicación Django almacenada en un repositorio Git. Al hacer una nueva implementación, se selecciona una versión específica del código (por ejemplo, el último commit en la rama principal) y luego se ejecuta el siguiente proceso:

Obtener código:

    git checkout main
    
Instalar dependencias (usando un archivo requirements.txt):
    
    pip install -r requirements.txt
    
Compilar activos (en Django, podrías usar collectstatic para reunir los archivos estáticos):
    
    python manage.py collectstatic

#### Etapa de lanzamiento (Release Stage)

La etapa de lanzamiento toma la compilación generada en la etapa anterior y la combina con la configuración específica de la implementación (como variables de entorno, claves de API, y otros detalles que varían según el entorno de ejecución). El resultado es una versión lista para ser ejecutada.
¿Qué ocurre en esta etapa?

    Se combinan los archivos compilados y el paquete de código con la configuración necesaria para el entorno (por ejemplo, los secretos y claves API).
    Se genera una versión específica que puede ser ejecutada inmediatamente en un entorno de ejecución (como un servidor de producción, staging, o desarrollo).

Ejemplo:

Supongamos que tu aplicación Django necesita conectarse a una base de datos PostgreSQL en el entorno de producción. Las credenciales de esta base de datos (que no están en el código, sino en las variables de entorno) se combinan con la compilación.

    export DATABASE_URL=postgres://user:password@host:port/dbname

Una vez que la configuración se combina con la compilación, la aplicación está lista para lanzarse.

#### Etapa de ejecución (Runtime Stage)

Finalmente, la etapa de ejecución es cuando la aplicación realmente se pone en marcha. Se inicia un proceso con la versión específica creada en la etapa de lanzamiento y se ejecuta en el entorno de producción o el entorno de destino.
¿Qué ocurre en esta etapa?

    Se inicia el servidor de la aplicación utilizando los archivos compilados y configurados.
    La aplicación comienza a aceptar solicitudes o a ejecutar tareas según sea necesario.

Ejemplo con Django:

Si estás usando un servidor web como Gunicorn para ejecutar la aplicación Django en un entorno de producción, el proceso de ejecución podría ser así:

    gunicorn myapp.wsgi:application --bind 0.0.0.0:8000

Aquí, la aplicación Django se ejecuta y comienza a procesar solicitudes HTTP. Este es el momento en el que los usuarios pueden interactuar con la aplicación.

#### Ejemplo completo:

Imagina que tienes una aplicación Django que se ejecuta en la nube utilizando Heroku, un servicio que sigue los principios de las 12 Factor App.

    Compilación:
        Heroku obtiene el código desde tu repositorio Git.
        Instala las dependencias listadas en requirements.txt.
        Ejecuta cualquier comando de precompilación (como python manage.py collectstatic).

    Lanzamiento:
        Heroku toma la compilación y combina las variables de entorno (como DATABASE_URL, SECRET_KEY, etc.) con la compilación.
        Se genera una versión lista para ejecutarse.

    Ejecución:
        Heroku ejecuta tu aplicación Django en un entorno controlado, utilizando un servidor como Gunicorn.
        Tu aplicación está ahora accesible en internet para que los usuarios interactúen con ella.

###VI. Procesos
### Ejecute la aplicación como uno o más procesos sin estado. 

En una aplicación de Doce Factores, los procesos son fundamentales para ejecutar el código de la aplicación, pero deben cumplir ciertas reglas para garantizar la escalabilidad, confiabilidad y portabilidad del sistema. Vamos a desglosar lo que mencionas con más detalles y ejemplos para que quede claro.

#### Procesos sin estado

En las aplicaciones de Doce Factores, los procesos que ejecutan el código de la aplicación no deben almacenar estado local. Esto significa que no deben depender de variables en memoria o del sistema de archivos local para guardar información a largo plazo. Esto se hace para que los procesos sean intercambiables y se puedan ejecutar en cualquier lugar o en cualquier momento sin perder información.

#### Escenario de producción: muchos procesos

En un entorno de producción, tu aplicación puede ejecutarse en varios procesos a la vez. Estos procesos podrían estar en diferentes servidores o instancias en la nube. Cada proceso puede manejar una parte del tráfico de la aplicación o ejecutar diferentes tipos de tareas (por ejemplo, uno para solicitudes web, otro para procesamiento en segundo plano, etc.).

En este caso, si un proceso guarda información en su propia memoria o sistema de archivos, otro proceso no tendría acceso a esa información. Esto podría causar problemas cuando diferentes procesos manejan diferentes partes del tráfico o tareas.

Por ejemplo, si la aplicación almacena el estado de la sesión de un usuario en la memoria de un proceso y el próximo request del usuario es manejado por otro proceso, este segundo proceso no sabría nada de la sesión del usuario.
Solución: Servicios de respaldo con estado

La solución en las aplicaciones de Doce Factores es que cualquier dato que necesite persistencia (como la sesión de un usuario o los resultados de una operación) debe guardarse en servicios de respaldo con estado, como bases de datos, sistemas de caché, o servicios de almacenamiento en la nube.

#### Caché de una sola transacción

Si tu aplicación necesita realizar una operación que involucra datos temporales, puedes utilizar la memoria o el sistema de archivos local como una especie de caché temporal, pero solo para el tiempo de vida del proceso.

Por ejemplo:

    Descargas un archivo grande, lo procesas y luego guardas el resultado en una base de datos. En este caso, puedes descargar el archivo a una ubicación temporal en el sistema de archivos local del proceso, procesarlo y luego eliminarlo una vez que hayas guardado el resultado en un servicio de respaldo (como una base de datos).

#### Conclusión

En una aplicación de Doce Factores, los procesos deben ser sin estado y no compartir memoria o sistema de archivos local entre ellos. Cualquier información que necesite persistencia o ser compartida entre diferentes procesos debe almacenarse en servicios de respaldo externos, como bases de datos o cachés. Esto asegura que la aplicación sea escalable, confiable y capaz de manejar reinicios o cambios en el entorno de ejecución sin pérdida de datos.

## VII. Enlace de puerto
### Servicios de exportación vía enlace portuario 

En el contexto de las aplicaciones de Doce Factores, uno de los principios clave es que la aplicación debe ser autónoma y no depender de un servidor web externo para funcionar. En lugar de ejecutarse dentro de un contenedor de servidor web como Apache (para aplicaciones PHP) o Tomcat (para aplicaciones Java), la aplicación debe exportar HTTP directamente, vinculándose a un puerto y escuchando las solicitudes entrantes. Vamos a desglosarlo paso a paso con ejemplos para hacerlo más claro.

#### Aplicación web tradicional dentro de un servidor web

En muchos entornos tradicionales, las aplicaciones web dependen de servidores como Apache o Tomcat para funcionar. Por ejemplo:

    En una aplicación PHP, el código PHP se ejecuta como parte de Apache. Cuando alguien accede a la página web, Apache recibe la solicitud HTTP y ejecuta el código PHP correspondiente. Apache se encarga de manejar todo el proceso de recibir solicitudes y devolver respuestas.

    De manera similar, en una aplicación Java, esta se ejecuta dentro de Tomcat. Tomcat recibe las solicitudes HTTP, ejecuta el código Java, y devuelve la respuesta correspondiente.

#### En una aplicación de Doce Factores, la aplicación es autónoma

En una aplicación de Doce Factores, no se depende de un servidor web como Apache o Tomcat. En lugar de eso, la aplicación misma actúa como un servidor web, vincula su funcionamiento a un puerto específico, y escucha directamente las solicitudes que llegan a ese puerto.
Ejemplo con Flask (Python):

Flask es un microframework de Python que sigue este principio. Cuando ejecutas una aplicación Flask, la propia aplicación se convierte en un servidor web que escucha en un puerto.


    from flask import Flask
    
    app = Flask(__name__)
    
    @app.route('/')
    def hello():
        return 'Hello, World!'
    
    if __name__ == '__main__':
        # La aplicación vincula el puerto 5000 y escucha solicitudes HTTP
        app.run(port=5000)

Cuando ejecutas este código, Flask inicia un servidor que escucha en el puerto 5000. Puedes acceder a la aplicación visitando http://localhost:5000/ en tu navegador. No necesitas Apache, Tomcat, ni ningún otro servidor web externo para manejar las solicitudes.


#### Cómo funciona en producción

En producción, la misma lógica se aplica, pero a menudo se añade una capa de enrutamiento para manejar las solicitudes entrantes de manera eficiente y distribuirlas a los procesos adecuados.
Ejemplo de capa de enrutamiento en producción:

En lugar de acceder a http://localhost:5000/, los usuarios acceden a un nombre de dominio público como https://miaplicacion.com. Aquí es donde entra la capa de enrutamiento, como Nginx o un servicio de balanceo de carga, que se encarga de recibir las solicitudes de los usuarios en el dominio público y redirigirlas al puerto donde la aplicación está vinculada.

    Nginx puede recibir una solicitud en https://miaplicacion.com y reenviar esa solicitud al puerto 5000, donde la aplicación Flask está escuchando.

Este enfoque permite que la aplicación sea completamente autónoma y no dependa de servidores web como Apache o Tomcat para ejecutar su código.

## VIII. Concurrencia
### Ampliación horizontal a través del modelo de proceso 

¿Qué es un proceso?

Imagina que un proceso es como un "trabajador" que realiza una tarea específica dentro de una aplicación. Cuando ejecutas cualquier programa, ya sea un juego, una aplicación web o una calculadora, ese programa se convierte en uno o más procesos que funcionan en segundo plano dentro del sistema operativo.
Diferencias en cómo se manejan los procesos en diferentes tipos de aplicaciones

#### Aplicaciones PHP:
        PHP es un lenguaje que se usa mucho para crear sitios web. Cuando visitas una página web, PHP crea un proceso que responde a tu solicitud. Pero, solo crea este proceso cuando es necesario (cuando alguien visita la web). Estos procesos de PHP son como trabajadores que se contratan solo cuando hay trabajo que hacer y se despiden después de terminar el trabajo.

#### Aplicaciones Java:
        Java, por otro lado, es más como tener un súper trabajador que ya está en su puesto de trabajo todo el tiempo, esperando recibir múltiples tareas. Este súper trabajador (llamado JVM) ocupa un espacio grande y maneja varias tareas a la vez desde el inicio. Es como tener un empleado fijo que está listo para cualquier tarea en lugar de contratar uno por cada trabajo nuevo.

### ¿Qué es el "modelo de doce factores"?

Es una metodología para desarrollar aplicaciones que funcionen bien en la nube, es decir, en servidores que están conectados a internet. Uno de los principios clave de este modelo es cómo manejar los procesos.

Cómo se usan los procesos en el modelo de doce factores

Cada tarea tiene su propio proceso:
      
    Imagina que tienes una aplicación web. Esta aplicación puede recibir solicitudes de usuarios (como mostrar una página web) y hacer tareas en segundo plano (como enviar correos electrónicos o procesar pagos). En el modelo de doce factores, cada tipo de trabajo tiene su propio proceso.
        Por ejemplo, las solicitudes de la web son manejadas por un "proceso web", mientras que las tareas de fondo, como enviar correos, las maneja un "proceso de trabajo". Cada proceso hace un trabajo específico, como si fueran diferentes departamentos en una empresa.

    Escalabilidad:
        Cuando una aplicación necesita manejar más trabajo, el modelo de procesos facilita la expansión. Imagina que de repente hay muchos usuarios accediendo a tu web o necesitas enviar muchos correos electrónicos. En lugar de hacer que un solo proceso maneje todo (como en el ejemplo de Java), puedes agregar más procesos de cada tipo. Es como contratar más trabajadores especializados para que la carga de trabajo se reparta entre ellos.
        Por ejemplo, si tu aplicación está recibiendo muchas visitas, simplemente agregas más "procesos web" para que manejen más usuarios a la vez. Esto se llama "escalado horizontal", ya que estás agregando más procesos (en lugar de hacer uno más grande).

    Gestión de procesos por el sistema operativo:
        Los procesos en las aplicaciones de doce factores no deben intentar gestionarse a sí mismos. En cambio, deben confiar en herramientas especializadas del sistema operativo o servicios en la nube para manejar la creación, reinicio y finalización de los procesos.
        Por ejemplo, herramientas como systemd en Linux o servicios en la nube como AWS se encargan de vigilar los procesos y reiniciarlos si fallan.

## IX. Disponibilidad
### Maximice la solidez con un inicio rápido y un apagado elegante 


Para maximizar la solidez en una aplicación de doce factores, hay dos conceptos clave que permiten que los procesos sean más ágiles y robustos: inicio rápido y apagado elegante. Aquí te explico ambos de manera concisa y con ejemplos:
Inicio rápido

Los procesos deben estar listos para recibir solicitudes en segundos desde que se ejecuta el comando de inicio. Esto permite que la aplicación:

    Escale rápidamente agregando más procesos según el tráfico.
    Implemente cambios de código rápidamente, minimizando el tiempo de inactividad.

Ejemplo: Imagina que tienes una aplicación financiera que responde a solicitudes de datos. Si el número de usuarios crece de repente, puedes iniciar rápidamente más procesos para manejar el tráfico. Si cada proceso tarda solo unos segundos en activarse, los usuarios no notarán el aumento en la carga.
Apagado elegante

Cuando un proceso debe cerrarse, lo hace de manera ordenada:

    Deja de aceptar nuevas solicitudes.
    Finaliza las solicitudes que ya están en proceso.
    Luego se apaga completamente.

Ejemplo en un servidor web: Si decides detener tu servidor de Node.js, primero dejaría de aceptar nuevas conexiones, terminaría de procesar las solicitudes actuales y luego se cerraría sin interrumpir a los usuarios.

Para procesos de trabajo (background workers), si un proceso se apaga mientras está procesando un trabajo, devuelve ese trabajo a la cola para que otro proceso lo pueda continuar.
Robusto contra fallos

En caso de una falla inesperada (muerte súbita del servidor), los procesos deben estar diseñados para manejarlo sin perder información. Esto se logra usando colas de trabajo que devuelven tareas incompletas automáticamente.

Ejemplo: Si tu aplicación usa una cola de trabajos para procesar informes financieros y un servidor falla repentinamente, la cola puede reasignar los trabajos a otro proceso activo, asegurando que ningún trabajo se pierda.
Resumen

    Inicio rápido: Los procesos deben iniciarse en segundos para mayor agilidad.
    Apagado elegante: Cierran ordenadamente, terminando trabajos en curso sin interrupciones.
    Robustez ante fallos: Diseñados para manejar cierres inesperados, devolviendo trabajos a la cola.


## X. Paridad desarrollo/producción
### Mantenga el desarrollo, la puesta en escena y la producción lo más similares posible 

La paridad entre desarrollo y producción es un principio clave en la metodología de las aplicaciones de "doce factores". Básicamente, significa que el entorno en el que desarrollas tu aplicación debe ser lo más similar posible al entorno en el que se ejecutará en producción. Esto evita que surjan problemas inesperados cuando llevas tu aplicación de un entorno a otro (por ejemplo, de tu computadora al servidor).

Aquí te explico de manera clara y con ejemplos cómo se manifiesta este principio, por qué es importante y cómo implementarlo:
1. Reducir la brecha de tiempo

    Problema: En aplicaciones tradicionales, puede pasar mucho tiempo entre que un desarrollador escribe el código y este se implementa en producción (días o semanas).
    Solución (12 factores): En una aplicación de doce factores, el código se implementa rápidamente, a veces minutos después de ser escrito. Esto se logra con procesos automatizados de integración y entrega continua (CI/CD).

Ejemplo:

    En una aplicación tradicional, podrías tener que esperar semanas para que los cambios que hiciste en el código lleguen a producción.
    Con CI/CD (como GitHub Actions o Jenkins), cuando un desarrollador hace un cambio en el código, este pasa por pruebas automáticas y, si todo está bien, se despliega en producción en cuestión de minutos.

2. Reducir la brecha de personal

    Problema: En aplicaciones tradicionales, los desarrolladores escriben el código, pero son los equipos de operaciones los que lo implementan, lo que crea una desconexión entre ambos.
    Solución (12 factores): Los desarrolladores no solo escriben el código, sino que también son responsables de la implementación. De esta manera, están directamente involucrados en cómo funciona su código en producción.

Ejemplo:

    Tradicionalmente, si algo sale mal en producción, el equipo de operaciones tiene que arreglarlo, y los desarrolladores pueden no estar involucrados.
    Con las aplicaciones de doce factores, los desarrolladores están involucrados en todo el proceso, desde el desarrollo hasta la puesta en producción, lo que mejora la calidad del código.

3. Reducir la brecha de herramientas

    Problema: A veces los desarrolladores usan diferentes herramientas y tecnologías en sus entornos locales que no coinciden con las de producción. Por ejemplo, pueden usar SQLite en sus máquinas locales y PostgreSQL en producción, lo que puede causar problemas inesperados.
    Solución (12 factores): Tanto el entorno de desarrollo como el de producción deben usar las mismas herramientas y versiones. Si usas PostgreSQL en producción, también deberías usar PostgreSQL en desarrollo.

Ejemplo:

    Supongamos que en tu entorno de desarrollo usas SQLite porque es más fácil de configurar, pero en producción usas PostgreSQL. En SQLite, podrías no tener problemas, pero en PostgreSQL (que es más complejo), pueden aparecer errores inesperados.
    La solución sería usar Docker o herramientas como Vagrant para replicar el entorno de producción en tu máquina local, usando las mismas bases de datos, colas, caché, etc.

4. Uso de servicios de respaldo (bases de datos, colas, caché)

    Problema: Los desarrolladores a menudo usan versiones más simples o diferentes servicios de respaldo en desarrollo (como usar memoria local para caché) y versiones más complejas en producción (como Memcached). Esto puede generar errores difíciles de rastrear.
    Solución (12 factores): Todos los entornos (desarrollo, puesta en escena, producción) deben usar los mismos servicios de respaldo. Si usas Redis en producción, usa Redis también en desarrollo.

Ejemplo:

    En desarrollo, puedes estar usando caché en memoria local y en producción estás usando Redis. Lo que puede funcionar en tu entorno local podría no funcionar igual en producción.
    Para evitar estos problemas, puedes usar Redis en ambos entornos. Si es difícil instalar Redis localmente, podrías usar herramientas como Docker para hacerlo más sencillo.

Herramientas para asegurar la paridad entre desarrollo y producción

    Docker: Con Docker, puedes crear contenedores que replican exactamente el entorno de producción en tu entorno local. Esto incluye las versiones exactas de bases de datos, sistemas de colas, etc.
    Vagrant: Crea entornos de desarrollo que imitan tu entorno de producción utilizando máquinas virtuales.
    Homebrew/apt-get: Estas herramientas facilitan la instalación de servicios como PostgreSQL, Redis, o RabbitMQ en tu máquina local.

