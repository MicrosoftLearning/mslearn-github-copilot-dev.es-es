---
lab:
  title: "Ejercicio: Consolidación del código duplicado mediante GitHub\_Copilot"
  description: "Obtenga información sobre cómo analizar un código base complejo y consolidar la lógica de código duplicada mediante herramientas de GitHub\_Copilot."
---

# Consolidación del código duplicado mediante GitHub Copilot

La lógica de código duplicado se suele introducir al desarrollar o extender un código base que incluye características similares o relacionadas. Es posible que no sea intencionada y puede ser tan simple como reutilizar código para crear prototipos de una nueva característica. Si la lógica duplicada evoluciona para que coincida con el código circundante a lo largo del tiempo, el problema puede resultar más complicado. Los cambios realizados en nombres de variable, nombres de función y estructuras de código en una ubicación (pero no en la otra) pueden enmascarar la lógica duplicada. Una programación apresurada, una documentación deficiente y una falta de revisiones de código adecuadas puede empeorar el problema. Al final, la lógica duplicada dificulta la lectura, mantenimiento, depuración y prueba del código.

En este ejercicio, revisará un proyecto existente que contiene lógica de código duplicada, analizará las opciones de consolidación, consolidará la lógica de código duplicado y probará el código refactorizado para asegurarse de que funciona según lo previsto. Usará GitHub Copilot en el modo Preguntar para comprender un proyecto de código existente y explorar las opciones para refactorizar la lógica. Use GitHub Copilot en modo agente para refactorizar el código mediante la combinación de lógica duplicada en métodos auxiliares compartidos. Pruebe el código original y refactorizado para asegurarse de que la lógica consolidada funciona según lo previsto.

Este ejercicio debería tardar en completarse **30** minutos aproximadamente.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar una cuenta de GitHub y una suscripción de GitHub Copilot propias. Si no tiene una cuenta de GitHub, puede <a href="https://github.com/" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

## Antes de comenzar

El entorno de laboratorio debe incluir lo siguiente: Git 2.48 o posterior, SDK de .NET 9.0 o posterior, Visual Studio Code con la extensión Kit de desarrollo de C# y acceso a una cuenta de GitHub con GitHub Copilot habilitado.

### Configuración del entorno de laboratorio

Si usa un equipo local como entorno de laboratorio para este ejercicio:

- Para obtener ayuda a fin de configurar el equipo local como entorno de laboratorio, abra el siguiente vínculo en un explorador: <a href="https://go.microsoft.com/fwlink/?linkid=2320147" target="_blank">Configure los recursos de entorno de laboratorio</a>.

- Para obtener ayuda a fin de habilitar la suscripción de GitHub Copilot en Visual Studio Code, abra el siguiente vínculo en un explorador: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

Si usa un entorno de laboratorio hospedado para este ejercicio:

- Para obtener ayuda a fin de habilitar la suscripción de GitHub Copilot en Visual Studio Code, pegue la siguiente dirección URL en la barra de navegación del sitio de un explorador: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

- Para asegurarse de que el SDK de .NET está configurado para usar el repositorio oficial de NuGet.org como origen para descargar y restaurar paquetes:

    Abra un terminal de comandos y luego ejecute los siguientes comandos:

    ```bash

    dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org

    ```

### Descarga del proyecto de código de ejemplo

Siga estos pasos para descargar el proyecto de ejemplo y abrirlo en Visual Studio Code:

1. Abra una ventana del explorador en el entorno de laboratorio.

1. Para descargar un archivo ZIP que contenga el proyecto de aplicación de ejemplo, abra la URL siguiente en el explorador: [Laboratorio de GitHub Copilot: consolidar el código duplicado](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/GHCopilotEx7LabApps.zip)

    El archivo ZIP se denomina **GHCopilotEx7LabApps.zip**.

1. Extraiga los archivos del archivo **GHCopilotEx7LabApps.zip**.

    Por ejemplo:

    1. Vaya a la carpeta de descargas del entorno de laboratorio.

    1. Haga clic con el botón derecho en *GHCopilotEx7LabApps.zip* y, después seleccione **Extraer todo**.

    1. Seleccione **Mostrar los archivos extraídos al completar** y, a continuación, **Extraer**.

1. Copia la carpeta **GHCopilotEx7LabApps** en una ubicación que sea fácil de acceder, como la carpeta Escritorio de Windows.

