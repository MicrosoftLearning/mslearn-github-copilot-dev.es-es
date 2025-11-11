<!-- ---
lab:
    title: 'Exercise - Resolve GitHub issues using GitHub Copilot'
    description: 'Learn how to identify and address performance bottlenecks and code inefficiencies using GitHub Copilot tools.'
--- -->

# Resolución de incidencias de GitHub con GitHub Copilot

Las incidencias de GitHub son una manera eficaz de realizar el seguimiento de los errores, mejoras y tareas de un proyecto.

En este ejercicio, usará GitHub Copilot para ayudarle a analizar y resolver incidencias de GitHub relacionadas con vulnerabilidades de seguridad en una aplicación de comercio electrónico.

Este ejercicio debería tardar en completarse **40** minutos aproximadamente.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar su propia cuenta de GitHub y suscripción de GitHub Copilot. Si no tiene una cuenta de GitHub, puede <a href="https://github.com/" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

## Antes de comenzar

El entorno de laboratorio debe incluir lo siguiente: Git 2.48 o posterior, SDK de .NET 9.0 o posterior, Visual Studio Code con la extensión Kit de desarrollo de C# y acceso a una cuenta de GitHub con GitHub Copilot habilitado.

Si usa un equipo local como entorno de laboratorio para este ejercicio:

- Para obtener ayuda a fin de configurar el equipo local como entorno de laboratorio, abra el siguiente vínculo en un explorador: <a href="https://go.microsoft.com/fwlink/?linkid=2320147" target="_blank">Configure los recursos de entorno de laboratorio</a>.

- Para obtener ayuda sobre cómo habilitar la suscripción de GitHub Copilot en Visual Studio Code, abra el siguiente vínculo en un explorador: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

Si usa un entorno de laboratorio hospedado para este ejercicio:

- Para obtener ayuda a fin de habilitar la suscripción de GitHub Copilot en Visual Studio Code, pegue la siguiente dirección URL en la barra de navegación del sitio de un explorador: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

- Para asegurarse de que el SDK de .NET está configurado para usar el repositorio oficial de NuGet.org como origen para descargar y restaurar paquetes:

    Abra un terminal de comandos y luego ejecute los siguientes comandos:

    ```bash

    dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org

    ```

- Para asegurarse de que Git está configurado para usar su nombre y dirección de correo electrónico:

    Actualice los siguientes comandos con la información y, a continuación, ejecute los comandos:

    ```bash

    git config --global user.name "Julie Miller"

    ```

    ```bash

    git config --global user.email julie.miller@example.com

    ```

## Escenario del ejercicio

Es desarrollador de software y trabaja para una empresa de consultoría. Los clientes necesitan ayuda para resolver incidencias en sus repositorios de GitHub. Debe asegurarse de que todas las incidencias se solucionan y cierran. Puede usar Visual Studio Code como entorno de desarrollo y GitHub Copilot para ayudar con las tareas de desarrollo. Se le asigna a la aplicación siguiente:

- ContosoShopEasy: ContosoShopEasy es una aplicación de comercio electrónico que contiene varias vulnerabilidades de seguridad. Las vulnerabilidades representan incidencias comunes de seguridad encontradas en aplicaciones reales.

Este ejercicio incluye las siguientes tareas:

1. Importe el repositorio ContosoShopEasy.
1. Revise las incidencias en GitHub.
1. Clone el repositorio localmente y revise el código base.
1. Analice las incidencias con el modo Preguntar de GitHub Copilot.
1. Resuelva las incidencias con el modo Agente de GitHub Copilot.
1. Pruebe y compruebe el código refactorizado.
1. Confirme los cambios y cierre las incidencias.

### Importación del repositorio ContosoShopEasy

GitHub Importer le permite crear una copia de un repositorio existente en su propia cuenta de GitHub, lo que le proporciona control total sobre la copia importada. Aunque GitHub Importer no migra incidencias, solicitudes de incorporación de cambios o discusiones, importa flujos de trabajo de Acciones de GitHub. El repositorio que importe incluye un flujo de trabajo de Acciones de GitHub que crea incidencias asociadas con el código base.

En esta tarea, importará el repositorio ContosoShopEasy y ejecutará un flujo de trabajo para crear incidencias de GitHub para las vulnerabilidades de seguridad incluidas en el código base.

Realice los pasos siguientes para completar esta tarea:

1. Abra una ventana del explorador y vaya a GitHub.com.

1. Inicie sesión en su cuenta de GitHub y abra la pestaña de repositorios.

    Para abrir la pestaña de repositorios, haga clic en el icono de perfil de la esquina superior derecha y seleccione **Repositorios**.

1. En la pestaña Repositorios, seleccione el botón **Nuevo**.

1. En la sección **Crear un nuevo repositorio**, seleccione **Importar un repositorio**.

    Aparece la página **Importar el proyecto a GitHub**.

1. En este página, en **Detalles del repositorio de origen**, escriba la siguiente dirección URL para el repositorio de origen:

    ```plaintext
    https://github.com/MicrosoftLearning/resolve-github-issues-lab-project
    ```

1. En la sección **Detalles del nuevo repositorio**, en la lista desplegable **Propietario**, seleccione el nombre de usuario de GitHub.

1. En el campo **Nombre del repositorio**, escriba **ResolveGitHubIssues** y seleccione **Comenzar importación**.

    GitHub crea el nuevo repositorio en su cuenta con los archivos de proyecto de ContosoShopEasy.

1. Espere a que se complete el proceso de importación y abra el nuevo repositorio.

    > **NOTA**: El repositorio puede tardar un minuto o dos en importarse.

1. Abra la pestaña Acciones del repositorio.

1. En el lado izquierdo de la página en **Todos los flujos de trabajo**, seleccione el flujo de trabajo **Create ContosoShopEasy Training Issues** y, a continuación, seleccione **Ejecutar flujo de trabajo**.

1. En el cuadro de diálogo de flujo de trabajo que aparece, escriba **CREATE** y, a continuación, seleccione **Ejecutar flujo de trabajo**.

1. Supervise el progreso en pantalla del flujo de trabajo.

    Después de un momento, la página se actualizará y mostrará una barra de progreso. El flujo de trabajo debe completarse correctamente en menos de un minuto.

1. Asegúrese de que el flujo de trabajo se completa correctamente antes de continuar.

    Una marca de verificación dentro de un círculo verde indica que el flujo de trabajo se ejecutó correctamente (debería aparecer a la izquierda del nombre del flujo de trabajo).

    Si aparece una X dentro de un círculo rojo a la izquierda del nombre del flujo de trabajo, significa que se produjo un error en el flujo de trabajo. Si el flujo de trabajo no se ejecuta correctamente, asegúrese de que seleccionó la cuenta al importar el repositorio y de que la cuenta tiene permisos de lectura y escritura. Puede usar la característica **Chat with Copilot** de GitHub para ayudar a diagnosticar el problema.

