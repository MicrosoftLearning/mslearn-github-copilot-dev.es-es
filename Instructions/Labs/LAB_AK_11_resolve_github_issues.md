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

Las importaciones de repositorios de GitHub permiten crear una copia de un repositorio existente en una cuenta propia de GitHub. Este proceso conserva el historial del repositorio original al tiempo que le proporciona control total sobre la copia importada. En esta tarea, importará el proyecto ContosoShopEasy y creará incidencias de GitHub que reflejan las vulnerabilidades de seguridad presentes en el código base.

Realice los pasos siguientes para completar esta tarea:

1. Abra una ventana del explorador y vaya a GitHub.com.

1. Inicie sesión en su cuenta de GitHub.

1. Cree un repositorio denominado**ContosoShopEasy**.

    Para crear un repositorio, seleccione el icono**+** en la esquina superior derecha de GitHub y, después, seleccione**Nuevo repositorio**.

1. Copie los archivos del proyecto ContosoShopEasy del entorno de laboratorio local en el nuevo repositorio.

    Puede cargar archivos directamente desde la interfaz web de GitHub o clonar el repositorio vacío e insertar los archivos de ContosoShopEasy desde la máquina local.

1. Cree las siguientes incidencias de GitHub para realizar el seguimiento de las vulnerabilidades de seguridad:

    - **Vulnerabilidad de inyección de código SQL**: La funcionalidad de búsqueda de productos acepta entradas no autorizadas y es vulnerable a ataques por inyección. El método`SearchProducts` de`ProductService.cs` incorpora directamente la entrada del usuario en consultas SQL simuladas sin la parametrización adecuada.

    - **Hash de contraseñas no seguras**: La aplicación usa hash MD5 para el almacenamiento de contraseñas, que es criptográficamente no seguro. El método`GetMd5Hash` de`UserService.cs` implementa este enfoque de hash vulnerable.

    - **Exposición de datos sensibles**: Los números de tarjeta de crédito completos, los códigos CVV y las contraseñas se registran en texto no cifrado. El método`ProcessPayment` de`PaymentService.cs` y los métodos de registro e inicio de sesión de`UserService.cs` exponen información confidencial.

    - **Credenciales de administrador codificadas de forma rígida**: El nombre de usuario de administrador y la contraseña se codifican de forma rígida en la clase`SecurityValidator.cs`, lo que hace que sean accesibles para cualquiera con acceso al código fuente.

    - **Incidencias de validación de entrada**: La aplicación acepta caracteres potencialmente peligrosos sin un saneamiento correcto. El`ValidateInput` método de`SecurityValidator.cs` registra advertencias, pero sigue aceptando entradas malintencionadas.

    - **Divulgación de información**: El registro de depuración expone información confidencial del sistema y detalles de configuración. En varias clases de la aplicación se registran datos confidenciales con fines de depuración.

    - **Tokens de sesión predecibles**: Los tokens de sesión siguen patrones predecibles basados en el nombre de usuario y la marca de tiempo. El método`GenerateSessionToken` de`SecurityValidator.cs` crea tokens que se pueden adivinar fácilmente.

    - **Problemas de seguridad en la carga de archivos**: La aplicación acepta tipos de archivo peligrosos sin una validación adecuada. El método`ValidateFileUpload` de`SecurityValidator.cs` proporciona una protección insuficiente frente a cargas malintencionadas.

### Revisión de las incidencias en GitHub

Las incidencias de GitHub sirven como un sistema de seguimiento centralizado para errores, vulnerabilidades de seguridad y solicitudes de mejora. Cada incidencia proporciona contexto sobre el problema, su gravedad y el posible impacto en la aplicación. Comprender estas incidencias antes de profundizar en el código ayuda a establecer prioridades y garantiza una corrección completa.

En esta tarea, revisará las incidencias abiertas del proyecto ContosoShopEasy y comprenderá las vulnerabilidades de seguridad que se deben solucionar.