1. Abra la carpeta **GHCopilotEx7LabApps** en Visual Studio Code.

    Por ejemplo:

    1. Abra Visual Studio Code en el entorno de laboratorio.

    1. En Visual Studio Code, en el menú **Archivo**, seleccione **Abrir archivo**.

    1. Vaya a la carpeta Escritorio de Windows, seleccione **GHCopilotEx7LabApps** y luego **Seleccionar carpeta**.

1. En la vista EXPLORADOR DE SOLUCIONES de Visual Studio Code, compruebe la siguiente estructura del proyecto:

    - GHCopilotEx7LabApps\
        - ECommerceOrderAndReturn\
            - Dependencies\
            - Configuration\
                - AppConfig.cs
            - Models\
                - Order.cs
                - Return.cs
            - Security\
                - SecurityValidator.cs
            - Services\
                - AuditService.cs
                - EmailService.cs
                - InventoryService.cs
            - EXPECTED_OUTPUT.md
            - OrderProcessor.cs
            - Program.cs
            - README.md
            - ReturnProcessor.cs

## Escenario del ejercicio

Es desarrollador de software y trabaja para una empresa de consultoría. Los clientes necesitan ayudar a consolidar la lógica de código duplicada. El objetivo es mejorar la capacidad de mantenimiento del código a la vez que se conserva la funcionalidad existente. Se le asigna a la aplicación siguiente:

- E-CommerceOrdersAndReturns: Se trata de una aplicación de comercio electrónico que procesa los pedidos de los clientes y controla los resultados del producto. Incluye la lógica empresarial básica para validar pedidos y devoluciones, calcular los gastos de envío, enviar notificaciones por correo electrónico, registrar actividades de auditoría y gestionar los niveles de inventario.

Este ejercicio incluye las siguientes tareas:

1. Revise los pedidos de comercio electrónico y devuelva el código base manualmente.
1. Identifique el código duplicado mediante el GitHub Copilot Chat (modo Preguntar).
1. Consolide la lógica duplicada utilizando GitHub Copilot Chat (modo Agente).
1. Pruebe los pedidos de comercio electrónico refactorizado y devuelva código.

### Revise los pedidos de comercio electrónico y devuelva el código base manualmente.

El primer paso de cualquier esfuerzo de refactorización es asegurarse de que comprende el código base existente. Es importante comprender la estructura del código, la lógica de negocios y los resultados generados cuando se ejecuta el código.

En esta tarea, revisará los componentes principales del proyecto de procesamiento de pedidos de comercio electrónico y devolverá el código, analizará el código para ver patrones de código duplicados y probará el código.

Realice los pasos siguientes para completar esta tarea:

1. Dedique un minuto a revisar la estructura del proyecto ECommerceOrderAndReturn.

    El código base sigue una arquitectura superpuesta típica de las aplicaciones empresariales. Las principales capas arquitectónicas incluyen: Modelos, configuración, seguridad, servicios y procesamiento.

1. Examine las clases de procesamiento principales.

    Abra **OrderProcessor.cs** y **ReturnProcessor.cs** en paralelo. Estas clases representan la lógica empresarial principal para procesar pedidos de clientes y devoluciones de productos, respectivamente.

    Observe que las dos clases tienen firmas de método similares y patrones de procesamiento. Este es el tipo más obvio de duplicación, pero hay duplicaciones adicionales y más sutiles en todo el código base.

1. Revise la capa Servicios.

    Vaya a la carpeta **Servicios** y examine **EmailService.cs**, **AuditService.cs** e **InventoryService.cs**.

    Es posible que observe que estos servicios implementan patrones similares para controlar las notificaciones por correo electrónico, el registro de auditoría y la administración del inventario. Cada servicio tiene métodos que siguen estructuras similares, pero se duplican para distintos procesos empresariales (pedidos frente a devoluciones).

1. Ejecute la aplicación y revise el resultado de la consola.

    > **NOTA**: Se almacena una copia del resultado de la consola en el archivo EXPECTED_OUTPUT.md incluido en el directorio del proyecto. Usará este archivo para comprobar que el comportamiento de la aplicación no ha cambiado después de consolidar el código duplicado.

    Puede ejecutar la aplicación desde la vista EXPLORADOR DE SOLUCIONES haciendo clic con el botón derecho en **ECommerceOrdersAndReturns**, seleccionando **Depurar** y, a continuación, seleccionando **Iniciar nueva instancia**.

    El resultado de la consola incluye:

    - Niveles de inventario iniciales
    - Procesamiento de pedidos con validación, cálculo del envío, procesamiento de pagos, reserva de inventario, notificaciones por correo electrónico y registro de auditoría
    - Devolver el procesamiento con pasos similares, pero adaptados para devoluciones
    - Niveles de inventario actualizados
    - Pruebas de validación de seguridad con varias entradas no válidas

    La aplicación ejecuta 5 escenarios de prueba para demostrar errores de validación de seguridad y procesamiento correctos.