### Revisión de las incidencias en GitHub

Las incidencias de GitHub sirven como un sistema de seguimiento centralizado para errores, vulnerabilidades de seguridad y solicitudes de mejora. Cada incidencia proporciona contexto sobre el problema, su gravedad y el posible impacto en la aplicación. Comprender estas incidencias antes de profundizar en el código ayuda a establecer prioridades y garantiza una corrección completa.

En esta tarea, revisará las incidencias de GitHub y examinará las vulnerabilidades de seguridad que deben solucionarse.

Realice los pasos siguientes para completar esta tarea:

1. Seleccione la pestaña **Incidencias** del repositorio y, a continuación, dedique un minuto a revisar la página de incidencias.

    Debería ver 10 incidencias abiertas. Tenga en cuenta lo siguiente:

    - Todas las incidencias están etiquetadas como errores.
    - Todas las incidencias tienen un nivel de prioridad.
    - Todas las incidencias están asignadas a alguien.

1. Para mostrar solo las incidencias críticas, seleccione la lista desplegable **Etiquetas** y, a continuación, seleccione la etiqueta **crítica**.

    La lista de incidencias debe actualizarse para mostrar solo las incidencias críticas.

    - **🔐 Eliminar las credenciales de administrador codificadas de forma rígida**  

    - **🔐 Corregir las infracciones de almacenamiento de datos de tarjetas de crédito**  

1. Para mostrar solo las incidencias de alta prioridad, seleccione la lista desplegable **Etiquetas**, anule la selección de **crítico** y, a continuación, seleccione la etiqueta **alta prioridad**.

    La lista de incidencias debe actualizarse para mostrar solo las incidencias de alta prioridad.

    - **🔐 Corregir la omisión de seguridad de validación de entrada**  

    - **🔐 Eliminar los datos confidenciales del registro de depuración**  

    - **🔐 Reemplazar el hash de contraseña MD5 por alternativa segura**  

    - **🔐 Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos**  

1. Seleccione la incidencia **Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos**.

1. Dedique un minuto a revisar los detalles de la incidencia.

    Los detalles de la incidencia deben describir el problema y la corrección esperada.

    > **NOTA**: El proceso que se usa para documentar las incidencias, incluidos los procesos manuales frente a los automatizados con IA, puede afectar a la calidad general y la precisión de las descripciones de estas. Las incidencias incluidas en este entrenamiento se escribieron mediante el modo agente de GitHub Copilot después de que el agente revisara el código base. GitHub Copilot se puede usar para generar descripciones muy detalladas de las vulnerabilidades, ubicaciones de código, ejemplos del código vulnerable, riesgos de seguridad y criterios de aceptación para las correcciones.

1. Observe que no se ha asignado a nadie a la incidencia.

1. Vuelva a la pestaña Incidencias y borre los filtros.

1. Seleccione las siguientes incidencias críticas y de alta prioridad y, a continuación, use la lista desplegable **Asignar** para asignárselas a usted mismo.

    - **🔐 Corregir las infracciones de almacenamiento de datos de tarjetas de crédito**  

    - **🔐 Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos**  

    Por lo general, es mejor trabajar primero en las incidencias de prioridad más alta. Asignarse las incidencias a usted mismo le ayuda a realizar un seguimiento del progreso a medida que trabaja en el proceso de corrección.

### Clonación local del repositorio y revisión del código base

La aplicación ContosoShopEasy sigue una arquitectura en capas típica de las aplicaciones empresariales, con una separación clara entre modelos, servicios, acceso a datos y componentes de seguridad.

Un primer más importante al resolver las incidencias de seguridad es tomarse el tiempo para comprender la estructura básica, el comportamiento y las características de un código base.

En esta tarea, creará un clon local del repositorio, examinará la estructura del proyecto en Visual Studio Code, revisará la salida de la consola de la aplicación e identificará las vulnerabilidades de seguridad dentro del código base.

Realice los pasos siguientes para completar esta tarea:

1. Vuelva a la página raíz del repositorio (pestaña Código).

1. Clone el repositorio ResolveGitHubIssues en el entorno de desarrollo local.

    Por ejemplo, puede usar los pasos siguientes para clonar el repositorio mediante la CLI de Git:

    1. Copie la dirección URL del repositorio seleccionando el botón **Código** y, a continuación, copie la dirección URL HTTPS.

    1. Abra una ventana de terminal, vaya al directorio donde desea clonar el repositorio y, a continuación, ejecute un comando "git clone" que use la dirección URL del repositorio.

        Por ejemplo, abra Windows PowerShell, vaya a C:\TrainingProjects y ejecute el siguiente comando (reemplazando **your-username** por el nombre de usuario de GitHub):

        ```bash
        git clone https://github.com/your-username/ResolveGitHubIssues.git
        ```

1. Abra el repositorio clonado en Visual Studio Code.

    Asegúrese de que usa la versión más reciente de Visual Studio Code y de que tiene instaladas y habilitadas las extensiones de GitHub Copilot y GitHub Copilot Chat.

