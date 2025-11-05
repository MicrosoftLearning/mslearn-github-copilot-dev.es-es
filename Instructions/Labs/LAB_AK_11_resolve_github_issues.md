<!-- ---
lab:
    title: 'Exercise - Resolve GitHub issues using GitHub Copilot'
    description: 'Learn how to identify and address performance bottlenecks and code inefficiencies using GitHub Copilot tools.'
--- -->

# Resolución de incidencias de GitHub con GitHub Copilot

Las incidencias de GitHub son una manera eficaz de realizar el seguimiento de los errores, mejoras y tareas de un proyecto. En este ejercicio, aprenderá a usar GitHub Copilot para analizar y resolver incidencias en código base de ejemplo.

En este ejercicio, trabajará con una aplicación de comercio electrónico de ejemplo denominada ContosoShopEasy. La aplicación contiene varias vulnerabilidades de seguridad que se han registrado como incidencias de GitHub. El objetivo es usar GitHub Copilot para ayudarle a analizar y resolver estas incidencias.

Este ejercicio debería tardar en completarse**40** minutos aproximadamente.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar su propia cuenta de GitHub y suscripción de GitHub Copilot. Si no tiene una cuenta de GitHub, puede<a href="https://github.com/" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

## Antes de comenzar

El entorno de laboratorio debe incluir lo siguiente: Git 2.48 o posterior, SDK de .NET 9.0 o posterior, CLI de GitHub, Visual Studio Code con la extensión del Kit de desarrollo de C# y acceso a una cuenta de GitHub con GitHub Copilot habilitado.

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

Es desarrollador de software y trabaja para una empresa de consultoría. Los clientes necesitan ayuda para resolver incidencias registradas en un proyecto de GitHub. El objetivo es usar las incidencias como guía al actualizar el proyecto de código mediante GitHub Copilot en Visual Studio Code. Debe asegurarse de que todas las incidencias se solucionan y cierran. Se le asigna a la aplicación siguiente:

- ContosoShopEasy: una aplicación realista de comercio electrónico con varias vulnerabilidades de seguridad que se han registrado como incidencias de GitHub. La aplicación muestra problemas comunes de seguridad encontrados en aplicaciones reales mientras se mantiene un flujo de trabajo funcional de comercio electrónico.

Este ejercicio incluye las siguientes tareas:

1. Importe el repositorio ContosoShopEasy.
1. Revise las incidencias en GitHub.
1. Clone el repositorio y revise el código base.
1. Analice las incidencias con el modo Preguntar de GitHub Copilot.
1. Resuelva las incidencias con el modo Agente de GitHub Copilot.
1. Pruebe y compruebe el código refactorizado.
1. Confirme los cambios y cierre las incidencias.

### Importación del repositorio ContosoShopEasy

GitHub Importer le permite crear una copia de un repositorio existente en su propia cuenta de GitHub, lo que le proporciona control total sobre la copia importada. Aunque GitHub Importer no migra incidencias, solicitudes de incorporación de cambios o discusiones, el repositorio incluye un flujo de trabajo de Acciones de GitHub que automatiza la creación de incidencias en función del código base.

En esta tarea, importará el proyecto ContosoShopEasy y creará incidencias de GitHub que reflejan las vulnerabilidades de seguridad presentes en el código base.

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

    GitHub crea un nuevo repositorio en su cuenta con los archivos de proyecto de ContosoShopEasy.

    > **NOTA**: El proceso de importación puede tardar unos minutos en finalizar.

1. Espere a que finalice y abra el nuevo repositorio.

1. Vaya a la pestaña "Acciones" del repositorio y, a continuación, ejecute el flujo de trabajo de Acciones de GitHub**Create ContosoShopShopEasy Training Issues**.

1. Escriba "CREATE" para confirmar la creación de la incidencia.

    El flujo de trabajo creará incidencias en el repositorio para cada vulnerabilidad de seguridad identificada en el código base.

    Incidencias de prioridad crítica

    1. **Credenciales de administrador codificadas de forma rígida**  
        Quite el nombre de usuario y la contraseña del administrador codificado de forma rígida.

    1. **Almacenamiento de datos de tarjetas de crédito**  
        Corrija las infracciones de cumplimiento de PCI DSS.

    Incidencias de prioridad alta

    1. **Vulnerabilidad de inyección de código SQL**  
        Proteja la funcionalidad de búsqueda de productos.

    1. **Hash de contraseña no segura**  
        Reemplace MD5 por hash seguro.

    1. **Información confidencial en los registros**  
        Elimine contraseñas o tarjetas de la salida de depuración.

    1. **Omisión de validación de entrada**  
        Corrija la validación que detecta amenazas, pero las permite.

    Incidencias de prioridad media

    1. **Tokens de sesión predecibles**  
        Implemente tokens criptográficos seguros.

    1. **Validación de correo electrónico poco seguro**  
        Mejore la validación del formato de correo electrónico.

    1. **Requisitos de contraseña insuficientes**  
        Refuerce las reglas de complejidad de contraseñas.

    Incidencias de prioridad baja

    1. **Divulgación de información**  
         Reduzca los mensajes de error detallados y la salida de depuración.