1. Dedique un minuto a clasificar los patrones de código duplicados que haya observado.

    Por ejemplo:

    **Métodos duplicados**: OrderProcessor y ReturnProcessor tienen métodos idénticos `Validate()` y similares `CalculateShipping()`.

    **Patrones similares en la capa de servicio**: Cada servicio tiene métodos que siguen patrones similares, pero que se duplican para diferentes procesos empresariales (pedidos frente a devoluciones).

Es importante comprender la funcionalidad existente antes de realizar cambios. Al ejecutar el código y revisar la salida, establece una línea base que puede usar para comprobar que la refactorización no interrumpe la funcionalidad existente.

### Identifique el código duplicado mediante el GitHub Copilot Chat (modo Preguntar).

El modo Preguntar de GitHub Copilot Chat es una herramienta excelente para analizar bases de código complejas e identificar patrones de duplicación sutiles que podrían no ser evidentes a simple vista. En el modo Peguntar, Copilot actúa como revisor de código inteligente que puede analizar varios archivos simultáneamente e identificar duplicaciones obvias y ocultas (lógica de código).

En esta tarea, usará GitHub Copilot para identificar sistemáticamente los distintos tipos de patrones de código duplicados en la aplicación de comercio electrónico.

Realice los pasos siguientes para completar esta tarea:

1. Abra la vista Chat de GitHub Copilot y, después, configure el modo Preguntar y el modelo GPT-4.1.

    Si la vista Chat aún no está abierta, seleccione el icono **Chat** situado en la parte superior de la ventana de Visual Studio Code. Asegúrese de que el modo de chat está establecido en **Preguntar** y use el modelo **GPT-4.1**.

    El modelo GPT-4.1 está disponible con el plan gratuito de GitHub Copilot, está diseñado para controlar tareas complejas y proporciona sugerencias o análisis de código inteligentes.

1. Cierre los archivos que estén abiertos en el editor.

    GitHub Copilot usa archivos que se abren en el editor para establecer el contexto. Cerrar pestañas de archivos no deseados ayuda a reducir el ruido en el análisis.

1. Agregue los archivos OrderProcessor y ReturnProcessor al contexto Chat.

    Use la operación de arrastrar y soltar para añadir los archivos **OrderProcessor.cs** y **ReturnProcessor.cs** desde el EXPLORADOR DE SOLUCIONES al contexto Chat.

    Al añadir un archivo al contexto Chat, se le indica a GitHub Copilot que incluya ese archivo en el contexto al analizar la solicitud.

    Si usa la vista de carpetas predeterminada en lugar del EXPLORADOR DE SOLUCIONES, puede hacer clic con el botón derecho en un archivo y luego seleccionar **Agregar archivo al chat**. También puede abrir un archivo en el editor de código para ayudar a establecer el contexto.

1. Pida a GitHub Copilot que identifique patrones de código duplicados en los archivos seleccionados.

    Por ejemplo, envíe el siguiente mensaje para analizar la duplicación principal:

    ```text
    What duplicate code exists between OrderProcessor.cs and ReturnProcessor.cs? Identify specific methods and logic that are duplicated between these classes. Describe opportunities to consolidate duplicate code.
    ```

1. Dedique un minuto a revisar las respuestas de GitHub Copilot.

    GitHub Copilot debería identificar la duplicación del método `Validate()` y los patrones similares en los métodos `CalculateShipping()`. También puede tener en cuenta patrones similares en relación con el registro de auditoría, el control de errores y el procesamiento de pagos o reembolsos.

1. Actualice el contexto de chat para especificar el archivo **EmailService.cs**.

    Abra **EmailService.cs** en el editor. También puede agregar el archivo **EmailService.cs** al contexto Chat mediante una operación de arrastrar y soltar. Quite todos los demás archivos del contexto.

