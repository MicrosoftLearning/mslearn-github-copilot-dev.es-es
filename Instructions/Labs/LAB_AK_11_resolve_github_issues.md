<!-- ---
lab:
    title: 'Exercise - Resolve GitHub issues using GitHub Copilot'
    description: 'Learn how to identify and address performance bottlenecks and code inefficiencies using GitHub Copilot tools.'
--- -->

# Resolución de incidencias de GitHub con GitHub Copilot

Las incidencias de GitHub son una manera eficaz de realizar el seguimiento de los errores, mejoras y tareas de un proyecto.

En este ejercicio, usará GitHub Copilot para ayudarle a analizar y resolver incidencias de GitHub relacionadas con vulnerabilidades de seguridad en una aplicación de comercio electrónico.

Este ejercicio debería tardar en completarse**40** minutos aproximadamente.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar su propia cuenta de GitHub y suscripción de GitHub Copilot. Si no tiene una cuenta de GitHub, puede<a href="https://github.com/" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

## Antes de comenzar

El entorno de laboratorio debe incluir lo siguiente: Git 2.48 o posterior, SDK de .NET 9.0 o posterior, Visual Studio Code con la extensión Kit de desarrollo de C# y acceso a una cuenta de GitHub con GitHub Copilot habilitado.

Si usa un equipo local como entorno de laboratorio para este ejercicio:

- Para obtener ayuda a fin de configurar el equipo local como entorno de laboratorio, abra el siguiente vínculo en un explorador:<a href="https://go.microsoft.com/fwlink/?linkid=2320147" target="_blank">Configure los recursos de entorno de laboratorio</a>.

- Para obtener ayuda sobre cómo habilitar la suscripción de GitHub Copilot en Visual Studio Code, abra el siguiente vínculo en un explorador:<a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

Si usa un entorno de laboratorio hospedado para este ejercicio:

- Para obtener ayuda a fin de habilitar la suscripción de GitHub Copilot en Visual Studio Code, pegue la siguiente dirección URL en la barra de navegación del sitio de un explorador:<a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

- Para asegurarse de que el SDK de .NET está configurado para usar el repositorio oficial de NuGet.org como origen para descargar y restaurar paquetes:

    Abra un terminal de comandos y luego ejecute los siguientes comandos:

    ```bash

    dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org

    ```

- Para asegurarse de que Git está configurado para usar su nombre y dirección de correo electrónico:

    Actualice los siguientes comandos con la información y, a continuación, ejecute los comandos:

    ```bash

    git config --global user.name "John Doe"

    ```

    ```bash

    git config --global user.email johndoe@example.com

    ```

## Escenario del ejercicio

Es desarrollador de software y trabaja para una empresa de consultoría. Los clientes necesitan ayuda para resolver incidencias en sus repositorios de GitHub. Debe asegurarse de que todas las incidencias se solucionan y cierran. Puede usar Visual Studio Code y GitHub Copilot como entorno de desarrollo. Se le asigna a la aplicación siguiente:

- ContosoShopEasy: ContosoShopEasy es una aplicación de comercio electrónico que contiene varias vulnerabilidades de seguridad. Las vulnerabilidades representan incidencias comunes de seguridad encontradas en aplicaciones reales.

Este ejercicio incluye las siguientes tareas:

1. Importe el repositorio ContosoShopEasy.
1. Revise las incidencias en GitHub.
1. Clone el repositorio y revise el código base.
1. Analice las incidencias con el modo Preguntar de GitHub Copilot.
1. Resuelva las incidencias con el modo Agente de GitHub Copilot.
1. Pruebe y compruebe el código refactorizado.
1. Confirme los cambios y cierre las incidencias.

> **NOTA**: Para ahorrar tiempo durante este ejercicio de entrenamiento, resolverá un grupo de incidencias e insertará actualizaciones en una sola confirmación. El procesamiento de incidencias por lotes no es un procedimiento recomendado. Microsoft y GitHub recomiendan resolver cada incidencia de forma individual con distintas confirmaciones en lugar de procesarlas por lotes. La resolución de incidencias de forma individual proporciona una mejor rastreabilidad, revisiones de código más sencillas y opciones de reversión más seguras si surgen problemas.

### Importación del repositorio ContosoShopEasy

GitHub Importer le permite crear una copia de un repositorio existente en su propia cuenta de GitHub, lo que le proporciona control total sobre la copia importada. Aunque GitHub Importer no migra incidencias, solicitudes de incorporación de cambios o discusiones, importa flujos de trabajo de Acciones de GitHub. El repositorio que importe incluye un flujo de trabajo de Acciones de GitHub que crea incidencias asociadas con el código base.

En esta tarea, importará el repositorio ContosoShopEasy y ejecutará un flujo de trabajo para crear incidencias de GitHub para las vulnerabilidades de seguridad incluidas en el código base.

Realice los pasos siguientes para completar esta tarea:

1. Abra una ventana del explorador y vaya a GitHub.com.

1. Inicie sesión en su cuenta de GitHub.

1. Abra la pestaña de repositorios.

    Para abrir la pestaña de repositorios, haga clic en el icono de perfil de la esquina superior derecha y seleccione**Repositorios**.

