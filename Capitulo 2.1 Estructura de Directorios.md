  ## 2.1 Estrucutura de Directorios - ¿Cuál es la estructura de directorios en Laravel y para qué se utiliza cada uno?

En Laravel, la estructura de directorios está organizada de manera que separa diferentes componentes de la aplicación y proporciona un enfoque claro para la organización del código. A continuación, se describe la estructura de directorios más comúnmente utilizada en una aplicación Laravel:

1. Carpeta `app`:
   - La carpeta `app` es el corazón de tu aplicación Laravel. Aquí es donde encontrarás los modelos, controladores, políticas y otros componentes clave de tu aplicación.
   - La carpeta `app/Console` contiene comandos de consola personalizados que puedes crear para realizar tareas específicas en tu aplicación.
   - La carpeta `app/Http` contiene los controladores HTTP de tu aplicación, que manejan las solicitudes y las respuestas HTTP.
   - La carpeta `app/Models` es donde puedes definir los modelos de Eloquent, que representan las tablas de la base de datos y se utilizan para interactuar con los datos.
   - La carpeta `app/Policies` contiene las políticas de autorización, que determinan qué acciones están permitidas para los modelos.
   - Otros directorios como `app/Providers`, `app/Listeners`, `app/Events` y `app/Exceptions` contienen clases que se utilizan para la gestión de servicios, eventos, excepciones y otros aspectos de la aplicación.

2. Carpeta `bootstrap`:
   - La carpeta `bootstrap` contiene archivos importantes para el proceso de inicio de Laravel, como la carga automática de clases y la configuración del entorno.

3. Carpeta `config`:
   - La carpeta `config` contiene archivos de configuración para tu aplicación Laravel. Aquí puedes ajustar la configuración de la base de datos, el correo electrónico, los servicios y otros aspectos de la aplicación.

4. Carpeta `database`:
   - La carpeta `database` contiene archivos de migración y semillas de datos para gestionar la estructura y los datos de la base de datos.
   - El directorio `database/factories` contiene archivos de fábrica que definen la estructura de los datos ficticios para tus pruebas y desarrollo.
   - El directorio `database/seeds` contiene archivos de semillas que puedes utilizar para poblar tu base de datos con datos iniciales.

5. Carpeta `public`:
   - La carpeta `public` es el punto de entrada de tu aplicación. Aquí se encuentra el archivo `index.php` que inicia el framework y maneja las solicitudes HTTP.
   - Los archivos estáticos, como imágenes, hojas de estilo y JavaScript, se almacenan en el directorio `public`.

6. Carpeta `resources`:
   - La carpeta `resources` contiene los archivos de vistas, assets y traducciones de tu aplicación.
   - La carpeta `resources/views` contiene los archivos de vistas de Blade, donde se define la estructura y el contenido de las páginas.
   - La carpeta `resources/assets` es donde puedes almacenar tus archivos de JavaScript, CSS y otros assets.
   - La carpeta `resources/lang` contiene los archivos de traducción para diferentes idiomas.

7. Carpeta `routes`:
   - La carpeta `routes` contiene los archivos de enrutamiento de tu aplicación.
   - El archivo `routes/web.php` define las rutas que gestionan las solicitudes web y las respuestas correspondientes.
   - El archivo `routes/api.php` define las rutas para las API de tu aplicación.

8. Carpeta `storage`:


   - La carpeta `storage` es donde Laravel almacena archivos generados dinámicamente, como archivos de logs, caché, sesiones y otros archivos temporales.
   - La carpeta `storage/app` es utilizada para almacenar archivos generados por la aplicación.
   - La carpeta `storage/framework` contiene archivos de caché y sesiones.
   - La carpeta `storage/logs` almacena los archivos de registro de la aplicación.

9. Carpeta `tests`:
   - La carpeta `tests` contiene los archivos de prueba para tu aplicación Laravel. Aquí puedes escribir pruebas unitarias y de integración para verificar el correcto funcionamiento de tus componentes.

Esta estructura de directorios proporciona una organización clara y modular para tu aplicación Laravel, lo que facilita el mantenimiento, la escalabilidad y la colaboración en el desarrollo del proyecto.

### Algo más??

Aquí tienes algunos elementos adicionales en la estructura de directorios de Laravel:

10. Carpeta `vendor`:
   - La carpeta `vendor` es generada por Composer y contiene las dependencias de terceros instaladas en tu aplicación. Aquí se encuentran los paquetes y las bibliotecas necesarias para el funcionamiento de Laravel y otras bibliotecas adicionales que hayas instalado.

11. Archivo `.env`:
   - El archivo `.env` es un archivo de configuración donde se definen las variables de entorno específicas de tu aplicación, como la configuración de la base de datos, credenciales de servicios externos, etc. Este archivo es crucial para configurar tu entorno de desarrollo y producción y se encuentra en la raíz del proyecto.

12. Archivo `artisan`:
   - El archivo `artisan` es la interfaz de línea de comandos de Laravel. Proporciona una amplia gama de comandos útiles para tareas de desarrollo, como la generación de código, la ejecución de migraciones, el inicio de un servidor de desarrollo, la ejecución de pruebas y mucho más.

Estos son algunos elementos clave de la estructura de directorios de Laravel. Cada uno de ellos desempeña un papel importante en la organización y funcionalidad de tu aplicación. Al comprender la función de cada carpeta y archivo, podrás navegar y trabajar eficientemente en tu proyecto Laravel. 