1. Pida a GitHub Copilot que identifique las duplicaciones en la clase EmailService.

    Por ejemplo:

    ```text
    Analyze the EmailService class. What duplicate logic exists within this service for handling order confirmations versus return confirmations? Describe opportunities to consolidate duplicate code.
    ```

1. Dedique un minuto a revisar las respuestas de GitHub Copilot.

    GitHub Copilot debe identificar la lógica duplicada para controlar las confirmaciones de pedido y devolver confirmaciones. Esto incluye un enfoque con plantilla para preparar y enviar correos electrónicos. GitHub Copilot también puede identificar patrones duplicados relacionados con los métodos auxiliares y el resultado de la consola.

1. Actualice el contexto del chat para especificar los archivos **AuditService.cs** e **InventoryService.cs**.

    Abra **AuditService.cs** y **InventoryService.cs** en el editor. También puede añadir estos archivos al contexto del chat mediante una operación de arrastrar y soltar. Quite todos los demás archivos del contexto.

1. Pida a GitHub Copilot que identifique las duplicaciones en los archivos de servicio de auditoría e inventario.

    Por ejemplo:

    ```text
    Analyze the AuditService and InventoryService classes. Identify the methods that contain duplicate logic patterns that could be consolidated. Describe opportunities to consolidate duplicate code.
    ```

1. Dedique un minuto a revisar las respuestas de GitHub Copilot.

    GitHub Copilot debería identificar patrones como la creación/validación/almacenamiento de entradas de auditoría en AuditService y la validación/actualización/registro de inventario en InventoryService. GitHub Copilot también puede identificar patrones duplicados relacionados con métodos auxiliares.

1. Pida a GitHub Copilot que realice un análisis completo de duplicación.

    Por ejemplo:

    ```text
    @workspace Analyze the entire ECommerceOrderAndReturn codebase and identify all forms of code duplication, including method-level, service-level, and architectural pattern duplications. Prioritize the duplications by impact and refactoring difficulty. Describe an approach for consolidating this code.
    ```

    Después de analizar archivos específicos, puede obtener una visión más amplia pidiendo a GitHub Copilot que incluya toda la base de código en su análisis. El mayor ámbito puede revelar patrones de duplicación adicionales, como el control de errores, el registro y la lógica de validación similares en varios archivos o capas. Tener una única respuesta que informe y priorice la estrategia de refactorización suele ser útil.

    > **NOTA**: Las palabras clave `@workspace` y `#codebase` le dicen a GitHub Copilot que incluya todo el código base en el contexto de su análisis. La palabra clave `@workspace` solo está disponible cuando se usa GitHub Copilot en el modo Preguntar. La palabra clave `#codebase` se puede usar en cualquier modo (Preguntar, Editar o Agente).

1. Dedique un minuto a revisar las respuestas de GitHub Copilot.

    La respuesta debe proporcionar un análisis completo de todos los patrones de duplicación y sugerir un enfoque para consolidar el código duplicado. En un escenario de producción, debe analizar cada sección de la respuesta y considerar el uso de avisos de seguimiento para profundizar en áreas específicas.

    Para este ejercicio de entrenamiento, es importante comprender qué tipos de información puede proporcionar GitHub Copilot, pero puede centrarse en la sección de resumen al considerar la estrategia de refactorización.

    Por ejemplo:

    ```md
    
    **Summary**

    The codebase contains significant method-level and service-level duplication, especially in validation, shipping calculation, audit logging, email notification, and inventory management. The highest priority and easiest wins are consolidating validation and shipping logic. Service-level helper methods should be refactored next. The processor workflow pattern can be abstracted for further maintainability, though this is more complex.

    Start with shared services for validation and shipping, then refactor service helpers, and finally consider architectural abstraction for processors.

    ```

1. Compruebe el análisis de GitHub Copilot con la revisión manual del código.

    Compare los resultados de GitHub Copilot con sus propias observaciones. Asegúrese de que comprende no solo lo que está duplicado, sino por qué existen estos patrones y cómo deben consolidarse al tiempo que mantienen la integridad de la lógica de negocios.

El modo Preguntar de GitHub Copilot es especialmente eficaz para identificar duplicaciones sutiles que van más allá de los simples casos de copiar y pegar. Puede reconocer patrones lógicos similares, reglas de negocio equivalentes implementadas de forma diferente y duplicaciones arquitectónicas que abarcan varios archivos.