1. En la pestaña Repositorios, seleccione el botón**Nuevo**.

1. En la sección**Crear un nuevo repositorio**, seleccione**Importar un repositorio**.

    Aparece la página**Importar el proyecto a GitHub**.

1. En este página, en**Detalles del repositorio de origen**, escriba la siguiente dirección URL para el repositorio de origen:

    ```plaintext
    https://github.com/MicrosoftLearning/resolve-github-issues-lab-project
    ```

1. En la sección**Detalles del nuevo repositorio**, en la lista desplegable**Propietario**, seleccione el nombre de usuario de GitHub.

1. En el campo**Nombre del repositorio**, escriba**ResolveGitHubIssues** y seleccione**Comenzar importación**.

    GitHub crea el nuevo repositorio en su cuenta con los archivos de proyecto de ContosoShopEasy.

    > **NOTA**: El repositorio puede tardar un minuto o dos en importarse.

1. Espere a que finalice el proceso de importación y abra el nuevo repositorio.

1. Abra la pestaña Acciones del repositorio.

1. En el lado izquierdo de**Todos los flujos de trabajo**, seleccione el flujo de trabajo**Create ContosoShopEasy Training Issues** y, a continuación, seleccione**Ejecutar flujo de trabajo**.

1. En el cuadro de diálogo de flujo de trabajo que aparece, escriba**CREATE** y, a continuación, seleccione**Ejecutar flujo de trabajo**.

1. Supervise el progreso en pantalla del flujo de trabajo.

    Después de un momento, la página se actualizará y mostrará una barra de progreso. El flujo de trabajo debe completarse correctamente en menos de un minuto.

1. Asegúrese de que el flujo de trabajo se completa correctamente antes de continuar.

    Una marca de verificación en un círculo verde a la izquierda del nombre del flujo de trabajo indica que el flujo de trabajo se ejecutó correctamente.

    Si ve una X en un círculo rojo a la izquierda del nombre del flujo de trabajo, significa que se produjo un error en el flujo de trabajo. Si el flujo de trabajo no se ejecuta correctamente, asegúrese de que seleccionó la cuenta al importar el repositorio y de que la cuenta tiene permisos de lectura y escritura. Puede usar la característica**Chat with Copilot** de GitHub para ayudar a diagnosticar el problema.

### Revisión de las incidencias en GitHub

Las incidencias de GitHub sirven como un sistema de seguimiento centralizado para errores, vulnerabilidades de seguridad y solicitudes de mejora. Cada incidencia proporciona contexto sobre el problema, su gravedad y el posible impacto en la aplicación. Comprender estas incidencias antes de profundizar en el código ayuda a establecer prioridades y garantiza una corrección completa.

En esta tarea, revisará las incidencias de GitHub y examinará las vulnerabilidades de seguridad que deben solucionarse.

Realice los pasos siguientes para completar esta tarea:

1. Seleccione la pestaña**Incidencias** del repositorio y, a continuación, dedique un minuto a revisar la página de incidencias.

    Debería ver una lista con 10 incidencias. Observe que las incidencias se definen como errores y que se les ha asignado un nivel de prioridad.

1. Para mostrar solo las incidencias críticas, seleccione la lista desplegable**Etiquetas** y, a continuación, seleccione la etiqueta**crítica**.

    La lista de incidencias se filtra para mostrar solo las incidencias críticas.

    - **🔐 Corregir las infracciones de almacenamiento de datos de tarjetas de crédito**  

    - **🔐 Eliminar las credenciales de administrador codificadas de forma rígida**  

1. Para mostrar solo las incidencias de alta prioridad, seleccione la lista desplegable**Etiquetas**, anule la selección de**crítico** y, a continuación, seleccione la etiqueta**alta prioridad**.

    La lista de incidencias se filtra para mostrar solo las incidencias de alta prioridad.

    - **🔐 Corregir la omisión de seguridad de validación de entrada**  

    - **🔐 Eliminar los datos confidenciales del registro de depuración**  

    - **🔐 Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos**  

    - **🔐 Reemplazar el hash de contraseña MD5 por alternativa segura**  

1. Seleccione la incidencia**Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos**.

1. Dedique un minuto a revisar los detalles de la incidencia.

    Los detalles de la incidencia deben describir el problema y la corrección esperada.

    > **NOTA**: El proceso usado para generar incidencias, incluidos los procesos manuales frente a los automatizados, afecta a la calidad general y la precisión de las descripciones de las incidencias. Las incidencias incluidas en este entrenamiento se escribieron mediante el modo agente de GitHub Copilot después de que el agente revisara el código base. GitHub Copilot generó descripciones muy detalladas de las vulnerabilidades, ubicaciones de código, ejemplos del código vulnerable, riesgos de seguridad y criterios de aceptación para las correcciones.

1. Observe que no se ha asignado a nadie a la incidencia.

1. Vuelva a la pestaña Incidencias y borre los filtros.

1. Seleccione todas las incidencias y, a continuación, use la lista desplegable**Asignar** para asignárselos a sí mismo.

    Asignarse las incidencias a sí mismo ayuda a realizar un seguimiento del progreso a medida que trabaja en el proceso de corrección.

### Clonación del repositorio y revisión del código base