Realice los pasos siguientes para completar esta tarea:

1. Vaya al repositorio ContosoShopEasy en GitHub.

1. Seleccione la pestaña**Incidencias** para ver todas las incidencias abiertas.

1. Revise la descripción de cada incidencia y anote de las siguientes categorías de vulnerabilidades de seguridad:

    **Vulnerabilidades por inyección SQL**: Funcionalidad de búsqueda de productos que incorpora directamente la entrada del usuario en las consultas de base de datos, lo que crea oportunidades para ataques malintencionados por inyección de código SQL.

    **Procedimientos criptográficos no seguros**: Uso del hash MD5 para el almacenamiento de contraseñas, que se considera criptográficamente débil y que no es adecuado para la seguridad de las contraseñas.

    **Exposición de datos sensibles**: Registro de números completos de tarjetas de crédito, códigos CVV, contraseñas y otra información confidencial que nunca se debe almacenar o registrar en texto no cifrado.

    **Credenciales codificadas de forma rígida**: Los nombres de usuario de administrador y las contraseñas se insertan directamente en el código fuente, lo que hace que sean accesibles para cualquiera con acceso al repositorio.

    **Errores de validación de entrada**: Validación y saneamiento de la entrada del usuario insuficientes, lo que permite que la aplicación procese contenido potencialmente malintencionado.

    **Divulgación de información**: Registro de depuración que expone la configuración confidencial del sistema, los procesos internos y los datos de usuario.

    **Administración no segura de las sesiones**: Generación de tokens de sesión predecibles que podrían permitir a los atacantes secuestrar sesiones de usuario.

    **Vulnerabilidades de carga de archivos**: Validación inadecuada de los archivos cargados, lo que podría permitir la ejecución de código malintencionado.

1. Tenga en cuenta que estas incidencias representan vulnerabilidades de seguridad comunes que se encuentran en aplicaciones reales y se alinean con las directrices de seguridad de OWASP.

### Clonación del repositorio y revisión del código base

Comprender la estructura y la funcionalidad de un código base existente es esencial antes de implementar correcciones de seguridad. La aplicación ContosoShopEasy sigue una arquitectura en capas típica de las aplicaciones empresariales, con una separación clara entre modelos, servicios, acceso a datos y componentes de seguridad. Revisar la estructura de código y ejecutar la aplicación ayuda a establecer una línea base para las pruebas después de implementar mejoras de seguridad.

En esta tarea, clonará el repositorio ContosoShopEasy, examinará la estructura del proyecto y observará el comportamiento actual de la aplicación.

Realice los pasos siguientes para completar esta tarea:

1. Clone el repositorio ContosoShopEasy en el entorno de desarrollo local.

    Abra una ventana de terminal y ejecute el comando siguiente y reemplace`your-username` por el nombre de usuario de GitHub:

    ```bash
    git clone https://github.com/your-username/ContosoShopEasy.git
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

1. Identifique los archivos y métodos específicos asociados a cada vulnerabilidad de seguridad:

    - **Inyección de código SQL**: método`ProductService.cs` -`SearchProducts`
    - **Hash de contraseñas no seguras**: método`UserService.cs` -`GetMd5Hash`
    - **Exposición de datos confidenciales**: método`PaymentService.cs` -`ProcessPayment` y`UserService.cs`: métodos de registro o inicio de sesión
    - **Credenciales codificadas de forma rígida**:`SecurityValidator.cs`: constantes de credenciales de administrador
    - **Validación de la entrada**: método`SecurityValidator.cs` -`ValidateInput`
    - **Divulgación de información**: Varias clases con registro de depuración
    - **Tokens predecibles**: método`SecurityValidator.cs` -`GenerateSessionToken`
    - **Problemas de carga de archivos**: método`SecurityValidator.cs` -`ValidateFileUpload`

### Análisis de las incidencias con el modo Preguntar de GitHub Copilot

El modo Preguntar de GitHub Copilot proporciona funcionalidades de análisis de código inteligentes que pueden ayudar a identificar vulnerabilidades de seguridad, comprender su posible impacto y sugerir estrategias de corrección. Al analizar sistemáticamente cada problema de seguridad, puede desarrollar una comprensión completa de los problemas antes de implementar correcciones. Este enfoque garantiza que las soluciones aborden las causas principales en lugar de solo los síntomas.

En esta tarea, usará el modo Preguntar de GitHub Copilot para analizar sistemáticamente cada vulnerabilidad de seguridad en la aplicación ContosoShopEasy.

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

1. Analice los problemas de exposición de datos confidenciales.

    Abra el archivo`PaymentService.cs` y busque el método`ProcessPayment`. Agréguelo al contexto de chat y pregunte lo siguiente:

    ```text
    What sensitive information is being logged in this payment processing method? Why is logging full credit card numbers and CVV codes a security risk, and how should payment data be handled securely?
    ```

1. Examine la vulnerabilidad de credenciales codificadas de forma rígida.

    Abra el archivo`SecurityValidator.cs` y busque las constantes de credenciales de administrador. Agregue el código pertinente al contexto de chat y pregunte lo siguiente:

    ```text
    What security risks are created by hardcoding admin credentials in source code? How should application credentials be managed securely in production environments?
    ```

1. Analice los puntos débiles de validación de entrada.

    Céntrese en el método`ValidateInput` de`SecurityValidator.cs` y pregunte lo siguiente:

    ```text
    What makes this input validation method ineffective against malicious input? How can I implement proper input sanitization to prevent XSS and other injection attacks?
    ```

1. Revise los problemas de divulgación de información.

    Seleccione varios métodos que contengan el registro de depuración en distintos archivos y pregunte lo siguiente:

    ```text
    How does excessive debug logging create security vulnerabilities? What information should never be logged, and how can I implement secure logging practices?
    ```

1. Examine la generación de tokens predecibles.

    Céntrese en el método`GenerateSessionToken` y pregunte lo siguiente:

    ```text
    Why are predictable session tokens a security risk? How should secure, unpredictable session tokens be generated to prevent session hijacking attacks?
    ```

1. Analice los problemas de validación de carga de archivos.

    Revise el método`ValidateFileUpload` y pregunte lo siguiente:

    ```text
    What makes this file upload validation insufficient for security? How can I implement comprehensive file upload security to prevent malicious file execution?
    ```

1. Documente los resultados del análisis como referencia durante la fase de corrección.

    Tome notas sobre las recomendaciones de GitHub Copilot para cada categoría de vulnerabilidad. Esta documentación guiará la implementación de las correcciones de seguridad en la siguiente tarea.

### Resolución de incidencias con el modo Agente de GitHub Copilot

El modo Agente de GitHub Copilot permite la implementación autónoma de correcciones de seguridad complejas en varios archivos y métodos. A diferencia del modo Preguntar, que proporciona análisis y recomendaciones, el modo Agente puede modificar directamente el código para implementar mejoras de seguridad. Este enfoque es especialmente eficaz para la corrección sistemática de la seguridad, donde es necesario abordar de forma coherente varias vulnerabilidades relacionadas.

En esta tarea, usará el modo Agente de GitHub Copilot para implementar correcciones de seguridad completas para todas las vulnerabilidades identificadas en la aplicación ContosoShopEasy.

Realice los pasos siguientes para completar esta tarea:

1. Cambie GitHub Copilot Chat al modo Agente.

    En la vista Chat, localice el selector de modos y cambie de**Preguntar** a**Agente**. El modo Agente permite a GitHub Copilot realizar modificaciones directas de código en función de las instrucciones.

1. Solucione primero la vulnerabilidad de inyección de código SQL.

    Abra el archivo`ProductService.cs` y busque el método`SearchProducts`. Use la indicación siguiente para dar instrucciones al agente:

    ```text
    Fix the SQL injection vulnerability in the SearchProducts method. Remove the simulated SQL query logging that demonstrates the vulnerability, and implement proper input sanitization to safely handle search terms. Ensure the method still functions correctly for legitimate searches while preventing malicious input.
    ```

1. Supervise el progreso del agente y revise los cambios propuestos.

    El agente modificará el código para quitar el registro vulnerable e implementará un control de entrada más seguro. Revise los cambios para asegurarse de que mantienen la funcionalidad al tiempo que aborda el problema de seguridad.

1. Implemente el hash de contraseñas seguras.

    Céntrese en el archivo`UserService.cs` y use la indicación siguiente:

    ```text
    Replace the MD5 password hashing with bcrypt or PBKDF2. Update the GetMd5Hash method to use a cryptographically secure hashing algorithm with proper salt generation. Ensure compatibility with existing user authentication while improving security.
    ```

1. Revise y pruebe los cambios de hash de contraseña.

    El agente implementará un hash de contraseña más seguro. A fin de probar los cambios, ejecute la aplicación para asegurarse de que el registro de usuario y el inicio de sesión siguen funcionando correctamente.

1. Aborde la exposición de datos confidenciales en el procesamiento de pagos.

    Abra el archivo e`PaymentService.cs` indique lo siguiente al agente:

    ```text
    Fix sensitive data logging in the ProcessPayment method. Remove logging of full credit card numbers, CVV codes, and other sensitive payment information. Implement secure logging that masks sensitive data while maintaining useful operational information.
    ```

1. Quite las credenciales de administrador codificadas de forma rígida.

    Céntrese en el archivo`SecurityValidator.cs` y use esta indicación:

    ```text
    Remove hardcoded admin credentials and replace them with a secure configuration approach. Implement environment variable or configuration file-based credential management while maintaining the functionality for educational demonstration purposes.
    ```

1. Implemente la validación de entrada.

    Indique al agente que corrija las vulnerabilidades de validación de entrada:

    ```text
    Strengthen the ValidateInput method to properly sanitize user input and prevent XSS attacks. Implement comprehensive input validation that rejects malicious content while allowing legitimate user input. Ensure the method returns false for truly dangerous input.
    ```

1. Reduzca la divulgación de información a través del registro.

    Solucione los problemas de registro de depuración en varios archivos:

    ```text
    Review all console logging throughout the application and remove or mask sensitive information. Implement secure logging practices that provide useful debugging information without exposing passwords, credit card data, or system internals.
    ```

1. Implemente la generación de tokens de sesión seguros.

    Céntrese en la vulnerabilidad de los tokens de sesión:

    ```text
    Replace the predictable session token generation with a cryptographically secure random token generator. Ensure tokens are unpredictable and sufficiently long to prevent brute force attacks.
    ```

1. Refuerce la validación de la carga de archivos.

    Solucione los problemas de seguridad de carga de archivos:

    ```text
    Implement comprehensive file upload validation that checks file types, sizes, and content. Reject dangerous file types and implement proper security controls to prevent malicious file uploads.
    ```

1. Pruebe la aplicación después de cada cambio importante.

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

1. Pruebe la corrección de inyección de código SQL mediante el examen de la funcionalidad de búsqueda de productos.

    Compruebe que el método`SearchProducts` ya no registra consultas SQL vulnerables y que la funcionalidad de búsqueda sigue funcionando correctamente con términos de búsqueda legítimos.

1. Compruebe las mejoras de seguridad de contraseñas.

    Compruebe que los procesos de registro e inicio de sesión del usuario ya no registran contraseñas en texto no cifrado y que se implementa el hash de contraseña más seguro. La aplicación debe seguir autenticando a los usuarios correctamente.

1. Confirme las mejoras de seguridad de procesamiento de pagos.

    Asegúrese de que el procesamiento de pagos ya no registra números completos de tarjetas de crédito o códigos CVV, a la vez que mantiene la capacidad de procesar los pagos correctamente.

1. Valide la seguridad de las credenciales de administrador.

    Compruebe que las credenciales de administrador codificadas de forma rígida ya no se muestran en registros o auditorías de seguridad, mientras que la funcionalidad de administrador sigue siendo accesible a través de medios seguros.

1. Pruebe las mejoras de validación de entrada.

    Confirme que la validación de entrada mejorada controla correctamente la entrada legítima y potencialmente malintencionada sin interrumpir las interacciones normales del usuario.

1. Compruebe las correcciones de divulgación de información.

    Revise la salida de la consola para asegurarse de que la información confidencial del sistema, los detalles de configuración y los datos de usuario ya no se exponen a través del registro de depuración.

1. Compruebe la seguridad de los tokens de sesión.

    Si los tokens de sesión se generan durante la ejecución de la aplicación, confirme que sean aleatorios e impredecibles en lugar de seguir el enfoque basado en patrones anterior.

1. Valide las mejoras de seguridad de carga de archivos.

    Pruebe las mejoras de validación de la carga de archivos para asegurarse de que los tipos de archivo peligrosos se rechazan correctamente mientras se aceptan los archivos legítimos.

1. Compare la salida de auditoría de seguridad con la versión original.

    Ejecute la característica de auditoría de seguridad y compare los resultados con las observaciones iniciales. La auditoría debe mostrar una posición de seguridad mejorada al tiempo que mantiene el valor educativo.

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

1. Confirme los cambios con mensajes descriptivos que hagan referencia a las incidencias de GitHub.

    Use mensajes de confirmación que describan claramente las correcciones de seguridad y hagan referencia a números de incidencia:

    ```bash
    git commit -m "Fix SQL injection vulnerability in ProductService SearchProducts method

    - Remove vulnerable SQL query logging
    - Implement proper input sanitization
    - Maintain search functionality while preventing injection attacks

    Fixes #1"
    ```

1. Realice confirmaciones adicionales para cada categoría de corrección de seguridad principal.

    Confirme las mejoras en el hash de contraseñas:

    ```bash
    git commit -m "Replace MD5 with secure password hashing

    - Implement bcrypt/PBKDF2 for password storage
    - Add proper salt generation
    - Maintain authentication compatibility

    Fixes #2"
    ```

1. Continúe con confirmaciones para las correcciones de seguridad restantes:

    ```bash
    git commit -m "Remove sensitive data from payment processing logs

    - Mask credit card numbers in logging
    - Remove CVV code exposure
    - Maintain operational logging capabilities

    Fixes #3"

    git commit -m "Remove hardcoded admin credentials

    - Implement secure credential management
    - Use environment variables for sensitive config
    - Maintain admin functionality for demo purposes

    Fixes #4"

    git commit -m "Strengthen input validation and prevent XSS

    - Implement comprehensive input sanitization
    - Reject malicious content properly
    - Maintain user experience for legitimate input

    Fixes #5"

    git commit -m "Reduce information disclosure in debug logging

    - Remove sensitive data from console output
    - Implement secure logging practices
    - Maintain useful debugging information

    Fixes #6"

    git commit -m "Implement secure session token generation

    - Replace predictable tokens with cryptographically secure random generation
    - Increase token entropy to prevent brute force attacks

    Fixes #7"

    git commit -m "Enhance file upload security validation

    - Implement comprehensive file type checking
    - Add file size and content validation
    - Reject dangerous file types effectively

    Fixes #8"
    ```

1. Inserte los cambios en el repositorio de GitHub.

    ```bash
    git push origin main
    ```

1. Compruebe que las incidencias de GitHub se cierran automáticamente.

    Vaya al repositorio en GitHub y compruebe que las incidencias están marcadas como cerradas debido a los mensajes de confirmación con los que se les hace referencia.

1. Revise el historial de confirmaciones para asegurarse de que todas las correcciones de seguridad están documentadas correctamente.

    Compruebe que los mensajes de confirmación describen claramente las mejoras de seguridad y proporcionan una buena pista de auditoría para futuras referencias.