> **NOTA**: El análisis generado durante esta tarea se usa para informar a la estrategia de refactorización que implemente en la sección siguiente.

### Consolide la lógica duplicada utilizando GitHub Copilot Chat (modo Agente).

El modo agente de GitHub Copilot le permite asignar tareas complejas de refactorización de varios pasos que abarcan varios archivos y capas arquitectónicas. El agente puede crear archivos nuevos de forma autónoma, modificar el código existente e implementar estrategias de refactorización completas al tiempo que le mantiene informado de su progreso.

En esta tarea, usará el agente GitHub Copilot para eliminar sistemáticamente los patrones de código duplicados identificados en la tarea anterior, empezando por las duplicaciones más sencillas y avanzando hacia consolidaciones más complejas en la capa de servicio.

Realice los pasos siguientes para completar esta tarea:

1. Cambie la Vista de chat de GitHub Copilot al modo Agente.

    Al usar el modo Agente, GitHub Copilot puede realizar cambios autónomos en el código base. El modo Agente es especialmente útil para tareas complejas de refactorización de varios pasos.

    Para cambiar los modos, busque el selector de modo (normalmente en la esquina inferior izquierda de la vista Chat) y seleccione **Agente**.

1. Dedique un minuto a planificar la estrategia de refactorización.

    Antes de asignar tareas al agente GitHub Copilot, considere el orden lógico para la refactorización. Use el análisis de la tarea anterior para informar de sus decisiones.

    Por ejemplo:

    Si GitHub Copilot sugirió:

    "Comience con los servicios compartidos para la validación y el envío, luego refactorice los asistentes de servicio y, por último, considere la abstracción arquitectónica para los procesadores".

    Puede usar uno de los siguientes métodos:

    - **Fase 1**: Duplicación básica de lógica de negocios (cálculo de validación y envío)
    - **Fase 2**: Duplicaciones de nivel de servicio (correo electrónico, auditoría, servicios de inventario)
    - **Fase 3**: Problemas transversales y mejoras arquitectónicas

    Este enfoque por fases garantiza que los cambios se puedan administrar y que se puedan probar de forma incremental.

1. Pida al agente GitHub Copilot que consolide la lógica de validación en las clases OrderProcessor y ReturnProcessor.

    Por ejemplo, envíe la siguiente tarea al agente GitHub Copilot:

    ```text
    Create a shared ValidationService class that consolidates the duplicate Validate() method logic from OrderProcessor and ReturnProcessor. The service should handle ID validation for both orders and returns while maintaining all existing security checks, business rules, and logging. Update both processor classes to use the new shared service and remove the duplicate private methods. Build and test the code to ensure the functionality remains intact. Continue working until the validation service is fully integrated.
    ```

1. Supervise el progreso del agente en la Vista de chat.

    El progreso del agente debe estar visible en el chat, ya que completa la tarea asignada.

    Para ayudar al agente a medida que se procesa la tarea, proporcione permiso para continuar o proporcionar contexto adicional según sea necesario. Por ejemplo, si el agente solicita permiso para compilar o ejecutar la aplicación, seleccione **Continuar.**

    El agente realizará lo siguiente durante esta tarea:

    - Crear un nuevo **archivo ValidationService.cs** en la carpeta Servicios
    - Extracción de la lógica de validación en un método reutilizable
    - Actualizar ambas clases de procesador para usar el nuevo servicio
    - Eliminación de los métodos de validación privada duplicados
    - Comprobación de la funcionalidad con una compilación y ejecución de pruebas correctas

1. Revise y acepte los cambios del servicio de validación.

    Use las pestañas del editor de código para examinar los cambios propuestos por el agente. Puede desplazarse por las ediciones del chat para ver las modificaciones de código específicas. Seleccione **Mantener** en la pestaña del editor para aceptar la edición actual. Puede seleccionar **Deshacer** en la pestaña editor para rechazar una edición.

    Seleccione **Mantener** o **Deshacer** en la Vista de chat para aceptar o rechazar todos los cambios.

    El nuevo servicio de validación debe mantener toda la lógica de validación existente al tiempo que proporciona una única implementación reutilizable. Si los cambios son correctos, aceptelos.

    > **NOTA**: Al trabajar en código de producción, es importante probarlo exhaustivamente después de operaciones de refactorización significativas. Esto implica compilar y probar la aplicación para comprobar que las características funcionan según lo previsto, se pasan las pruebas unitarias y la salida sigue siendo coherente con el comportamiento original. Para ahorrar tiempo durante este ejercicio de entrenamiento, recurrirá al agente para realizar pruebas incrementales. Se realizará una prueba adicional (comprobación manual) una vez completadas todas las tareas de refactorización.