Comprender la estructura y la funcionalidad de un código base existente es esencial antes de implementar correcciones de seguridad. La aplicación ContosoShopEasy sigue una arquitectura en capas típica de las aplicaciones empresariales, con una separación clara entre modelos, servicios, acceso a datos y componentes de seguridad. Revisar la estructura de código y ejecutar la aplicación ayuda a establecer una línea base para las pruebas después de implementar mejoras de seguridad.

En esta tarea, clonará el repositorio ContosoShopEasy, examinará la estructura del proyecto, observará el comportamiento actual de la aplicación y revisará las vulnerabilidades de seguridad.

Realice los pasos siguientes para completar esta tarea:

1. Abra la pestaña Código del repositorio.

1. Clone el repositorio ResolveGitHubIssues en el entorno de desarrollo local.

    Por ejemplo, puede usar los pasos siguientes para clonar el repositorio mediante la CLI de Git:

    1. Copie la dirección URL del repositorio seleccionando el botón**Código** y, a continuación, copie la dirección URL HTTPS.

    1. Abra una ventana de terminal, vaya al directorio donde desea clonar el repositorio y ejecute el siguiente comando (reemplazando**your-username** por su nombre de usuario de GitHub):

    ```bash
    git clone https://github.com/your-username/ResolveGitHubIssues.git
    ```

1. Abra el repositorio clonado en Visual Studio Code.

    Vaya a la carpeta del repositorio y ábrala en Visual Studio Code. Asegúrese de que tiene instaladas y habilitadas las extensiones GitHub Copilot y GitHub Copilot Chat.