### Revisión de las incidencias en GitHub

Las incidencias de GitHub sirven como un sistema de seguimiento centralizado para errores, vulnerabilidades de seguridad y solicitudes de mejora. Cada incidencia proporciona contexto sobre el problema, su gravedad y el posible impacto en la aplicación. Comprender estas incidencias antes de profundizar en el código ayuda a establecer prioridades y garantiza una corrección completa.

En esta tarea, revisará las incidencias abiertas del proyecto ContosoShopEasy y comprenderá las vulnerabilidades de seguridad que se deben solucionar.

Realice los pasos siguientes para completar esta tarea:

1. Vaya al repositorio ResolveGitHubIssues en GitHub.

1. Seleccione la pestaña**Incidencias** para ver todas las incidencias abiertas.

1. Revise cada descripción de las incidencias y tenga en cuenta que el flujo de trabajo ha creado 10 incidencias de seguridad específicas organizadas por prioridad:

    **Incidencias de prioridad crítica**: representan los riesgos de seguridad más graves que podrían comprometer por completo el sistema o llevar a infracciones normativas.

    **Incidencias de alta prioridad**: son vulnerabilidades de seguridad graves que podrían permitir el acceso no autorizado o infracciones de los datos.

    **Incidencias de prioridad media**: representan puntos débiles de seguridad que podrían aprovecharse, pero su impacto inmediato es menor.

    **Incidencias de prioridad baja**: se trata de mejoras de seguridad que reducen la pérdida de información y mejoran la posición general de seguridad.

1. Tenga en cuenta que cada incidencia incluye descripciones detalladas de la vulnerabilidad, la ubicación específica del código, ejemplos de código vulnerable, riesgos de seguridad y criterios de aceptación para las correcciones.

1. Revise la incidencia**ContosoShopShop Security Training - Issue Summary**, que proporciona información general sobre todas las vulnerabilidades y los objetivos de aprendizaje.

1. Tenga en cuenta que estas incidencias representan vulnerabilidades de seguridad comunes que se encuentran en aplicaciones reales y se alinean con las directrices de seguridad de OWASP.

### Clonación del repositorio y revisión del código base

Comprender la estructura y la funcionalidad de un código base existente es esencial antes de implementar correcciones de seguridad. La aplicación ContosoShopEasy sigue una arquitectura en capas típica de las aplicaciones empresariales, con una separación clara entre modelos, servicios, acceso a datos y componentes de seguridad. Revisar la estructura de código y ejecutar la aplicación ayuda a establecer una línea base para las pruebas después de implementar mejoras de seguridad.

En esta tarea, clonará el repositorio ContosoShopEasy, examinará la estructura del proyecto y observará el comportamiento actual de la aplicación.

Realice los pasos siguientes para completar esta tarea:

1. Clone el repositorio ResolveGitHubIssues en el entorno de desarrollo local.

    Abra una ventana de terminal y ejecute el comando siguiente y reemplace`your-username` por el nombre de usuario de GitHub:

    ```bash
    git clone https://github.com/your-username/ResolveGitHubIssues.git
    ```

1. Abra el repositorio clonado en Visual Studio Code.

    Vaya a la carpeta del repositorio y ábrala en Visual Studio Code. Asegúrese de que tiene instaladas y habilitadas las extensiones GitHub Copilot y GitHub Copilot Chat.