1. Pida al agente GitHub Copilot que consolide la lógica de cálculo de envío.

    Por ejemplo, use la siguiente tarea para consolidar los cálculos de envío:

    ```text
    Create a shared ShippingCalculationService that consolidates the similar CalculateShipping() logic from OrderProcessor and ReturnProcessor. The service should handle both order shipping (with free shipping thresholds) and return shipping (with processing fees) while maintaining the different business rules for each type. Update both processor classes to use the new shared service. Build and test the code to ensure the functionality remains intact. Continue working until the shipping calculation service is fully integrated.
    ```

    El agente debe crear un servicio de envío que controle ambos escenarios al tiempo que conserva las distintas reglas de negocio para pedidos frente a devoluciones.

    > **NOTA**: Si el agente encuentra algún problema durante el proceso de refactorización de código, debe hacer referencia a las clases de procesador originales para obtener instrucciones y debe seguir actualizando y probando el código hasta que el servicio de cálculo de envío esté totalmente integrado. Si el agente no puede realizar la tarea asignada, o si el agente entra en un bucle de revisión de código que no puede resolver, detenga el agente y deshaga las modificaciones. La sesión de chat debe incluir suficiente contexto para solucionar el problema y actualizar la tarea (solicitud). También puede pedir a GitHub Copilot que le ayude a actualizar la tarea asignada de una manera que resuelva el problema.

1. Revise y acepte los cambios.

1. Pida al agente GitHub Copilot que refactorice las duplicaciones de EmailService.

    Por ejemplo, use la siguiente tarea para consolidar las duplicaciones del servicio de correo electrónico:

    ```text
    Refactor the EmailService class to eliminate duplicate logic in the helper methods. Create a unified approach for template building, subject formatting, email sending, and activity logging that can handle both order and return confirmations. The public methods SendOrderConfirmation and SendReturnConfirmation should remain, but they should use shared private helper methods. Build and test the code to ensure the functionality remains intact. Continue working until the unified approach is fully integrated.
    ```

1. Revise y acepte los cambios.

1. Pida al agente GitHub Copilot que consolide las duplicaciones de AuditService.

    Por ejemplo, use la siguiente tarea para consolidar las duplicaciones del servicio de auditoría:

    ```text
    Refactor the AuditService class to consolidate the duplicate logic in LogOrderActivity and LogReturnActivity. Create shared helper methods for audit entry creation, validation, storage, and compliance checking. The public methods should remain but use common underlying logic. Build and test the code to ensure the functionality remains intact. Continue working until the shared helper methods are fully integrated.
    ```

1. Revise y acepte los cambios.

1. Pida al agente GitHub Copilot que aborde las duplicaciones de InventoryService.

    Por ejemplo, use la siguiente tarea para gestionar las duplicaciones del servicio de inventario:

    ```text
    Refactor the InventoryService class to eliminate duplicate logic between ReserveOrderInventory and RestoreReturnInventory. Create shared helper methods for inventory validation, level updates, and transaction logging while maintaining the different business logic for reservations versus restorations. Build and test the code to ensure the functionality remains intact. Continue working until the shared helper methods are fully integrated.
    ```

1. Pida al agente GitHub Copilot que consolide cualquier duplicación restante en el código base.

    Por ejemplo, use la siguiente tarea para abordar las duplicaciones restantes:

    ```text
    Analyze the entire ECommerceOrderAndReturn codebase and identify any remaining duplicate code patterns that should be consolidated. Focus on cross-cutting concerns like payment processing, status updates, and error handling. Create shared services or helper methods as needed to eliminate these duplications while maintaining existing functionality. Build and test the code to ensure the functionality remains intact. Continue working until all identified duplications are fully integrated.
    ```

    La asignación de tareas como “detectar cualquier problema restante” al agente GitHub Copilot solo debe realizarse al final del proceso de refactorización y solo debe utilizarse cuando sea necesario. Intentar este tipo de análisis general demasiado pronto puede producir resultados inesperados o fallos en las tareas que deben revertirse. Es mejor crear un enfoque planeado y abordar las revisiones de forma prioritaria mediante un proceso preconfigurado.

    > **Nota:** Incluso después de que GitHub Copilot "consolide los patrones de código duplicados restantes", puede haber oportunidades para una mayor consolidación. Sin embargo, el enfoque planeado que implementó debe consolidar todas las duplicaciones principales en el código base. Si tiene dudas, puede repetir el proceso de análisis y refactorización. Recuerde que GitHub Copilot no debe usarse como sustituto de un proceso de revisión de código formal.