1. Examine la estructura del proyecto en la vista EXPLORER.

    La aplicación ContosoShopEasy sigue una arquitectura en capas con los siguientes componentes:

    - **Data/**: Contiene repositorios de datos en **OrderRepository.cs**, **ProductRepository.cs** y **UserRepository.cs**.

    - **Models/**: Contiene modelos de datos para **Category.cs**, **Order.cs**, **Product.cs** y **User.cs**.

    - **Security/**: Contiene lógica de validación de seguridad en **SecurityValidator.cs**

    - **Services/**: Contiene lógica de negocios en **OrderService.cs**, **PaymentService.cs**, **ProductService.cs** y **UserService.cs**.

    - **Program.cs**: Punto de entrada principal de la aplicación con configuración de inserción de dependencias

    - **README.md**: Documentación que explica el propósito y las vulnerabilidades de la aplicación

1. Para observar el comportamiento actual de la aplicación, compile y ejecute la aplicación.

    Por ejemplo, puede abrir la ventana de terminal integrado de Visual Studio Code y ejecutar los siguientes comandos:

    ```bash
    cd ContosoShopEasy
    dotnet build
    dotnet run
    ```

    La aplicación ejecuta una simulación del flujo de trabajo de comercio electrónico que expone vulnerabilidades de seguridad a través del registro detallado de la consola.

1. Tómese un minuto para revisar la salida de la consola.

    La aplicación ContosoShopEasy usa intencionadamente el registro excesivo como herramienta educativa. Además de exponer las incidencias de seguridad en el código base, algunos de los registros generan realmente las incidencias. La inclusión de registros que crean incidencias de seguridad muestra los problemas reales de exceso de registro encontrados en algunos sistemas de producción. El registro en la aplicación ContosoShopEasy se usa para ayudar a los desarrolladores a distinguir entre dos tipos de incidencias:

    - Incidencias creadas por el registro: aproximadamente el 40 % de las vulnerabilidades de la aplicación ContosoShopEasy se deben a un exceso de registro. Por ejemplo, la exposición de contraseñas, la divulgación de números de tarjetas de crédito, la exposición de tokens de sesión y la divulgación de información de configuración.

    - Incidencias que existen independientemente del registro: aproximadamente el 60 % de las vulnerabilidades de la aplicación ContosoShopEasy existen independientemente del registro. Por ejemplo, la inyección de código SQL, el hash de contraseña no segura, las credenciales codificadas de forma rígida, los tokens predecibles, la omisión de validación de entrada, el almacenamiento de tarjetas de crédito y la validación de correo electrónico poco seguro. Aunque el registro no crea estas vulnerabilidades, ayuda a exponer las incidencias en el entorno de entrenamiento.

1. Para comenzar la revisión de las vulnerabilidades de seguridad en el código base, expanda la carpeta **Models** y, a continuación, abra el archivo **Order.cs**.

1. Desplácese hacia abajo hasta encontrar la clase **PaymentInfo**.

    Observe los comentarios relativos a las propiedades CardNumber y CVV. Este código está relacionado con la incidencia **Corregir infracciones de almacenamiento de datos de tarjetas de crédito** que se ha asignado a usted mismo.

1. Expanda la carpeta **Security** y abra el archivo **SecurityValidator.cs**.

    Observe que la aplicación ContosoShopEasy usa los comentarios de código, la lógica y el registro para exponer incidencias de seguridad. Aunque la implementación es inventada, este enfoque ayuda a resaltar las vulnerabilidades que son comunes en las aplicaciones reales.

    > **NOTA**: La clase SecurityValidator.cs está diseñada para centralizar la lógica relacionada con la seguridad para la aplicación ContosoShopEasy, lo que facilita la búsqueda, la administración y la resolución de incidencias de seguridad. En una aplicación real, se podría usar una clase como SecurityValidator para aplicar procedimientos recomendados de seguridad y validación de entrada. Sin embargo, la implementación específica en ContosoShopEasy es intencionadamente poco segura y se ha inventado para exponer las vulnerabilidades.

1. Tómese un minuto para encontrar las siguientes incidencias de seguridad:

    - Cerca de la parte superior del archivo, observe el comentario relacionado con las constantes de credenciales de administrador (líneas 7-9). Este código está relacionado con la incidencia "Eliminar las credenciales de administrador codificadas de forma rígida".

    - Busque el método ValidateInput y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Corregir la omisión de seguridad de validación de entrada".

    - Busque el método ValidateEmail y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Mejorar la seguridad de validación del correo electrónico".

    - Busque el método ValidatePasswordStrength y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Reforzar los requisitos de seguridad de contraseñas".

    - Busque el método ValidateCreditCard y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia **Corregir infracciones de almacenamiento de datos de tarjetas de crédito** que se ha asignado a usted mismo.

    - Busque el método GenerateSessionToken y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Corregir la generación de tokens de sesión predecibles".

    - Busque el método RunSecurityAudit y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Reducir la divulgación de información en los mensajes de error (salida de la consola)".

    Varios de los métodos del archivo SecurityValidator.cs también están relacionados con la incidencia "Eliminar los datos confidenciales del registro de depuración".

    Las incidencias expuestas por la clase SecurityValidator se encuentran normalmente distribuidas entre las clases de aplicaciones reales, especialmente los códigos base heredados o mal mantenidos.

1. Expanda la carpeta **Services** y abra el archivo **UserService.cs**.

1. Tómese un minuto para encontrar las siguientes incidencias de seguridad:

    - Busque los métodos RegisterUser, LoginUser y ValidateUserInput y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Eliminar los datos confidenciales del registro de depuración".

    - Busque el método GetMd5Hash y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Reemplazar el hash de contraseña MD5 por alternativa segura".

1. Abra el archivo **PaymentService.cs**.

1. Dedique un minuto a revisar los comentarios de los métodos de pago y validación.

    Las vulnerabilidades de seguridad de este código están relacionadas con la incidencia **Corregir infracciones de almacenamiento de datos de tarjetas de crédito** que se asignó a usted mismo.

    La clase PaymentService también está relacionada con otras incidencias. Por ejemplo, las incidencias "Eliminar los datos confidenciales del registro de depuración" y "Reducir la divulgación de información en los mensajes de error (salida de la consola )".

    Observe que la clase PaymentService usa OrderRepository para conservar los datos de pedido relacionados con el pago. Si la clase OrderRepository no gestiona correctamente los datos confidenciales, podría provocar vulnerabilidades de exposición de datos en la clase OrderRepository.

1. Abra el archivo **ProductService.cs**.

1. Dedique un minuto a revisar el método SearchProducts.

    Las vulnerabilidades de seguridad de este código están relacionadas con la incidencia **Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos** que se asignó a usted mismo.

    Observe que el método SearchProducts de ProductService llama al método SearchProducts en ProductRepository. Es posible que quiera analizar el método del repositorio para determinar si también requiere mejoras de seguridad.

1. Haga una lista de los archivos de código relacionados con las incidencias asignadas.

    Las incidencias que se ha asignadas a usted mismo son:

    - **🔐 Corregir las infracciones de almacenamiento de datos de tarjetas de crédito**
    - **🔐 Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos**

    Los archivos de código relacionados con la incidencia "Corregir las infracciones de almacenamiento de datos de tarjetas de crédito" son:

    - Clase Models/Orders.cs/PaymentInfo
    - Método Security/SecurityValidator.cs/ValidateCreditCard
    - Data/OrderRepository.cs

    Los archivos de código relacionados con la incidencia "Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos" son:

    - Método Services/ProductService.cs/SearchProducts
    - Método Data/ProductRepository.cs/SearchProducts

### Análisis de las incidencias con el modo Preguntar de GitHub Copilot

Las incidencias de GitHub suelen contener problemas complejos que requieren un análisis cuidadoso antes de implementar las correcciones. Comprender las causas principales, los posibles impactos y las mejores estrategias de corrección es fundamental para una resolución eficaz.

Las siguientes extensiones de GitHub para Visual Studio Code pueden ayudarle a analizar las incidencias de GitHub:

- **GitHub Copilot Chat**: El modo Preguntar de GitHub Copilot proporciona funcionalidades de análisis de código inteligentes que pueden ayudar a identificar vulnerabilidades de seguridad, comprender su posible impacto y sugerir estrategias de corrección.

- **Solicitudes de incorporación de cambios de GitHub**: la extensión Solicitudes de incorporación de cambios de GitHub integra las incidencias de GitHub directamente en Visual Studio Code, lo que le permite administrarlas e interactuar con ellas sin salir del entorno de desarrollo.

Con el análisis sistemático de las incidencias de seguridad, puede desarrollar una comprensión completa de los problemas antes de implementar correcciones. Este enfoque garantiza que las soluciones aborden las causas principales en lugar de solo los síntomas.

En esta tarea, usará el modo Preguntar de GitHub Copilot para analizar las incidencias de GitHub asignadas a usted.

Realice los pasos siguientes para completar esta tarea:

1. Asegúrese de que las extensiones GitHub Copilot Chat y Solicitudes de incorporación de cambios de GitHub están instaladas en Visual Studio Code.

    Abra la vista Extensiones en Visual Studio Code y revise las extensiones instaladas. Si falta alguna extensión, instálela antes de continuar.

    Por ejemplo, puede usar los pasos siguientes para instalar la extensión Solicitudes de incorporación de cambios de GitHub:

    1. Abra la vista Extensiones en Visual Studio Code.

    1. En la vista Extensiones, busque **Solicitudes de incorporación de cambios de GitHub**.

    1. Seleccione **Solicitudes de incorporación de cambios de GitHub** en los resultados de búsqueda y, a continuación, instale la extensión.

        Una vez finalizada la instalación, es posible que tenga que volver a cargar Visual Studio Code para que los cambios surtan efecto. Se debe agregar un icono de **GitHub** a la barra de actividad de Visual Studio Code.

1. Para abrir la vista de solicitudes de incorporación de cambios de GitHub, seleccione el icono de **GitHub** en la barra de actividades.

    Si se le solicita, inicie sesión en su cuenta de GitHub para conectar Visual Studio Code a los repositorios de GitHub.

1. Observe que la vista de GitHub incluye dos secciones, **Solicitudes de incorporación de cambios** e **Incidencias**.

    La sección **Incidencias** permite ver y administrar las incidencias desde los repositorios de GitHub directamente en Visual Studio Code. La sección **Solicitudes de incorporación de cambios** permite administrar las solicitudes de incorporación de cambios.

1. Contraiga la sección **Solicitudes de incorporación de cambios**.

1. Tómese un minuto para revisar la sección **Incidencias**.

    Observe que las incidencias que se ha asignado a usted mismo aparecen en la sección "Mis incidencias" (no se han definido hitos). Si expande la sección **Incidencias recientes**, puede ver todas las incidencias que se agregaron al repositorio.

1. En la sección "Mis incidencias", seleccione **Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos**.

    La extensión Solicitudes de incorporación de cambios de GitHub abre los detalles de la incidencia en una nueva pestaña del editor. Puede revisar la descripción de la incidencia, los comentarios y cualquier información relacionada en esta pestaña. Puede usar los detalles de la incidencia para ayudar a construir las indicaciones que envía a GitHub Copilot en la vista Chat.

1. Abra la vista Chat de GitHub Copilot y asegúrese de que está seleccionado el modo **Preguntar**.

    Si la vista Chat aún no está abierta, seleccione el icono **Chat** situado en la parte superior de la ventana de Visual Studio Code. Compruebe que el modo de chat está establecido en **Preguntar** y que usa el modelo **GPT-4.1**.

    > **NOTA**: El modelo GPT-4.1 proporciona excelentes funcionalidades de análisis de código y se incluye con el plan Gratis de GitHub Copilot. Elegir un modelo diferente puede producir resultados diferentes.

1. Asegúrese de que empieza con una sesión de chat limpia.

    Las sesiones de chat ayudan a organizar las interacciones con GitHub Copilot. Cada sesión mantiene su propio contexto, lo que le permite centrarse en tareas o incidencias concretas. El historial de conversaciones dentro de una sesión proporciona continuidad, lo que permite a GitHub Copilot basarse en interacciones anteriores para devolver respuestas más precisas y pertinentes. Esta conversación de chat se centrará en analizar y resolver las dos vulnerabilidades de seguridad que tiene asignadas en la aplicación ContosoShopEasy. Después de completar el análisis de las incidencias de GitHub mediante el modo Preguntar de GitHub Copilot, puede usar la misma conversación para ayudar a implementar los cambios de código mediante el modo Agente de GitHub Copilot. GitHub Copilot puede usar el análisis detallado del modo Preguntar para informar a su generación de código en el modo Agente, lo que garantiza que las correcciones se alinean con las vulnerabilidades identificadas y las estrategias de corrección recomendadas.

    Si es necesario, puede iniciar una nueva sesión de chat seleccionando el botón **Nuevo chat** (el icono **+** de la parte superior del panel Chat).

#### Análisis de la vulnerabilidad de inyección de código SQL

La vulnerabilidad de inyección de código SQL existe en el archivo ProductService.cs y posiblemente en el archivo ProductRepository.cs. Analizará ambos archivos para comprender el alcance completo de la vulnerabilidad.

Siga estos pasos para analizar la vulnerabilidad de inyección de código SQL:

1. Abra el archivo **ProductService.cs** y busque el método **SearchProducts**.

1. En el editor de código, seleccione todo el método **SearchProducts**.

    Al seleccionar código en el editor, el chat se centra en ese contexto. GitHub Copilot usa el código seleccionado para proporcionar análisis y recomendaciones pertinentes.

1. Pida a GitHub Copilot que analice el código de vulnerabilidad de inyección de código SQL.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    Analyze the SearchProducts method for SQL injection vulnerabilities. Consider the following issue description: "The product search functionality is vulnerable to SQL injection attacks. User input is directly concatenated into SQL queries without proper parameterization or sanitization." Explain the impact of directly concatenating user input into SQL queries without proper parameterization or sanitization. What are the potential consequences if an attacker exploits this vulnerability?
    ```

1. Revise el análisis de GitHub Copilot.

    GitHub Copilot debe identificar que el método construye consultas SQL mediante la entrada del usuario sin un saneamiento adecuado. La consulta SQL simulada muestra cómo la entrada del usuario se concatena directamente en la cadena de consulta, lo que podría permitir que los atacantes manipulen la consulta de base de datos.

1. Pida instrucciones de corrección específicas.

    Por ejemplo, después de revisar el análisis inicial, puede enviar la siguiente indicación:

    ```text
    How can I modify this method to prevent SQL injection attacks? What secure coding practices should I implement to safely handle user input in database queries? Where should user input be validated and sanitized? What techniques can I use to construct SQL queries safely?
    ```

1. Dedique un minuto a revisar las sugerencias de corrección de GitHub Copilot.

    Debería ver recomendaciones para usar consultas con parámetros o métodos ORM que ayudan a administrar los riesgos de inyección de código SQL. También puede ver sugerencias para las técnicas de validación y saneamiento de entrada. GitHub Copilot proporciona con frecuencia fragmentos de código que muestran cómo implementar sugerencias.

1. Abra el archivo **ProductRepository.cs** en la carpeta **Datos** y busque el método **SearchProducts**.

    Durante la revisión del código, observó que el método SearchProducts de ProductService llama al método SearchProducts de ProductRepository. Puede analizar el método del repositorio para determinar si también requiere mejoras de seguridad.

1. En el editor de código, seleccione todo el método **SearchProducts** y, a continuación, pida a GitHub Copilot que analice el código para detectar la vulnerabilidad de inyección de código SQL.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    Analyze the SearchProducts method in ProductRepository. Does this method properly handle the search term to prevent SQL injection, or are there vulnerabilities here as well? How does this method relate to the vulnerability in ProductService?
    ```

1. Revise el análisis de GitHub Copilot del método del repositorio.

    GitHub Copilot debe tener en cuenta que, aunque el método del repositorio usa operaciones de cadena seguras (ToLower y Contains), la vulnerabilidad principal se encuentra en la capa ProductService donde la consulta SQL simulada se construye con la entrada del usuario. La propia implementación del repositorio es relativamente segura, pero la capa de servicio expone la vulnerabilidad a través de la construcción incorrecta de consultas SQL.

1. Cierre el archivo ProductRepository.cs.

1. Pida a GitHub Copilot que propone una estrategia de corrección completa para la vulnerabilidad de inyección de código SQL que incluya técnicas de validación y saneamiento de la entrada.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    #codebase I need to resolve SQL injection vulnerabilities associated with the SearchProducts method in the ProductService.cs file. Notice that user input is directly concatenated into SQL queries without proper parameterization or sanitization. The updated codebase should use parameterized queries or prepared statements, implement proper input validation and sanitization, remove debug logging of SQL queries, and add input length restrictions. My acceptance criteria includes: User input is properly parameterized; No raw SQL construction with user input; Input validation prevents malicious characters; Debug logging removed or sanitized. Review the codebase and identify the code files that must be updated to address the SQL injection vulnerability. Based on your code review and the current Chat conversation, suggest a phased approach to required file updates.
    ```

1. Documente los resultados del análisis como referencia durante la fase de corrección.

    Tome notas sobre las recomendaciones de GitHub Copilot para ambas categorías de vulnerabilidades. Esta documentación guiará la implementación de las correcciones de seguridad en la siguiente tarea.

#### Análisis de las infracciones de almacenamiento de datos de tarjetas de crédito

La vulnerabilidad de almacenamiento de datos de tarjetas de crédito existe en varios archivos: el modelo Order.cs, el servicio PaymentService.cs, el validador SecurityValidator.cs y, posiblemente, la capa de datos OrderRepository.cs. Analizará estos archivos para comprender el alcance completo de la vulnerabilidad.

Siga estos pasos para analizar las infracciones de almacenamiento de datos de tarjetas de crédito:

1. En la carpeta **Models**, abra el archivo **Order.cs** y busque la clase **PaymentInfo**.

1. En el editor de código, seleccione las propiedades **CardNumber** y **CVV** dentro de la clase **PaymentInfo**.

    Observe los comentarios que indican que estas propiedades son vulnerabilidades de seguridad. El almacenamiento de los números de tarjeta completos y de los códigos CVV infringe los requisitos de cumplimiento de PCI DSS.

1. Pida a GitHub Copilot que analice las infracciones de almacenamiento de datos de tarjetas de crédito.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    Why is storing full credit card numbers and CVV codes in the PaymentInfo class a PCI DSS compliance violation? What are the proper ways to handle payment card data securely?
    ```

1. Revise el análisis de GitHub Copilot.

    GitHub Copilot debe explicar que los requisitos de PCI DSS prohíben almacenar datos de autenticación confidenciales después de la autorización, incluidos los códigos CVV. También debe explicar que los números de tarjeta completos se deben tokenizar o enmascarar.

1. Pida instrucciones de corrección específicas.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    How should I modify the PaymentInfo class to comply with PCI DSS requirements? What properties should I add or change to store payment information securely?
    ```

1. Dedique un minuto a revisar las sugerencias de corrección de GitHub Copilot.

    Debería ver recomendaciones para quitar completamente la propiedad CVV, reemplazar CardNumber por una versión enmascarada o token, almacenar solo los últimos 4 dígitos y agregar una propiedad de tipo de tarjeta con fines de visualización.

1. Abra el archivo **PaymentService.cs** y busque el método **ProcessPayment**.

1. En el editor de código, seleccione todo el método **ProcessPayment**.

    Observe que el método crea un objeto PaymentInfo y almacena el número de tarjeta completo y el CVV. Este método también registra información confidencial de pago.

1. Pida a GitHub Copilot que analice el método ProcessPayment para ver las incidencias de almacenamiento de datos de tarjetas de crédito.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    What security vulnerabilities exist in the ProcessPayment method related to credit card data storage and logging? How does this method contribute to the PCI DSS violations?
    ```

1. Revise el análisis de GitHub Copilot.

    GitHub Copilot debe identificar varios problemas: el registro de los números de tarjeta completos y los códigos CVV, el almacenamiento de estos valores en el objeto PaymentInfo y la exposición de datos confidenciales en el flujo de procesamiento.

1. Solicite instrucciones de corrección específicas para el método ProcessPayment.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    How should I modify the ProcessPayment method to handle credit card data securely? What changes are needed to prevent storing and logging sensitive card information?
    ```

1. Abra el archivo **SecurityValidator.cs** y busque el método **ValidateCreditCard**.

1. En el editor de código, seleccione todo el método **ValidateCreditCard**.

    Tenga en cuenta que este método registra el número de tarjeta de crédito completo, lo cual es una vulnerabilidad de seguridad.

1. Pida a GitHub Copilot que analice el método ValidateCreditCard.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    What security issues exist in the ValidateCreditCard method? How should credit card validation be performed without logging sensitive data?
    ```

1. Revise las sugerencias de análisis y corrección de GitHub Copilot.

    GitHub Copilot debe generar una lista de incidencias de seguridad y algunas recomendaciones para que las prácticas de codificación sean seguras. Las recomendaciones pueden incluir quitar o enmascarar el número de tarjeta de crédito en las instrucciones de registro mediante algoritmos, validar los números de tarjeta y mejorar la longitud y la validación del formato del número de tarjeta.

1. Abra el archivo **OrderRepository.cs** en la carpeta **Datos**.

1. Revise el archivo para determinar si controla los objetos PaymentInfo.

    Observe que la clase OrderRepository almacena objetos Order, que incluyen PaymentInfo. Si la clase PaymentInfo almacena los números de tarjeta completos y los códigos CVV, el repositorio conservará esta información confidencial.

1. Pida a GitHub Copilot que analice el impacto de OrderRepository en el almacenamiento de datos de tarjetas de crédito.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    How does the OrderRepository contribute to credit card data storage violations? What happens when Order objects containing PaymentInfo with full card numbers and CVV codes are stored?
    ```

1. Revise el análisis de GitHub Copilot.

    GitHub Copilot debe explicar que el repositorio conserva los datos que se encuentra en los objetos Order y PaymentInfo. Si el modelo PaymentInfo se fija para almacenar solo datos seguros (tokens, últimos 4 dígitos), el repositorio almacenará automáticamente datos seguros en su lugar.

1. Cierre el archivo OrderRepository.cs.

1. Pida a GitHub Copilot que proporcione una estrategia de corrección completa para la incidencia "Corregir las infracciones de almacenamiento de datos de tarjetas de crédito" que incluya técnicas de validación y saneamiento de la entrada.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    #codebase I need to resolve credit card data storage violations associated with the PaymentInfo model in the OrderRepository.cs file. Notice that the model currently stores full card numbers and CVV codes. The updated codebase should never store CVV codes (remove CVV storage completely), tokenize card numbers and store tokens instead of actual card numbers, mask the display of credit card numbers to show only last 4 digits, and implement proper encryption if card data must be stored temporarily. My acceptance criteria includes: CVV storage completely removed; Full card numbers replaced with tokens; Only the last 4 digits of a credit card are stored for display; Card type detection implemented. Review the codebase and identify the code files that must be updated to address the credit card data storage violations. Based on your code review and the current Chat conversation, suggest a phased approach to required file updates.
    ```

1. Documente los resultados del análisis como referencia durante la fase de corrección.

    Tome notas sobre las recomendaciones de GitHub Copilot para ambas categorías de vulnerabilidades. Esta documentación guiará la implementación de las correcciones de seguridad en la siguiente tarea.

### Resolución de incidencias con el modo Agente de GitHub Copilot

El modo Agente de GitHub Copilot permite la implementación autónoma de correcciones de seguridad complejas en varios archivos y métodos. A diferencia del modo Preguntar, que proporciona análisis y recomendaciones, el modo Agente puede modificar directamente el código para implementar mejoras de seguridad. Este enfoque es especialmente eficaz para la corrección sistemática de la seguridad, donde es necesario abordar de forma coherente varias vulnerabilidades relacionadas.

En esta tarea, usará el modo Agente de GitHub Copilot para corregir las incidencias de GitHub que tiene asignadas.

Realice los pasos siguientes para completar esta tarea:

1. Cambie GitHub Copilot Chat al modo Agente.

    El modo Agente permite a GitHub Copilot realizar modificaciones directas de código en función de las instrucciones. El modo de agente sirve para establecer un contexto adecuado al revisar los archivos pertinentes en el código base. Puede agregar archivos y carpetas al contexto manualmente para asegurarse de que el agente tiene la información necesaria para realizar tareas complejas.

1. Dedique un minuto a considerar la estrategia de corrección.

    Cree una estrategia de corrección basada en el análisis que realizó con el modo Preguntar de GitHub Copilot. Tenga en cuenta el orden en el que abordará las incidencias asignadas, el enfoque para resolver las incidencias y cómo comprobar que las vulnerabilidades de código se han corregido correctamente.

    Las dos incidencias de GitHub asignadas son:

    1. 🔐 Corrección de la vulnerabilidad de inyección de código SQL en la búsqueda de productos (prioridad alta)
    1. 🔐 Corrección de las infracciones de almacenamiento de datos de tarjetas de crédito (prioridad crítica)

    Aunque la incidencia de almacenamiento de tarjetas de crédito tiene una gravedad mayor, la incidencia de inyección de código SQL es más sencilla de corregir y se puede solucionar primero. Esto le permite validar el flujo de trabajo con una corrección más sencilla antes de abordar las infracciones de almacenamiento de tarjetas de crédito más complejas.

    Estas incidencias están asociados a archivos y métodos específicos en el código base:

    - **Incidencia de inyección de código SQL**: ProductService.cs (método SearchProducts)
    - **Incidencia de almacenamiento de tarjetas de crédito**: Models/Order.cs (clase PaymentInfo), PaymentService.cs (método ProcessPayment), SecurityValidator.cs (método ValidateCreditCard) y OrderRepository.cs (persistencia de datos)

    > **NOTA**: La extensión Solicitudes de incorporación de cambios de GitHub admite el procesamiento de incidencias individualmente y en ramas independientes. La resolución de incidencias de forma individual proporciona una mejor rastreabilidad, revisiones de código más sencillas y opciones de reversión más seguras si surgen problemas. En un entorno de producción, debe solucionar cada incidencia individualmente con distintas confirmaciones y solicitudes de incorporación de cambios.

#### Resolución de la vulnerabilidad de inyección de código SQL

Siga estos pasos para resolver la vulnerabilidad de inyección de código SQL:

1. Cierre todos los archivos abiertos en el editor de código.

    Cerrar archivos ayuda al agente a centrarse en los archivos que agrega al contexto. Los archivos que se dejan abiertos en el editor de forma involuntaria pueden distraer de la tarea que se está realizando.

1. Agregue el archivo **ProductService.cs** al contexto de chat.

    La incidencia de inyección de código SQL se encuentra principalmente en el método SearchProducts del archivo ProductService.cs.

1. Pida a GitHub Copilot que solucione la vulnerabilidad de inyección de código SQL.

    El análisis que completó con el modo Preguntar de GitHub Copilot reveló que el método construye consultas SQL mediante la entrada del usuario sin un correcto saneamiento. Use el análisis para crear instrucciones de tareas claras que el agente pueda usar para corregir la vulnerabilidad.

    Por ejemplo, puede asignar la siguiente tarea al agente:

    ```text
    #codebase I need you to fix the SQL injection vulnerability in the SearchProducts method. Review the current Chat conversation related to SQL injection vulnerabilities to identify my expected code fixes and acceptance criteria. Remove the simulated SQL query logging that demonstrates the vulnerability, and implement proper input sanitization to safely handle search terms. Ensure that the method still functions correctly for legitimate searches while preventing malicious input. Update the DisplayKnownVulnerabilities method in SecurityValidator.cs to reflect that SQL injection protection is enabled.
    ```

1. Supervise el progreso del agente.

    El agente modificará el código para quitar el registro vulnerable e implementará un control de entrada más seguro.

1. Dedique un minuto a revisar los cambios propuestos y, a continuación, seleccione **Mantener** en la vista Chat.

    Revise siempre las modificaciones sugeridas de GitHub Copilot en el editor de código. Asegúrese de que mantienen la funcionalidad a la vez que abordan el problema de seguridad.

    Los cambios deben incluir:
    - Eliminación del registro de consultas SQL simulado
    - Eliminación o saneamiento del registro de depuración que expone el término de búsqueda
    - Adición de la lógica de validación o saneamiento de la entrada

    En un entorno de producción, el equipo debe completar la siguiente lista de comprobación antes de pasar a la siguiente incidencia:

    - El código ya no contiene la vulnerabilidad.
    - La aplicación sigue funcionando correctamente.
    - Los procedimientos recomendados de seguridad se implementan y no se presentan nuevas incidencias de seguridad.
    - Las pruebas automatizadas (si están disponibles) se superan correctamente.
    - Las actualizaciones de código están claramente documentadas.
    - Los cambios se confirman con mensajes descriptivos y se revisan por un igual antes de combinarse y cerrar la incidencia.

#### Resolución de las infracciones de almacenamiento de datos de tarjetas de crédito

Las infracciones de almacenamiento de datos de tarjetas de crédito abarcan varios archivos y requieren cambios coordinados. Deberá modificar el modelo de datos, actualizar los servicios que controlan los datos de pago y eliminar los datos confidenciales de los registros.

Siga estos pasos para resolver las infracciones de almacenamiento de datos de tarjetas de crédito:

1. Cierre los archivos que estén abiertos en el editor y agregue el archivo **Order.cs** (en la carpeta Models) al contexto de chat.

    La clase PaymentInfo de este archivo almacena los números de tarjeta completos y los códigos CVV, lo que infringe los requisitos de cumplimiento de PCI DSS.

1. Pida a GitHub Copilot que corrija la clase PaymentInfo.

    Por ejemplo, puede asignar la siguiente tarea al agente:

    ```text
    Fix PCI DSS compliance violations in the PaymentInfo class in Order.cs. Remove the CVV property entirely as CVV codes should never be stored. Replace the CardNumber property with a CardLastFourDigits property that stores only the last 4 digits. Add a CardType property to identify the card brand (Visa, Mastercard, etc.). Update the constructor and any initializations accordingly.
    ```

1. Supervise el progreso del agente y revise los cambios propuestos.

    El agente debe modificar la clase PaymentInfo para eliminar el almacenamiento de datos confidenciales. Revise los cambios y seleccione **Mantener** si soluciona la incidencia correctamente.

1. Cierre el archivo Order.cs y agregue el archivo **PaymentService.cs** al contexto de chat.

    El método ProcessPayment de este archivo registra los datos de pago confidenciales y crea objetos PaymentInfo con números de tarjeta completos y códigos CVV.

1. Pida a GitHub Copilot que corrija el método ProcessPayment.

    Por ejemplo, puede asignar la siguiente tarea al agente:

    ```text
    Fix the credit card data handling in the ProcessPayment method in PaymentService.cs. Remove all logging of full card numbers, CVV codes, and other sensitive payment data. Update the PaymentInfo object creation to store only the last 4 digits of the card number and the card type, without storing CVV. Implement card number masking in any remaining log statements (show only last 4 digits). Ensure the payment processing logic still works correctly.
    ```

1. Supervise el progreso del agente.

    Los cambios deben incluir:
    - Eliminación o enmascaramiento de los datos confidenciales en las instrucciones de registro
    - Actualizaciones de la creación de objetos PaymentInfo para que solo se usen los últimos 4 dígitos
    - Eliminación del almacenamiento de CVV
    - Adición de la lógica de detección de tipos de tarjeta (si es necesario)

1. Tómese un minuto para revisar los cambios propuestos en el editor de código y, a continuación, seleccione **Mantener** en la vista Chat.

    Revise siempre las modificaciones sugeridas de GitHub Copilot en el editor de código. Asegúrese de que mantienen la funcionalidad a la vez que abordan el problema de seguridad.

1. Cierre el archivo PaymentService.cs y agregue el archivo **SecurityValidator.cs** al contexto de chat.

    El método ValidateCreditCard registra números de tarjeta de crédito completos.

1. Pida a GitHub Copilot que corrija el método ValidateCreditCard.

    Por ejemplo, puede asignar la siguiente tarea al agente:

    ```text
    Fix the credit card validation logging in the ValidateCreditCard method in SecurityValidator.cs. Remove or mask the full credit card number in log statements, showing only the last 4 digits if logging is necessary. Ensure the validation logic continues to work correctly. Update the DisplayKnownVulnerabilities method to reflect that credit card data storage is now secure.
    ```

1. Supervise el progreso del agente.

    El agente debe actualizar el registro para enmascarar los datos confidenciales y mantener al mismo tiempo la funcionalidad de validación.

1. Tómese un minuto para revisar los cambios propuestos en el editor de código y, a continuación, seleccione **Mantener** en la vista Chat.

    Revise siempre las modificaciones sugeridas de GitHub Copilot en el editor de código. Asegúrese de que mantienen la funcionalidad a la vez que abordan el problema de seguridad.

1. Tenga en cuenta el impacto en OrderRepository.

    El archivo OrderRepository.cs almacena objetos Order, que incluyen PaymentInfo. Puesto que ha actualizado la clase PaymentInfo para almacenar solo datos seguros (últimos 4 dígitos, tipo de tarjeta), el repositorio conservará automáticamente datos seguros en lugar de números de tarjeta completos y códigos CVV. No se necesitan cambios directos en el repositorio, pero debe comprobarlo durante las pruebas.

1. Compile la aplicación para asegurarse de que todos los cambios se compilen correctamente.

    Ejecute el siguiente comando en el terminal:

    ```bash
    dotnet build
    ```

    Si hay errores de compilación, use GitHub Copilot para ayudar a identificar y resolver los problemas introducidos durante las correcciones de seguridad. Las incidencias comunes pueden incluir:
    - Referencias a propiedades eliminadas (CVV, valor de CardNumber completo)
    - Errores de coincidencia de parámetros de constructor
    - Errores de coincidencia de tipos en las asignaciones

### Prueba y comprobación del código refactorizado

Las pruebas completas después de la corrección de seguridad garantizan que las correcciones de vulnerabilidades no introduzcan regresiones funcionales al confirmar que las mejoras de seguridad son eficaces. Este proceso de verificación debe probar los aspectos de seguridad y la funcionalidad empresarial de la aplicación. Las pruebas adecuadas validan que la aplicación mantiene su comportamiento previsto a la vez que se refuerza la seguridad.

En esta tarea, probará sistemáticamente la aplicación ContosoShopEasy actualizada para comprobar que se han resuelto las dos incidencias de seguridad y que la funcionalidad principal permanece intacta.

Realice los pasos siguientes para completar esta tarea:

1. Ejecute la aplicación completa para observar el comportamiento general.

    Ejecute la aplicación y revise la salida de la consola:

    ```bash
    dotnet run
    ```

    Compare la salida con las notas de la ejecución de la aplicación original. Debería ver que se registra información significativamente menos confidencial.

1. Pruebe la corrección de inyección de código SQL.

    Compruebe que el método SearchProducts ya no registra la consulta SQL simulada con la entrada del usuario concatenada directamente en la cadena de consulta. La aplicación debe:

    - Seguir realizando búsquedas de productos correctamente.
    - No mostrar el registro de consultas SQL vulnerables.
    - Controlar los términos de búsqueda de forma segura sin exponer la vulnerabilidad de inyección de código SQL.
    - No registrar en exceso términos de búsqueda sin procesar.

1. Pruebe la corrección de almacenamiento de datos de tarjetas de crédito.

    Compruebe que la clase PaymentInfo y el código relacionado ya no almacenen ni registren números completos de tarjetas de crédito ni códigos CVV. La aplicación debe:

    - No registrar números completos de tarjetas de crédito (compruebe si hay enmascaramiento, por ejemplo, ***1234).
    - No registrar en absoluto códigos CVV.
    - No almacenar códigos CVV en el objeto PaymentInfo.
    - Almacenar solo los últimos 4 dígitos de los números de tarjetas.
    - Continuar procesando los pagos correctamente (simulados).

1. Compruebe las mejoras generales de seguridad.

    Compare la salida de la consola con las observaciones iniciales. Las mejoras clave deben incluir:

    - **Inyección de código SQL**: no hay consultas SQL simuladas que muestren la concatenación de la entrada del usuario.
    - **Datos de tarjetas de crédito**: no hay números de tarjeta completos ni códigos CVV en registros o datos almacenados.
    - La funcionalidad principal de la aplicación (búsqueda de productos, procesamiento de pagos) sigue funcionando correctamente

1. Documente los problemas o áreas restantes para mejorar.

    Anote cualquier problema de seguridad que pueda necesitar atención adicional o cualquier problema funcional que se deba solucionar.

### Confirmación de los cambios y cierre de las incidencias

Las procedimientos adecuados de control de versiones garantizan que las mejoras de seguridad se documentan correctamente y se realiza su seguimiento. Los mensajes de confirmación deben describir claramente las correcciones de seguridad implementadas, lo que facilita a los miembros del equipo comprender qué cambios se han realizado y por qué. Al cerrar las incidencias de GitHub con mensajes de confirmación descriptivos, se crea una pista de auditoría clara de los esfuerzos de corrección de seguridad.

En esta tarea, confirma las mejoras de seguridad en el repositorio y cerrará las incidencias de GitHub correspondientes.

Realice los pasos siguientes para completar esta tarea:

1. Abra la vista de control de código fuente de Visual Studio Code y revise los cambios realizados en cada uno de los archivos actualizados.

    Busque los cambios inesperados que se puedan haber introducido durante el proceso de corrección. Asegúrese de que todos los cambios se alineen con la estrategia de corrección y que no se hayan introducido nuevas vulnerabilidades.

1. Pida a GitHub Copilot que cree un mensaje de confirmación completo.

    Por ejemplo, puede usar la siguiente indicación en la vista Chat:

    ```text
    I need to create a commit message that summarizes the security fixes I implemented for two GitHub issues: "Fix SQL Injection Vulnerability in Product Search" and "Fix Credit Card Data Storage Violations." The commit message should clearly describe the changes made to address each issue, including specific code modifications and the overall impact on application security. Draft a detailed commit message that captures all relevant information.
    ```

1. Tómese un minuto para revisar el mensaje de confirmación propuesto.

    Asegúrese de que refleja con precisión las mejoras de seguridad realizadas y proporciona detalles suficientes para futuras referencias.

    Por ejemplo, el mensaje de confirmación podría ser similar al ejemplo siguiente:

    ```text
    Fix SQL injection and credit card data storage vulnerabilities

    Security improvements implemented:
    - Fix SQL injection in ProductService SearchProducts method
      - Remove vulnerable SQL query logging with user input
      - Implement proper input handling and sanitization
    
    - Fix PCI DSS violations for credit card data storage
      - Remove CVV property from PaymentInfo class
      - Replace CardNumber with CardLastFourDigits
      - Add CardType property for card brand identification
      - Update PaymentService to not log or store sensitive card data
      - Mask credit card numbers in SecurityValidator logs
    
    Fixes #[SQL_INJECTION_ISSUE_NUMBER] #[CREDIT_CARD_ISSUE_NUMBER]
    ```

1. Reemplace `[SQL_INJECTION_ISSUE_NUMBER]` y `[CREDIT_CARD_ISSUE_NUMBER]` por los números de incidencias reales del repositorio de GitHub.

    Puede encontrar estos números en la vista Solicitudes de incorporación de cambios de GitHub en Visual Studio Code o examinando las incidencias en GitHub.

    > **NOTA**: En un entorno de producción, cada incidencia se solucionaría normalmente en distintas confirmaciones con pruebas y revisiones de código individuales. La combinación de ambas correcciones en una sola confirmación se usa aquí para simplificar el flujo de trabajo del ejercicio de entrenamiento.

1. Realice una copia intermedia de los cambios y confírmelos y, a continuación, inserte los cambios en el repositorio de GitHub (o sincronícelos).

1. Abra GitHub y compruebe que las incidencias de GitHub se cierran automáticamente.

    Vaya al repositorio en GitHub y compruebe que las dos incidencias a las que se hace referencia en el mensaje de confirmación están marcadas como cerradas. GitHub cierra automáticamente las incidencias cuando los mensajes de confirmación incluyen la sintaxis "Corrige #[issue_number]".

1. Revise el historial de confirmaciones para asegurarse de que las correcciones de seguridad están documentadas correctamente.

    Compruebe que el mensaje de confirmación describe claramente las mejoras de seguridad y proporciona una buena pista de auditoría para futura referencia.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Por ejemplo, puede que quiera eliminar el repositorio ResolveGitHubIssues. Si usa un equipo local como entorno de laboratorio, puede archivar o eliminar el clon local del repositorio creado para este ejercicio.