1. Examine la estructura del proyecto en el Explorador de soluciones.

    La aplicación ContosoShopEasy sigue una arquitectura en capas con los siguientes componentes:

    - **Models/**: Contiene modelos de datos para`Product.cs`,`User.cs`,`Order.cs` y`Category.cs`
    - **Services/**: Contiene lógica de negocios en`ProductService.cs`,`UserService.cs`,`PaymentService.cs` y`OrderService.cs`
    - **Data/**: Contiene repositorios de datos en`ProductRepository.cs`,`UserRepository.cs` y`OrderRepository.cs`
    - **Security/**: Contiene la lógica de validación de seguridad en`SecurityValidator.cs`
    - **Program.cs**: Punto de entrada principal de la aplicación con configuración de inserción de dependencias
    - **README.md**: Documentación que explica el propósito y las vulnerabilidades de la aplicación

1. Compile y ejecute la aplicación para observar su comportamiento actual.

    Ejecute los siguientes comandos en una ventana de terminal:

    ```bash
    cd ContosoShopEasy
    dotnet build
    dotnet run
    ```

    La aplicación mostrará una demostración completa de la funcionalidad de comercio electrónico, incluida una auditoría de seguridad que revela las vulnerabilidades intencionadas.

1. Revise la salida de la consola para identificar el registro relacionado con la seguridad.

    Observe que la aplicación registra información confidencial, como contraseñas, números de tarjeta de crédito, credenciales de administrador y detalles internos del sistema. Esta salida es una prueba clara de los problemas de seguridad que se deben solucionar.

1. Dedique un minuto a examinar el código asociado a cada vulnerabilidad de seguridad tal como se define en las incidencias de GitHub:

    - **Inyección de código SQL** (n.º 1): método`ProductService.cs` -`SearchProducts` (en torno a la línea 35)
    - **Hash de contraseña no segura** (n.º 2): método`UserService.cs` -`GetMd5Hash` (en torno a la línea 55)
    - **Datos confidenciales en los registros** (n.º 3): varios archivos: métodos de registro, inicio de sesión o pago de`UserService.cs``PaymentService.cs`.
    - **Credenciales de administrador codificadas de forma rígida** (n.º 4):`SecurityValidator.cs`constantes de credenciales de administrador (líneas 7-9)
    - **Almacenamiento de datos de tarjetas de crédito** (n.º 5):`Models/Order.cs`: propiedades CardNumber y CVV
    - **Omisión de validación de entrada** (n.º 6): método que siempre devuelve true`SecurityValidator.cs` -`ValidateInput`
    - **Tokens de sesión predecibles** (n.º 7): método`SecurityValidator.cs` -`GenerateSessionToken`
    - **Validación de correo electrónico poco seguro** (n.º 8): método`SecurityValidator.cs` -`ValidateEmail`
    - **Requisitos de contraseña insuficientes** (n.º 9): método`SecurityValidator.cs` -`ValidatePasswordStrength`
    - **Divulgación de información** (n.º 10): varias clases con el registro detallado de depuración y el método de auditoría de seguridad

### Análisis de las incidencias con el modo Preguntar de GitHub Copilot

El modo Preguntar de GitHub Copilot proporciona funcionalidades de análisis de código inteligentes que pueden ayudar a identificar vulnerabilidades de seguridad, comprender su posible impacto y sugerir estrategias de corrección. Al analizar sistemáticamente cada problema de seguridad, puede desarrollar una comprensión completa de los problemas antes de implementar correcciones. Este enfoque garantiza que las soluciones aborden las causas principales en lugar de solo los síntomas.

En esta tarea, usará el modo Preguntar de GitHub Copilot para analizar sistemáticamente las vulnerabilidades de seguridad, empezando por las incidencias más críticas y siguiendo hacia abajo en orden de prioridad.

Realice los pasos siguientes para completar esta tarea:

1. Abra la vista GitHub Copilot Chat y asegúrese de que el modo Preguntar esté seleccionado.

    Si la vista Chat aún no está abierta, seleccione el icono**Chat** situado en la parte superior de la ventana de Visual Studio Code. Compruebe que el modo de chat está establecido en**Preguntar** y use el modelo**GPT-4.1** para el análisis de seguridad complejo.

1. Comience con el análisis de vulnerabilidades de inyección de código SQL.

    Abra el archivo`ProductService.cs` y busque el método`SearchProducts`. Seleccione todo el método y agréguelo al contexto de chat mediante arrastrar y colocar, o bien haga clic con el botón derecho y seleccione**Agregar al chat**.

1. Pida a GitHub Copilot que analice la vulnerabilidad de inyección de código SQL.

    Envíe la indicación siguiente para analizar el problema de seguridad:

    ```text
    Analyze the SearchProducts method for security vulnerabilities. What makes this code susceptible to SQL injection attacks, and what are the potential consequences if an attacker exploits this vulnerability?
    ```

1. Revise el análisis de GitHub Copilot y solicite instrucciones de corrección específicas.

    Después de revisar el análisis inicial, solicite correcciones específicas:

    ```text
    How can I modify this method to prevent SQL injection attacks? What secure coding practices should I implement to safely handle user input in database queries?
    ```

1. Analice la vulnerabilidad de hash de contraseña no segura.

    Abra el archivo`UserService.cs` y busque el método`GetMd5Hash`. Agregue este método al contexto chat y envíe la indicación siguiente:

    ```text
    Why is MD5 hashing unsuitable for password storage? What are the security risks of using MD5 for passwords, and what stronger alternatives should I use instead?
    ```

1. Pida instrucciones específicas sobre la implementación de hash de contraseñas seguras.

    ```text
    Show me how to implement secure password hashing using bcrypt or PBKDF2. What additional security measures should I implement for password handling?
    ```

1. Analice las incidencias de registro de datos confidenciales (incidencia n.º 3).

    Abra los archivos`PaymentService.cs` y`UserService.cs` y busque métodos que registren información confidencial. Agregue métodos pertinentes al contexto de chat y pregunte:

    ```text
    What sensitive information is being logged in the payment processing and user registration methods? Why is logging passwords, credit card numbers, and CVV codes a security risk?
    ```

1. Examine la vulnerabilidad de credenciales codificadas de forma rígida (incidencia n.º 4).

    Abra el archivo`SecurityValidator.cs` y busque las constantes de credenciales de administrador en torno a las líneas 7-9. Agregue el código pertinente al contexto de chat y pregunte lo siguiente:

    ```text
    What security risks are created by hardcoding admin credentials in source code? How should application credentials be managed securely in production environments?
    ```

1. Analice las incidencias de almacenamiento de datos de tarjetas de crédito (incidencia n.º 5).

    Abra el archivo`Models/Order.cs` y examine las propiedades CardNumber y CVV. Agregue este código al contexto de chat y pregunte:

    ```text
    Why is storing full credit card numbers and CVV codes a PCI DSS compliance violation? What are the proper ways to handle payment card data securely?
    ```

1. Revise la omisión de validación de entrada (incidencia n.º 6).

    Céntrese en el método`ValidateInput` en`SecurityValidator.cs` que siempre devuelve true a pesar de detectar amenazas. Preguntar:

    ```text
    What makes this input validation method ineffective? Why does it detect dangerous input but still return true, and how should proper input validation work?
    ```

1. Examine la generación de tokens de sesión predecibles (incidencia n.º 7).

    Céntrese en el método`GenerateSessionToken` de`SecurityValidator.cs` y pregunte lo siguiente:

    ```text
    Why are predictable session tokens based on username and timestamp a security risk? How should secure, unpredictable session tokens be generated?
    ```

1. Analice la validación de correo electrónico poco seguro (incidencia n.º 8).

    Revise el método`ValidateEmail` en`SecurityValidator.cs` que solo comprueba los caracteres "@" and "". Preguntar:

    ```text
    What makes this email validation insufficient? What are the security risks of weak email validation, and how should proper email validation be implemented?
    ```

1. Revise los requisitos de contraseña insuficientes (incidencia n.º 9).

    Examine el método`ValidatePasswordStrength` en`SecurityValidator.cs` que solo requiere 4 caracteres. Preguntar:

    ```text
    Why are these password requirements insufficient for security? What are proper password complexity requirements, and how should password strength be validated?
    ```

1. Analice las incidencias de divulgación de información (incidencia n.º 10).

    Seleccione el método`RunSecurityAudit` y otro registro de depuración en distintos archivos y pregunte:

    ```text
    How does the security audit method and excessive debug logging create information disclosure vulnerabilities? What information should never be exposed in logs or error messages?
    ```

1. Documente los resultados del análisis como referencia durante la fase de corrección.

    Tome notas sobre las recomendaciones de GitHub Copilot para cada categoría de vulnerabilidad. Esta documentación guiará la implementación de las correcciones de seguridad en la siguiente tarea.

### Resolución de incidencias con el modo Agente de GitHub Copilot

El modo Agente de GitHub Copilot permite la implementación autónoma de correcciones de seguridad complejas en varios archivos y métodos. A diferencia del modo Preguntar, que proporciona análisis y recomendaciones, el modo Agente puede modificar directamente el código para implementar mejoras de seguridad. Este enfoque es especialmente eficaz para la corrección sistemática de la seguridad, donde es necesario abordar de forma coherente varias vulnerabilidades relacionadas.

> **NOTA**: Para ahorrar tiempo durante este ejercicio de laboratorio, resolverá y probará una colección de incidencias e insertará actualizaciones en una sola confirmación. El procesamiento por lotes de incidencias de esta forma no es un procedimiento recomendado. Microsoft y GitHub recomiendan resolver cada incidencia de forma individual con distintas confirmaciones en lugar de procesarlas por lotes. La resolución de incidencias de forma individual proporciona una mejor rastreabilidad, revisiones de código más sencillas y opciones de reversión más seguras si surgen problemas. Cada corrección debe probarse exhaustivamente antes de pasar a la siguiente incidencia para asegurarse de que los cambios no introducen regresiones.

En esta tarea, usará el modo Agente de GitHub Copilot para implementar correcciones de seguridad completas para todas las vulnerabilidades identificadas en la aplicación ContosoShopEasy.

Realice los pasos siguientes para completar esta tarea:

1. Cambie GitHub Copilot Chat al modo Agente.

    En la vista Chat, localice el selector de modos y cambie de**Preguntar** a**Agente**. El modo Agente permite a GitHub Copilot realizar modificaciones directas de código en función de las instrucciones.

1. Solucione primero la vulnerabilidad de inyección de código SQL.

    Abra el archivo`ProductService.cs` y busque el método`SearchProducts`. Use la indicación siguiente para dar instrucciones al agente:

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