El agente GitHub Copilot destaca en tareas complejas de refactorización de múltiples archivos que requieren comprender la lógica empresarial y los patrones arquitectónicos. Al dividir la refactorización en fases lógicas y probar de forma incremental, se garantiza que la consolidación mantiene la integridad del sistema a la vez que mejora significativamente la calidad del código, la capacidad de mantenimiento, la extensibilidad y la reutilización.

### Pruebe los pedidos de comercio electrónico refactorizado y devuelva código.

Las pruebas y comprobaciones manuales son fundamentales para garantizar que el código refactorizado mantenga la lógica y la funcionalidad empresariales previstas. Un proceso de refactorización correcto debe lograr el objetivo previsto (por ejemplo, consolidar la lógica de código duplicado) al tiempo que genera un comportamiento idéntico a la implementación original.

En esta tarea, comprobará que el código refactorizado mantiene toda la funcionalidad original y que la consolidación se ha realizado correctamente.

Realice los pasos siguientes para completar esta tarea:

1. Compile el proyecto para comprobar si hay errores del compilador.

    Si hay errores de compilación, revise el código refactorizado y corrija los problemas. Puede usar GitHub Copilot para ayudar a diagnosticar y corregir los problemas que surjan del proceso de refactorización.

1. Ejecute la aplicación refactorizado y capture el resultado.

    La aplicación debe ejecutar los cinco escenarios de prueba exactamente igual que antes:

    - Presentación inicial del inventario
    - Procesamiento de pedidos válido con flujo de trabajo completo
    - Procesamiento de devolución válido con flujo de trabajo completo
    - Niveles de inventario actualizados
    - Pruebas de validación de seguridad con entradas no válidas

1. Pida a GitHub Copilot que compare el resultado generado por el código refactorizado con el resultado original.

    Por ejemplo:

    ```text
    Run the app and compare the generated output with the contents of the EXPECTED_OUTPUT.md file. Does the current output match the stored output? Explain any differences.
    ```

    La salida original, **EXPECTED_OUTPUT.md**, se incluye en la carpeta ECommerceOrderAndReturn.

    Puede crear un segundo archivo de resultado y pedir a GitHub Copilot que identifique las diferencias entre los dos archivos.

    La salida debe ser idéntica, lo que confirma que la lógica de negocios permanece sin cambios al consolidar la lógica de código duplicada.

1. Realice una revisión de código final.

    Revise el código base refactorizado para asegurarse de:

    - **Calidad del código**: Los métodos tienen un nombre correcto y siguen patrones coherentes
    - **Capacidad de mantenimiento**: Los cambios en las reglas de negocio ahora requieren actualizaciones en una sola ubicación
    - **Legibilidad**: La estructura de código es clara y lógica
    - **Reusabilidad**: Los servicios compartidos se pueden ampliar fácilmente para los requisitos futuros.
    - **Extensibilidad**: Se pueden agregar nuevas características con un impacto mínimo en el código existente

Las pruebas manuales comprueban que los esfuerzos de consolidación han logrado el objetivo previsto: eliminar el código duplicado al tiempo que mantiene la funcionalidad del sistema. La arquitectura ahora proporciona una base más fácil de mantener para el desarrollo futuro, donde los cambios en las reglas de negocio se pueden implementar en una sola ubicación en lugar de requerir actualizaciones en varias implementaciones duplicadas.

## Resumen

En este ejercicio, ha aprendido a usar GitHub Copilot para consolidar el código duplicado en una aplicación. Ha explorado el sistema de procesamiento de pedidos y devoluciones de comercio electrónico, ha identificado patrones de código duplicados y ha usado GitHub Copilot para refactorizar el código base para mejorar la capacidad de mantenimiento y la legibilidad.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Si ha realizado algún cambio, reviértalos según sea necesario. Si usa un equipo local como entorno de laboratorio, puede archivar o eliminar la carpeta de proyectos de ejemplo que ha creado para este ejercicio.