1. Examine la estructura del proyecto en la vista EXPLORER.

    La aplicación ContosoShopEasy sigue una arquitectura en capas con los siguientes componentes:

    - **Models/**: Contiene modelos de datos para**Category.cs**,**Order.cs**,**Product.cs** y**User.cs**.

    - **Services/**: Contiene lógica de negocios en**OrderService.cs**,**PaymentService.cs**,**ProductService.cs** y**UserService.cs**.

    - **Data/**: Contiene repositorios de datos en**OrderRepository.cs**,**ProductRepository.cs** y**UserRepository.cs**.

    - **Security/**: Contiene lógica de validación de seguridad en**SecurityValidator.cs**

    - **Program.cs**: Punto de entrada principal de la aplicación con configuración de inserción de dependencias

    - **README.md**: Documentación que explica el propósito y las vulnerabilidades de la aplicación

1. Compile y ejecute la aplicación para observar su comportamiento actual.

    Ejecute los siguientes comandos en una ventana de terminal:

    ```bash
    cd ContosoShopEasy
    dotnet build
    dotnet run
    ```

    La aplicación ejecuta una simulación del flujo de trabajo de comercio electrónico que expone vulnerabilidades de seguridad a través del registro detallado de la consola.

1. Revise la salida de la consola.

    Observe que la aplicación registra información confidencial, como contraseñas, números de tarjeta de crédito, credenciales de administrador y detalles internos del sistema. Esta salida es una prueba clara de los problemas de seguridad que se deben solucionar.

    > **NOTA**: La lógica de código y el registro en esta aplicación están diseñados para exponer vulnerabilidades de seguridad. Aunque la implementación se ha intentado, los registros resaltan los problemas de seguridad que son comunes en las aplicaciones reales.

1. Para comenzar un proceso de revisión que identifique las vulnerabilidades de seguridad en el código base, expanda la carpeta**Models** y abra el archivo**Order.cs**.

1. Desplácese hacia abajo hasta encontrar la clase**PaymentInfo**.

    Observe los comentarios relativos a las propiedades CardNumber y CVV. Este código está relacionado con la incidencia "Corregir infracciones de almacenamiento de datos de tarjetas de crédito".

1. Expanda la carpeta**Security** y abra el archivo**SecurityValidator.cs**.

1. Dedique un minuto a buscar las siguientes incidencias de seguridad:

    - Cerca de la parte superior del archivo, observe el comentario relacionado con las constantes de credenciales de administrador (líneas 7-9). Este código está relacionado con la incidencia "Eliminar las credenciales de administrador codificadas de forma rígida".

    - Busque el método ValidateInput y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Corregir la omisión de seguridad de validación de entrada".

    - Busque el método ValidateEmail y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Mejorar la seguridad de validación del correo electrónico".

    - Busque el método ValidatePasswordStrength y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Reforzar los requisitos de seguridad de contraseñas".

    - Busque el método GenerateSessionToken y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Corregir la generación de tokens de sesión predecibles".

    - Busque el método RunSecurityAudit y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Reducir la divulgación de información en los mensajes de error".

1. Expanda la carpeta**Services** y abra el archivo**UserService.cs**.

1. Dedique un minuto a buscar las siguientes incidencias de seguridad:

    - Busque los métodos RegisterUser, LoginUser y ValidateUserInput y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con las incidencias "Eliminar los datos confidenciales del registro de depuración".
    - Busque el método GetMd5Hash y revise los comentarios que describen las vulnerabilidades de seguridad. Este código está relacionado con la incidencia "Reemplazar el hash de contraseña MD5 por alternativa segura".

1. Abra el archivo**PaymentService.cs**.

1. Dedique un minuto a revisar los comentarios que describen las vulnerabilidades de seguridad.

    Este código está relacionado con la incidencia "Eliminar los datos confidenciales del registro de depuración".

1. Abra el archivo**ProductService.cs**.

1. Dedique un minuto a revisar el método SearchProducts.

    Este código está relacionado con la incidencia "Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos".

### Análisis de las incidencias con el modo Preguntar de GitHub Copilot

El modo Preguntar de GitHub Copilot proporciona funcionalidades de análisis de código inteligentes que pueden ayudar a identificar vulnerabilidades de seguridad, comprender su posible impacto y sugerir estrategias de corrección. Al analizar sistemáticamente cada problema de seguridad, puede desarrollar una comprensión completa de los problemas antes de implementar correcciones. Este enfoque garantiza que las soluciones aborden las causas principales en lugar de solo los síntomas.

En esta tarea, usará el modo Preguntar de GitHub Copilot para analizar sistemáticamente las vulnerabilidades de seguridad.

Realice los pasos siguientes para completar esta tarea:

1. Abra la vista GitHub Copilot Chat y asegúrese de que el modo Preguntar esté seleccionado.

    Si la vista Chat aún no está abierta, seleccione el icono**Chat** situado en la parte superior de la ventana de Visual Studio Code. Compruebe que el modo de chat está establecido en**Preguntar** y que está usando el modelo**GPT-4.1**.

1. Abra el archivo**ProductService.cs** y busque el método**SearchProducts**.

1. En el editor de código, seleccione todo el método**SearchProducts**.

    Al seleccionar código en el editor, el chat se centra en ese contexto. GitHub Copilot usa el código seleccionado para proporcionar análisis y recomendaciones pertinentes.

1. Pida a GitHub Copilot que analice el código de vulnerabilidad de inyección de código SQL.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    Analyze the SearchProducts method for security vulnerabilities. What makes this code susceptible to SQL injection attacks, and what are the potential consequences if an attacker exploits this vulnerability?
    ```

1. Revise el análisis de GitHub Copilot y, a continuación, solicite instrucciones de corrección específicas.

    Por ejemplo, después de revisar el análisis inicial, puede enviar la siguiente indicación:

    ```text
    How can I modify this method to prevent SQL injection attacks? What secure coding practices should I implement to safely handle user input in database queries?
    ```

1. Dedique un minuto a revisar las sugerencias de corrección de GitHub Copilot.

1. Abra el archivo**UserService.cs** y busque el método**GetMd5Hash**.

1. En el editor de código, seleccione todo el método**GetMd5Hash**.

1. Pida a GitHub Copilot que analice la vulnerabilidad de hash de contraseña no segura.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    Why is MD5 hashing unsuitable for password storage? What are the security risks of using MD5 for passwords, and what stronger alternatives should I use instead?
    ```

1. Revise el análisis de GitHub Copilot y, a continuación, solicite instrucciones de corrección específicas.

    Por ejemplo, después de revisar el análisis inicial, puede enviar la siguiente indicación:

    ```text
    Show me how to implement secure password hashing using bcrypt or PBKDF2. What additional security measures should I implement for password handling?
    ```

1. Dedique un minuto a revisar las sugerencias de corrección de GitHub Copilot.

1. En el archivo**UserService.cs**, busque los métodos**RegisterUser** y**LoginUser**.

    Estos métodos registran la información del usuario. El registro de información confidencial es una vulnerabilidad de seguridad.

1. En el editor de código, seleccione ambos métodos.

1. Pida a GitHub Copilot que analice la vulnerabilidad de registro de datos confidenciales.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    What sensitive information is being logged in the user registration and login methods? Why is logging passwords and user data a security risk?
    ```

1. Revise el análisis de GitHub Copilot y, a continuación, solicite instrucciones de corrección específicas.

    Por ejemplo, después de revisar el análisis inicial, puede enviar la siguiente indicación:

    ```text
    How can I modify these methods to prevent sensitive data logging? What secure logging practices should I implement to protect user information?
    ```

1. Dedique un minuto a revisar las sugerencias de corrección de GitHub Copilot.

1. Abra el archivo**PaymentService.cs** y busque el método**ProcessPayment**.

1. En el editor de código, seleccione todo el método**ProcessPayment**.

1. Pida a GitHub Copilot que analice el registro de datos de pago confidenciales.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    What sensitive payment information is being logged in this method? Why is logging credit card numbers and CVV codes a security risk?
    ```

1. Abra el archivo**SecurityValidator.cs** y busque las constantes de credenciales de administrador cerca de la parte superior del archivo.

1. En el editor de código, seleccione las constantes de credenciales de administrador codificadas de forma rígida.

1. Pida a GitHub Copilot que analice la vulnerabilidad de credenciales codificadas de forma rígida.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    What security risks are created by hardcoding admin credentials in source code? How should application credentials be managed securely in production environments?
    ```

1. Revise el análisis de GitHub Copilot y, a continuación, solicite instrucciones de corrección específicas.

    Por ejemplo, después de revisar el análisis inicial, puede enviar la siguiente indicación:

    ```text
    What are best practices for managing application credentials securely? How can I implement secure credential management in this application?
    ```

1. Dedique un minuto a revisar las sugerencias de corrección de GitHub Copilot.

1. En el archivo**SecurityValidator.cs**, busque el método**ValidateInput**.

1. En el editor de código, seleccione todo el método**ValidateInput**.

1. Pida a GitHub Copilot que analice la vulnerabilidad de omisión de validación de entrada.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    What makes this input validation method ineffective? Why does it detect dangerous input but still return true, and how should proper input validation work?
    ```

1. Revise el análisis de GitHub Copilot y, a continuación, solicite instrucciones de corrección específicas.

    Por ejemplo, después de revisar el análisis inicial, puede enviar la siguiente indicación:

    ```text
    How can I modify this method to implement effective input validation? What secure coding practices should I follow to prevent input validation bypass vulnerabilities?
    ```

1. Dedique un minuto a revisar las sugerencias de corrección de GitHub Copilot.

1. En el archivo**SecurityValidator.cs**, busque el método**GenerateSessionToken**.

1. En el editor de código, seleccione todo el método**GenerateSessionToken**.

1. Pida a GitHub Copilot que analice la vulnerabilidad de generación de tokens de sesión predecibles.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    Why are predictable session tokens based on username and timestamp a security risk? How should secure, unpredictable session tokens be generated?
    ```

1. Revise el análisis de GitHub Copilot y, a continuación, solicite instrucciones de corrección específicas.

    Por ejemplo, después de revisar el análisis inicial, puede enviar la siguiente indicación:

    ```text
    How can I modify this method to generate secure, unpredictable session tokens? What cryptographic techniques should I use to enhance session token security?
    ```

1. Dedique un minuto a revisar las sugerencias de corrección de GitHub Copilot.

1. En el archivo**SecurityValidator.cs**, busque el método**ValidateEmail**.

1. En el editor de código, seleccione todo el método**ValidateEmail**.

1. Pida a GitHub Copilot que analice la vulnerabilidad de validación de correo electrónico poco seguro.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    What makes this email validation insufficient? What are the security risks of weak email validation, and how should proper email validation be implemented?
    ```

1. Revise el análisis de GitHub Copilot y, a continuación, solicite instrucciones de corrección específicas.

    Por ejemplo, después de revisar el análisis inicial, puede enviar la siguiente indicación:

    ```text
    How can I modify this method to implement robust email validation? What techniques should I use to ensure email addresses are properly validated?
    ```

1. En el archivo**SecurityValidator.cs**, busque el método**ValidatePasswordStrength**.

1. En el editor de código, seleccione todo el método**ValidatePasswordStrength**.

1. Pida a GitHub Copilot que analice la vulnerabilidad de los requisitos de contraseña insuficientes.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    Why are these password requirements insufficient for security? What are proper password complexity requirements, and how should password strength be validated?
    ```

1. Revise el análisis de GitHub Copilot y, a continuación, solicite instrucciones de corrección específicas.

    Por ejemplo, después de revisar el análisis inicial, puede enviar la siguiente indicación:

    ```text
    How can I modify this method to enforce strong password requirements? What best practices should I follow for password strength validation?
    ```

1. Dedique un minuto a revisar las sugerencias de corrección de GitHub Copilot.

1. En la carpeta**Models**, abra el archivo**Order.cs** y busque la clase**PaymentInfo**.

1. En el editor de código, seleccione las propiedades**CardNumber** y**CVV** dentro de la clase**PaymentInfo**.

1. Pida a GitHub Copilot que analice las infracciones de almacenamiento de datos de tarjetas de crédito.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    Why is storing full credit card numbers and CVV codes a PCI DSS compliance violation? What are the proper ways to handle payment card data securely?
    ```

1. Vuelva al archivo**SecurityValidator.cs** y busque el método**RunSecurityAudit**.

1. En el editor de código, seleccione todo el método**RunSecurityAudit**.

1. Pida a GitHub Copilot que analice la vulnerabilidad de divulgación de información.

    Por ejemplo, puede enviar la siguiente indicación:

    ```text
    How does the security audit method create information disclosure vulnerabilities? What information should never be exposed in logs or error messages?
    ```

1. Documente los resultados del análisis como referencia durante la fase de corrección.

    Tome notas sobre las recomendaciones de GitHub Copilot para cada categoría de vulnerabilidad. Esta documentación guiará la implementación de las correcciones de seguridad en la siguiente tarea.

### Resolución de incidencias con el modo Agente de GitHub Copilot

El modo Agente de GitHub Copilot permite la implementación autónoma de correcciones de seguridad complejas en varios archivos y métodos. A diferencia del modo Preguntar, que proporciona análisis y recomendaciones, el modo Agente puede modificar directamente el código para implementar mejoras de seguridad. Este enfoque es especialmente eficaz para la corrección sistemática de la seguridad, donde es necesario abordar de forma coherente varias vulnerabilidades relacionadas.

En esta tarea, usará el modo Agente de GitHub Copilot para implementar correcciones de seguridad completas para todas las vulnerabilidades identificadas en la aplicación ContosoShopEasy.

Realice los pasos siguientes para completar esta tarea:

1. Cambie GitHub Copilot Chat al modo Agente.

    El modo Agente permite a GitHub Copilot realizar modificaciones directas de código en función de las instrucciones. El modo de agente sirve para establecer un contexto adecuado al revisar los archivos pertinentes en el código base. Puede agregar archivos y carpetas al contexto manualmente para asegurarse de que el agente tiene la información necesaria para realizar tareas complejas.

1. Dedique un minuto a considerar la estrategia de corrección.

    Según su análisis mediante el modo Preguntar de GitHub Copilot, planee su enfoque para abordar las vulnerabilidades de seguridad.

    Las incidencias de GitHub, en orden, comenzando por la más crítica, son las siguientes:

    1. 🔐 Corregir la vulnerabilidad de inyección de código SQL en la búsqueda de productos
    1. 🔐 Reemplazar el hash de contraseña MD5 por alternativa segura
    1. 🔐 Eliminar los datos confidenciales del registro de depuración
    1. 🔐 Eliminar las credenciales de administrador codificadas de forma rígida
    1. 🔐 Corregir las infracciones de almacenamiento de datos de tarjetas de crédito
    1. 🔐 Corregir la omisión de seguridad de validación de entrada
    1. 🔐 Corregir la generación de tokens de sesión predecibles
    1. 🔐 Mejorar la seguridad de validación del correo electrónico
    1. 🔐 Reforzar los requisitos de seguridad de contraseñas
    1. 🔐 Reducir la divulgación de información en mensajes de error

    Estas incidencias están asociadas a archivos y métodos específicos en el código base. Cuando se organiza por asociación de archivos, las incidencias son las siguientes:

    - **ProductService.cs**: Incidencia n.º 1
    - **UserService.cs**: Incidencias n.º 2 y n.º 3
    - **PaymentService.cs**: Incidencia n.º 3
    - **SecurityValidator.cs**: Incidencias n.º 4, nº. 6, n.º 7, n.º 8, n.º 9 y n.º 10
    - **Modelos/Order.cs**: Incidencia n.º 5

    La estrategia de corrección debe consistir en abordar cada incidencia sistemáticamente para garantizar así que las correcciones se implementan correctamente y de forma coherente.

1. Cierre todos los archivos abiertos en el editor de código para empezar con un contexto limpio.

1. Agregue el archivo**ProductService.cs** al contexto de chat.

    La incidencia de inyección de código SQL está asociada al archivo ProductService.cs y al método SearchProducts en particular.

1. Pida a GitHub Copilot que solucione primero la vulnerabilidad de inyección de código SQL.

    El análisis mediante el modo Preguntar de GitHub Copilot reveló que el método construye consultas SQL mediante la entrada de usuario sin un correcto saneamiento.

    El análisis se puede usar para construir una instrucción clara para que el agente corrija la vulnerabilidad. Por ejemplo, puede asignar la siguiente tarea al agente:

    ```text
    Fix the SQL injection vulnerability in the SearchProducts method. Remove the simulated SQL query logging that demonstrates the vulnerability, and implement proper input sanitization to safely handle search terms. Ensure the method still functions correctly for legitimate searches while preventing malicious input.
    ```

1. Supervise el progreso del agente.

    El agente modificará el código para quitar el registro vulnerable e implementará un control de entrada más seguro.

1. Dedique un minuto a revisar los cambios propuestos y, a continuación, seleccione**Mantener** en la vista Chat.

    Revise siempre las modificaciones sugeridas de GitHub Copilot en el editor de código. Asegúrese de que mantienen la funcionalidad a la vez que abordan el problema de seguridad.

    En un entorno de producción, el equipo debe completar la siguiente lista de comprobación antes de pasar a la siguiente incidencia:

    - El código ya no contiene la vulnerabilidad.
    - La aplicación sigue funcionando correctamente.
    - Los procedimientos recomendados de seguridad se implementan y no se presentan nuevas incidencias de seguridad.
    - Las pruebas automatizadas (si están disponibles) se superan correctamente.
    - Las actualizaciones de código están claramente documentadas.
    - Los cambios se confirman con mensajes descriptivos y se revisan por un igual antes de combinarse y cerrar la incidencia.

1. Implemente el hash de contraseñas seguras.

    Céntrese en el archivo`UserService.cs` y use la indicación siguiente:

    ```text
    Replace the MD5 password hashing with bcrypt or PBKDF2. Update the GetMd5Hash method to use a cryptographically secure hashing algorithm with proper salt generation. Ensure compatibility with existing user authentication while improving security.
    ```

1. Revise y pruebe los cambios de hash de contraseña.

    El agente implementará un hash de contraseña más seguro. A fin de probar los cambios, ejecute la aplicación para asegurarse de que el registro de usuario y el inicio de sesión siguen funcionando correctamente.

1. Solucionar el registro de datos confidenciales (incidencia n.º 3).

    Céntrese en los archivos`PaymentService.cs` y`UserService.cs` e indique al agente:

    ```text
    Fix sensitive data logging throughout the application. Remove logging of passwords, full credit card numbers, CVV codes, and other sensitive information. Implement secure logging that masks sensitive data while maintaining useful operational information.
    ```

1. Eliminar las credenciales de administrador codificadas de forma rígida (incidencia n.º 4).

    Céntrese en el archivo`SecurityValidator.cs` y use esta indicación:

    ```text
    Remove hardcoded admin credentials from the SecurityValidator class. Replace the hardcoded ADMIN_USERNAME and ADMIN_PASSWORD constants with a secure configuration approach using environment variables while maintaining the functionality for educational demonstration purposes.
    ```

1. Corregir las infracciones del almacenamiento de datos de tarjetas de crédito (incidencia n.º 5).

    Céntrese en el archivo`Models/Order.cs` e indique al agente:

    ```text
    Fix PCI DSS compliance violations in the Order model. Remove or modify the CardNumber and CVV properties to avoid storing full credit card numbers and CVV codes. Implement secure payment data handling that stores only last 4 digits for display purposes.
    ```

1. Corregir la omisión de validación de entrada (incidencia n.º 6).

    Indique al agente que corrija la vulnerabilidad de validación de entrada:

    ```text
    Fix the ValidateInput method in SecurityValidator that currently always returns true despite detecting threats. Implement proper input validation that actually rejects dangerous content when SQL injection, XSS, or other malicious patterns are detected.
    ```

1. Implementar la generación de tokens de sesión seguros (incidencia n.º 7).

    Céntrese en la vulnerabilidad de los tokens de sesión:

    ```text
    Replace the predictable session token generation in GenerateSessionToken method with a cryptographically secure random token generator. Remove the username and timestamp-based pattern and implement unpredictable tokens with sufficient entropy.
    ```

1. Reforzar la validación de correo electrónico (incidencia n.º 8).

    Solucione la validación de correo electrónico poco seguro:

    ```text
    Fix the ValidateEmail method that only checks for '@' and '.' characters. Implement proper email format validation using regex or built-in validation methods. Remove email logging and add appropriate length restrictions.
    ```

1. Mejorar los requisitos de contraseña (incidencia n.º 9).

    Céntrese en la validación de la seguridad de la contraseña:

    ```text
    Strengthen the ValidatePasswordStrength method that currently only requires 4 characters. Implement proper password complexity requirements including minimum 8 characters, uppercase, lowercase, numbers, and special characters. Remove password logging.
    ```

1. Reducir la divulgación de información (incidencia n.º 10).

    Solucione las incidencias de auditoría de seguridad y registro de depuración:

    ```text
    Fix information disclosure vulnerabilities by removing or restricting the RunSecurityAudit method and reducing verbose error messages throughout the application. Remove sensitive system information from logs while maintaining useful debugging capabilities.
    ```

1. Pruebe la aplicación.

    Una vez que el agente implemente correcciones para cada categoría de vulnerabilidad, ejecute la aplicación para asegurarse de que se conserva la funcionalidad:

    ```bash
    dotnet build
    dotnet run
    ```

1. Compruebe que las mejoras de seguridad no interrumpen la funcionalidad básica.

    Asegúrese de que la búsqueda de productos, el registro de usuarios, el procesamiento de pagos y otras características principales siguen funcionando correctamente después de implementar las correcciones de seguridad.

### Prueba y comprobación del código refactorizado

Las pruebas completas después de la corrección de seguridad garantizan que las correcciones de vulnerabilidades no introduzcan regresiones funcionales al confirmar que las mejoras de seguridad son eficaces. Este proceso de verificación debe probar los aspectos de seguridad y la funcionalidad empresarial de la aplicación. Las pruebas adecuadas validan que la aplicación mantiene su comportamiento previsto a la vez que se refuerza la seguridad.

En esta tarea, probará sistemáticamente la aplicación ContosoShopEasy actualizada para comprobar que se han resuelto los problemas de seguridad y que la funcionalidad principal permanece intacta.

Realice los pasos siguientes para completar esta tarea:

1. Compile la aplicación y resuelva los errores de compilación.

    Ejecute el siguiente comando para asegurarse de que el código se compila correctamente:

    ```bash
    dotnet build
    ```

    Si hay errores de compilación, use GitHub Copilot para ayudar a identificar y resolver los problemas introducidos durante las correcciones de seguridad.

1. Ejecute la aplicación completa para observar el comportamiento general.

    Ejecute la aplicación y revise la salida de la consola:

    ```bash
    dotnet run
    ```

    Compare la salida con las notas de la ejecución de la aplicación original. Debería ver que se registra información significativamente menos confidencial.

1. Probar la corrección de inyección de código SQL (incidencia n.º 1).

    Compruebe que el método`SearchProducts` ya no registra consultas SQL vulnerables y que la funcionalidad de búsqueda sigue funcionando correctamente con términos de búsqueda legítimos.

1. Comprobar las mejoras de seguridad de la contraseña (incidencia n.º 2).

    Compruebe que los procesos de registro e inicio de sesión del usuario ya no registran contraseñas en texto no cifrado y que se implementa el hash de contraseña más seguro. La aplicación debe seguir autenticando a los usuarios correctamente.

1. Confirmar las correcciones de registro de datos confidenciales (incidencia n.º 3).

    Asegúrese de que el procesamiento de pagos y las operaciones de usuario ya no registren contraseñas, números de tarjeta de crédito completos o códigos CVV, pero mantengan la capacidad de procesar transacciones correctamente.

1. Validar la eliminación de credenciales codificadas de forma rígida (incidencia n.º 4).

    Compruebe que las credenciales de administrador codificadas de forma rígida ya no se muestran en registros o auditorías de seguridad, mientras que la funcionalidad de administrador sigue siendo accesible a través de la configuración segura.

1. Probar el cumplimiento del almacenamiento de tarjetas de crédito (incidencia n.º 5).

    Confirme que el modelo de pedido ya no almacena números de tarjetas de crédito completos o códigos CVV, y que solo se conserva la información de pago enmascarada con fines de visualización.

1. Comprobar las correcciones de validación de entrada (incidencia n.º 6).

    Confirme que el método ValidateInput mejorado ahora rechaza correctamente las entradas peligrosas en lugar de simplemente registrar advertencias y devolver true.

1. Comprobar la seguridad de los tokens de sesión (incidencia n.º 7).

    Si se generan tokens de sesión durante la ejecución de la aplicación, confirme que parezcan aleatorios e imprevisibles en lugar de seguir el patrón de marca de tiempo de nombre de usuario anterior.

1. Probar las mejoras de validación de correo electrónico (incidencia n.º 8).

    Compruebe que la validación de correo electrónico ahora rechaza correctamente los formatos de correo electrónico no válidos en lugar de aceptar cualquier cadena con caracteres "@" and "".

1. Validar las mejoras de los requisitos de contraseña (incidencia n.º 9).

    Pruebe que la validación de contraseñas ahora aplica los requisitos de complejidad adecuados en lugar de aceptar cualquier cadena de cuatro caracteres.

1. Revisar las correcciones de divulgación de información (incidencia n.º 10).

    Compruebe que el método de auditoría de seguridad se elimina o restringe y que los mensajes de error detallados ya no exponen información confidencial del sistema.

1. Compare la posición general de seguridad con la versión original.

    Ejecute la aplicación y compare la salida de la consola con las observaciones iniciales. La aplicación debe mostrar mejoras importantes de la seguridad al tiempo que mantiene toda la funcionalidad básica.

1. Documente los problemas o áreas restantes para mejorar.

    Anote cualquier problema de seguridad que pueda necesitar atención adicional o cualquier problema funcional que se deba solucionar.

### Confirmación de los cambios y cierre de las incidencias

Las procedimientos adecuados de control de versiones garantizan que las mejoras de seguridad se documentan correctamente y se realiza su seguimiento. Los mensajes de confirmación deben describir claramente las correcciones de seguridad implementadas, lo que facilita a los miembros del equipo comprender qué cambios se han realizado y por qué. Al cerrar las incidencias de GitHub con mensajes de confirmación descriptivos, se crea una pista de auditoría clara de los esfuerzos de corrección de seguridad.

En esta tarea, confirma las mejoras de seguridad en el repositorio y cerrará las incidencias de GitHub correspondientes.

Realice los pasos siguientes para completar esta tarea:

1. Revise todos los cambios realizados en el código base.

    Use Git para ver qué archivos se han modificado:

    ```bash
    git status
    git diff
    ```

1. Realice una copia intermedia de todos los cambios relacionados con la seguridad para confirmar.

    Agregue los archivos modificados al área de almacenamiento provisional:

    ```bash
    git add .
    ```

1. Confirme todas las correcciones de seguridad con un mensaje completo que haga referencia a todas las incidencias de GitHub.

    Cree una única confirmación que solucione todas las vulnerabilidades de seguridad identificadas en el ejercicio de entrenamiento:

    ```bash
    git commit -m "Fix all ContosoShopEasy security vulnerabilities

    Security improvements implemented:
    - Fix SQL injection in ProductService SearchProducts method
    - Replace MD5 with secure password hashing (bcrypt/PBKDF2)
    - Remove sensitive data from debug logging (passwords, card numbers, CVV)
    - Remove hardcoded admin credentials, use environment variables
    - Fix PCI DSS violations in Order model (remove full card storage)
    - Fix input validation bypass to properly reject dangerous input
    - Implement secure session token generation with crypto randomness
    - Strengthen email validation with proper format checking
    - Improve password requirements (8+ chars, complexity rules)
    - Reduce information disclosure from security audit and debug logs

    Fixes #1 #2 #3 #4 #5 #6 #7 #8 #9 #10"
    ```

    > **NOTA**: En un entorno de producción, cada incidencia se solucionaría normalmente en distintas confirmaciones con pruebas y revisiones de código individuales. Este enfoque de una sola confirmación se usa aquí solo para ahorrar tiempo durante el ejercicio de entrenamiento.

1. Inserte los cambios en el repositorio de GitHub.

    ```bash
    git push origin main
    ```

1. Compruebe que las incidencias de GitHub se cierran automáticamente.

    Vaya al repositorio en GitHub y compruebe que las incidencias están marcadas como cerradas debido a los mensajes de confirmación con los que se les hace referencia.

1. Revise el historial de confirmaciones para asegurarse de que todas las correcciones de seguridad están documentadas correctamente.

    Compruebe que los mensajes de confirmación describen claramente las mejoras de seguridad y proporcionan una buena pista de auditoría para futuras referencias.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Por ejemplo, puede que quiera eliminar el repositorio ResolveGitHubIssues. Si usa un equipo local como entorno de laboratorio, puede archivar o eliminar el clon local del repositorio creado para este ejercicio.
