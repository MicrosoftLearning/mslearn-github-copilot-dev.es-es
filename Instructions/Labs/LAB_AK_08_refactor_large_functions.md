---
lab:
  title: "Ejercicio: Refactorización de funciones grandes mediante GitHub\_Copilot"
  description: "Obtenga información sobre cómo analizar código complejo y refactorizar funciones grandes en métodos más pequeños y centrados mediante herramientas de GitHub\_Copilot."
---

# Refactorización de funciones grandes mediante GitHub Copilot

Las funciones grandes pueden ser difíciles de leer, mantener y probar. A menudo contienen varias responsabilidades y pueden ser difíciles de entender de un vistazo. La refactorización de funciones grandes en otras más pequeñas y centradas puede mejorar la legibilidad y el mantenimiento del código.

En este ejercicio, revisará un proyecto existente que contiene una función grande, analizará las opciones de funciones de responsabilidad única más pequeñas, refactorizará la función grande en funciones más pequeñas y probará el código refactorizado para asegurarse de que funciona según lo previsto. Usará GitHub Copilot en el modo Preguntar para comprender un proyecto de código existente y explorar las opciones para refactorizar la lógica. Usará GitHub Copilot en modo Agente para refactorizar el código mediante la extracción de secciones de código de la función grande para crear funciones más pequeñas. Probará el código original y refactorizado para asegurarse de que el código refactorizado funciona según lo previsto.

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

- Abra un terminal de comandos y luego ejecute los siguientes comandos:

    A fin de asegurarse de que Visual Studio Code está configurado para usar la versión correcta de .NET, ejecute el siguiente comando:

    ```bash

    dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org

    ```

    Para asegurarse de que Git está configurado para usar el nombre y la dirección de correo electrónico, actualice los siguientes comandos con la información y, después, ejecute los comandos:

    ```bash

    git config --global user.name "John Doe"

    ```

    ```bash

    git config --global user.email johndoe@example.com

    ```

### Descarga del proyecto de código de ejemplo

Siga estos pasos para descargar el proyecto de ejemplo y abrirlo en Visual Studio Code:

1. Abra una ventana del explorador en el entorno de laboratorio.

1. Para descargar un archivo ZIP que contenga el proyecto de aplicación de ejemplo, abra la URL siguiente en el explorador: [Laboratorio de GitHub Copilot: Refactorización de funciones grandes](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/GHCopilotEx8LabApps.zip)

    El archivo ZIP se denomina **GHCopilotEx8LabApps.zip**.

1. Extraiga los archivos del archivo **GHCopilotEx8LabApps.zip**.

    Por ejemplo:

    1. Vaya a la carpeta de descargas del entorno de laboratorio.

    1. Haga clic con el botón derecho en *GHCopilotEx8LabApps.zip* y, después seleccione **Extraer todo**.

    1. Seleccione **Mostrar los archivos extraídos al completar** y, a continuación, **Extraer**.

1. Copia la carpeta **GHCopilotEx8LabApps** en una ubicación que sea fácil de acceder, como la carpeta Escritorio de Windows.

1. Abra la carpeta **GHCopilotEx8LabApps** en Visual Studio Code.

    Por ejemplo:

    1. Abra Visual Studio Code en el entorno de laboratorio.

    1. En Visual Studio Code, en el menú **Archivo**, seleccione **Abrir archivo**.

    1. Vaya a la carpeta Escritorio de Windows, seleccione **GHCopilotEx8LabApps** y luego **Seleccionar carpeta**.

1. En la vista EXPLORADOR DE SOLUCIONES de Visual Studio Code, compruebe la siguiente estructura del proyecto:

    - GHCopilotEx8LabApps\
        - ECommerceOrderProcessing\
            - src\
                - ECommerce.ApplicationCore\
                    - Entities\
                    - Exceptions\
                    - Interfaces\
                    - Services\
                        - OrderProcessor.cs
                - ECommerce.Console\
                    - order_audit_log.txt
                    - Program.cs
                - ECommerce.Infrastructure\
                    - Services\
        - ServerLogAnalysisUtility\

## Escenario del ejercicio

Es desarrollador de software y trabaja para una empresa de consultoría. Los clientes necesitan ayuda para refactorizar funciones grandes en aplicaciones heredadas. El objetivo es mejorar la legibilidad y capacidad de mantenimiento del código a la vez que se conserva la funcionalidad existente. Se le asigna a la aplicación siguiente:

- E-CommerceOrderProcessing: Esta aplicación de comercio electrónico se usa para procesar los pedidos de los clientes. El proceso incluye la validación de pedidos, la administración del inventario, el procesamiento de pagos, la coordinación del envío y las notificaciones al cliente. La aplicación usa principios de arquitectura limpia con una estructura en capas, pero contiene un método grande en la clase **OrderProcessor** que controla varias responsabilidades y se debe refactorizar en métodos más pequeños y centrados.

Este ejercicio incluye las siguientes tareas:

1. Revise manualmente el código base de procesamiento de pedidos de comercio electrónico.
1. Identifique las oportunidades de refactorización mediante GitHub Copilot Chat (modo Preguntar).
1. Refactorice una función grande en funciones más pequeñas y administrables mediante GitHub Copilot Chat (modo Agente).
1. Pruebe el código de procesamiento de pedidos de comercio electrónico refactorizado.

### Revisión manual del código base de procesamiento de pedidos de comercio electrónico

El primer paso de cualquier esfuerzo de refactorización es asegurarse de que comprende el código base existente. Es importante comprender la estructura del código, la lógica de negocios y los resultados generados cuando se ejecuta el código.

En esta tarea, revisará los componentes principales del proyecto de procesamiento de pedidos de comercio electrónico y ejecutará la aplicación para observar su funcionalidad.

Realice los pasos siguientes para completar esta tarea:

1. Asegúrese de que la carpeta GHCopilotEx8LabApps esté abierta en Visual Studio Code.

    Consulte la sección **Antes de empezar** si no ha descargado el proyecto de código de ejemplo.

1. Dedique un minuto a revisar la estructura del proyecto ECommerceOrderProcessing.

    El código base sigue un patrón de arquitectura en capas con tres proyectos principales:

    - **ECommerce.ApplicationCore**: contiene entidades de dominio, interfaces de lógica de negocios y el servicio OrderProcessor principal.
    - **ECommerce.Console**: contiene el punto de entrada de la aplicación de consola y la configuración de inserción de dependencias.
    - **ECommerce.Infrastructure**: contiene implementaciones de servicio para integraciones externas (pagos, envíos, inventario, etc.).

    Esta estructura representa una aplicación de .NET real que usa principios de arquitectura limpia, donde la lógica de negocios está separada de los problemas de infraestructura.

1. Abra la vista GitHub Copilot Chat.

    Si la vista Chat aún no está abierta, puede abrirla si selecciona el icono **Chat** situado en la parte superior de la ventana de Visual Studio Code.

1. En la vista Chat, asegúrese de que el modo de chat está establecido en **Preguntar** y el modelo está establecido en **GPT-4o**.

    Estos valores están disponibles en la esquina inferior izquierda de la vista Chat. El modo **Preguntar**de GitHub Copilot se usa para formular preguntas generales de programación y generar explicaciones relacionadas con el código. El modelo **GPT-4o**, que se incluye con el plan Gratis de GitHub Copilot, es una buena opción para el análisis de código y la guía de refactorización.

    Usará el modo **Agente** de GitHub Copilot más adelante en este ejercicio, pero por ahora debe usar el modo **Preguntar** para el análisis de código y las explicaciones.

    > **NOTA**: Las respuestas de GitHub Copilot pueden variar en función del modelo seleccionado. Se recomienda usar el modelo especificado al realizar este ejercicio de laboratorio. Puede repetir el ejercicio con otros modelo si quiere ver las diferencias.

1. Use la vista EXPLORADOR DE SOLUCIONES para buscar el archivo **OrderProcessor.cs**.

    El archivo **OrderProcessor.cs** se encuentra en la carpeta **src/ECommerce.ApplicationCore/Services**.

1. Abra el archivo **OrderProcessor.cs** en el editor de código.

    La clase OrderProcessor es responsable de procesar los pedidos de los clientes. Contiene la lógica de negocios principal para el procesamiento de pedidos, incluida la validación, el procesamiento de pagos y la notificación.

1. Dedique un minuto a revisar la clase **OrderProcessor**.

    Observe el método ProcessOrder. Este método representa la lógica empresarial principal para procesar los pedidos de los clientes. Observe que controla varias operaciones distintas. El método ProcessOrder es intencionadamente grande y complejo para demostrar escenarios reales en los que la lógica de negocios se ha acumulado con el tiempo, lo que dificulta la lectura, las pruebas y el mantenimiento.

1. Haga clic con el botón derecho en el método **ProcessOrder** y seleccione **Copilot** > **Explicar**.

    Si se le pide que **seleccione un intervalo de inclusión para explicarlo**, seleccione **ProcessOrder**.

    GitHub Copilot analizará el método ProcessOrder y proporcionará una explicación detallada de lo que hace el código, lo que le ayudará a comprender la lógica de negocios antes de investigar las opciones de refactorización.

1. Dedique unos minutos a revisar la explicación de GitHub Copilot.

    La explicación debe resaltar los principales pasos de procesamiento y las reglas de negocio, como los procedimientos de validación completos, las evaluaciones de riesgos de seguridad, la coordinación de varios servicios y el control de errores con funcionalidades de reversión.

1. Ejecute la aplicación para comprender su comportamiento actual.

    Tiene varias opciones para ejecutar la aplicación. Por ejemplo:

    En la vista EXPLORADOR DE SOLUCIONES, haga clic con el botón derecho en el proyecto **ECommerce.Console**, seleccione **Depurar** y después **Iniciar nueva instancia**. O bien, si tiene el archivo **Program.cs** abierto en Visual Studio Code, puede seleccionar el botón Ejecutar situado encima del editor.

    También puede ir a la carpeta **src/ECommerce.Console** en el terminal y escribir el siguiente comando de la CLI de .NET:

    ```bash
    dotnet run
    ```

1. Revise la salida de la consola que se genera cuando se ejecuta la aplicación.

    La aplicación genera una salida para cuatro casos de prueba. Cada caso de prueba muestra un escenario diferente:

    - **Prueba 1**: Procesamiento de pedidos válido con varios elementos.
    - **Prueba 2**: Validación de direcciones de correo electrónico no válida.
    - **Prueba 3**: Control de pagos rechazados.
    - **Prueba 4**: Comprobaciones de seguridad de pedidos sospechosos.

    En la salida de cada caso de prueba se muestra el procesamiento paso a paso, incluidos los mensajes de validación, las comprobaciones de inventario, el procesamiento de pagos, la programación de envíos y las notificaciones. En la salida también se muestra cómo se controlan los distintos escenarios de error con los mensajes de error adecuados y los procedimientos de limpieza.

1. Dedique un minuto a tener en cuenta las oportunidades de refactorización para el método ProcessOrder.

    El método ProcessOrder tiene varias responsabilidades distintas. Cada una de las secciones de código correspondientes se podría extraer en un método independiente.

Comprender la funcionalidad existente e identificar las oportunidades de refactorización le ayudará a crear una estrategia de refactorización que mantenga la lógica empresarial al tiempo que mejora la estructura del código. La arquitectura en capas ya proporciona una buena separación de preocupaciones en el nivel de proyecto, pero el método ProcessOrder grande necesita atención.

### Identificación de oportunidades de refactorización mediante GitHub Copilot Chat (modo Preguntar)

El modo Preguntar de GitHub Copilot Chat es una excelente herramienta para analizar código complejo e identificar oportunidades para refactorizar métodos grandes. En el modo Preguntar, Copilot puede analizar la estructura de código y sugerir maneras de dividir métodos monolíticos en métodos más pequeños y centrados.

En esta tarea, usará GitHub Copilot para evaluar el método ProcessOrder e identificar las oportunidades de refactorización que mantienen la lógica de negocios al tiempo que se mejora la estructura del código.

Realice los pasos siguientes para completar esta tarea:

1. Asegúrese de que tiene abierta la vista Chat de GitHub Copilot con el modo **Preguntar** y el modelo **GPT-4o** seleccionado.

1. Si ha abierto archivos distintos de OrderProcessor.cs, ciérralos ahora.

    GitHub Copilot usa archivos que se abren en el editor para establecer el contexto. Tener solo el archivo de destino abierto ayuda a centrar el análisis en el código que se quiere refactorizar y garantiza que GitHub Copilot proporciona las sugerencias más relevantes.

1. Agregue el archivo OrderProcessor.cs al contexto de Chat.

    Use una operación de arrastrar y colocar para agregar el archivo **src/ECommerce.ApplicationCore/Services/OrderProcessor.cs** desde el EXPLORADOR de SOLUCIONES al contexto de Chat. Agregar un archivo al contexto de chat indica a GitHub Copilot que lo incluya al analizar el mensaje, lo que mejora la precisión de su análisis.

1. Pídale a GitHub Copilot que analice el método ProcessOrder para buscar oportunidades de refactorización.

    Envíe un mensaje que pida a GitHub Copilot que analice el método ProcessOrder e identifique áreas específicas para mejorar. Considere la posibilidad de incluir detalles sobre lo que quiere lograr con la refactorización.

    Por ejemplo:

    ```text
    Analyze the ProcessOrder method in the OrderProcessor class. This method handles multiple responsibilities. Identify opportunities to break this large method into smaller, more focused methods. What specific functions could be extracted, and what would be the benefits of doing so?
    ```

1. Dedique unos minutos a revisar la respuesta de GitHub Copilot.

    GitHub Copilot debe identificar las distintas responsabilidades dentro del método ProcessOrder y sugerir cómo extraerlas en métodos independientes. El análisis debe identificar secciones lógicas distintas que pueden convertirse en métodos individuales, como las de lógica de validación, evaluaciones de seguridad, operaciones de inventario, procesamiento de pagos, coordinación del envío, control de notificaciones y finalización de pedidos.

    Por ejemplo, GitHub Copilot podría identificar lo siguiente:

    - Validación de entrada y comprobaciones de seguridad como candidatos para la extracción.
    - Operaciones de administración de inventario que se pueden agrupar.
    - Lógica de procesamiento de pagos con su propio control de errores.
    - Lógica de envíos y notificaciones como preocupaciones independientes.
    - Pasos de finalización de pedidos que se podrían aislar.

1. Pídale a GitHub Copilot que proporcione un plan de refactorización detallado.

    Por ejemplo:

    ```text
    Create a detailed refactoring plan for the ProcessOrder method. Show me what the ProcessOrder method would look like after refactoring and provide a list of the methods that should be extracted. I'd like to keep the input validation and security checks together in a single method. Include suggestions for method signatures and return types that would maintain the current error handling behavior.
    ```

    Los mensajes de seguimiento como este se pueden usar para obtener información adicional, pero debe evitar los mensajes que se desvíen del objetivo. El seguimiento lateral de la conversación de chat puede influir en las respuestas de GitHub Copilot. Un historial de chat limpio es importante.

1. Dedique unos minutos a revisar el plan de refactorización de GitHub Copilot.

    GitHub Copilot debe proporcionar un esquema claro en el que se muestre cómo se puede transformar el método ProcessOrder de un método monolítico grande en una serie de llamadas de método más pequeñas y centradas. Este plan debe mantener la lógica de negocios existente al tiempo que mejora la estructura de código y la legibilidad.

    La respuesta debe incluir lo siguiente:
    - Un flujo general que muestra los pasos principales como llamadas de método independientes.
    - Nombres de método sugeridos y firmas para los métodos extraídos.
    - Instrucciones sobre cómo controlar los errores de forma coherente entre métodos.
    - Explicaciones de cómo mejora la capacidad de mantenimiento de la estructura refactorizada.

1. Pida instrucciones adicionales sobre patrones de control de errores.

    Comprender el proceso de control de errores es fundamental para mantener el comportamiento existente al refactorizar el método ProcessOrder. Puede hacer que GitHub Copilot analice la estrategia de control de errores actual y sugiera una manera de mantener o mejorar el comportamiento existente.

    Por ejemplo:

    ```text
    In the current ProcessOrder method, there are multiple error scenarios with specific cleanup procedures (like releasing inventory on payment failure). In the refactored version, how should I handle errors consistently across the extracted methods? Should each method return an OrderResult object, throw exceptions, or use another pattern to maintain the existing error handling behavior?
    ```

1. Dedique unos minutos a revisar las recomendaciones de control de errores.

    GitHub Copilot debe proporcionar instrucciones para mantener patrones de control de errores coherentes en los métodos refactorizados. Esto es fundamental porque el método actual tiene un control complejo de errores con procedimientos de reversión que se deben conservar.

    Las recomendaciones deben abordar lo siguiente:
    - Cómo mantener el comportamiento de reversión actual (como la liberación del inventario en caso de errores de pago).
    - Si se usan valores devueltos, excepciones u objetos de resultado para la señalización de errores.
    - Cómo conservar el registro de auditoría a lo largo de los métodos refactorizados.
    - Formas de asegurarse de que los procedimientos de limpieza se siguen ejecutando en escenarios de error.

El modo Preguntar de GitHub Copilot destaca en el análisis de estructuras de código complejas y al proporcionar instrucciones estratégicas para la refactorización. La información de este análisis determinará el enfoque de refactorización específico que implementará en la sección siguiente, asegurándose de mantener la integridad de la lógica de negocios mientras se logra una mejor organización del código.

### Refactorización de funciones grandes mediante GitHub Copilot Chat (modo Agente)

El modo Agente le permite asignar tareas complejas de refactorización de código a GitHub Copilot. Las tareas asignadas pueden incluir la creación o actualización de varios archivos. El agente de GitHub Copilot procesa las tareas de forma autónoma, prueba y depura las actualizaciones mientras funciona y le mantiene informado al notificar su progreso en la vista Chat.

En esta tarea, usará el agente de GitHub Copilot para refactorizar sistemáticamente el método ProcessOrder mediante la extracción de métodos más pequeños y centrados a la vez que conserva la lógica empresarial existente y el comportamiento de control de errores.

Realice los pasos siguientes para completar esta tarea:

1. Asegúrese de que la vista Chat de GitHub Copilot está abierta en Visual Studio Code.

1. En la vista Chat, seleccione el modo **Agente**.

    El menú desplegable **Establecer modo** se encuentra en la esquina inferior izquierda de la vista Chat. En el modo **Agente**, GitHub Copilot procesa sus tareas asignadas (los mensajes) de forma autónoma.

1. Dedique un minuto a tener en cuenta la estrategia de refactorización.

    Use el análisis de la tarea anterior a fin de formular una estrategia para refactorizar el método ProcessOrder. El enfoque debe admitir pruebas incrementales.

    Por ejemplo, considere esta estrategia de refactorización por fases:

    - **Fase 1**: Cree métodos de código auxiliar dentro de la clase OrderProcessor.
    - **Fase 2**: Extraiga la lógica de validación de entrada y evaluación de seguridad.
    - **Fase 3**: Extraiga las operaciones de administración del inventario (comprobación y reserva).
    - **Fase 4**: Extraiga el procesamiento de pagos con detección de fraudes y control de errores.
    - **Fase 5**: Extraiga la coordinación de envíos y la administración del seguimiento.
    - **Fase 6**: Extraiga la lógica de notificación y comunicación.
    - **Fase 7**: Extraiga los procedimientos de finalización de pedidos.

    Este enfoque por fases garantiza que los cambios se puedan administrar y que las actualizaciones se puedan probar de forma incremental. El código refactorizado debe mantener la misma lógica de negocios y control de errores que el método original.

1. En el editor de código, desplácese hasta la parte inferior de la clase OrderProcessor y, después, cree el siguiente comentario de código después de la llave de cierre del método ProcessOrder:

    ```csharp

        }
    
        // Add stub methods here
        
    }

    ```

    El comentario de código debe ubicarse después de la llave de cierre final del método ProcessOrder y antes de la llave de cierre de la clase OrderProcessor.

    Le indicará a GitHub Copilot que use esta ubicación cuando cree los métodos de uso único dentro de la clase OrderProcessor.

1. Pídale al Agente de GitHub Copilot que cree métodos de código auxiliar que se pueden usar para contener el código extraído.

    Por ejemplo:

    ```text
    Review the current conversation. I want to start by creating stub code for the new single-purpose methods that will be used when refactoring the ProcessOrder method. Use the method declarations that you proposed in this conversation. Create the new stub methods below the "Add stub methods here" comment in the OrderProcessor class. Ensure that you're using appropriate method parameters and return types. Do not extract any code from the ProcessOrder method, just create the stub methods. After the stub methods are created, open the terminal, navigate to the "ECommerceOrderProcessing/src/ECommerce.Console" directory, then run a "dotnet build" command. Ensure that there are no build errors.
    ```

    La creación de los métodos auxiliares primero ayuda a garantizar que los nuevos métodos se definen correctamente y se integran en la estructura de código existente. Este enfoque permite realizar pruebas incrementales y validar la funcionalidad de cada método antes de extraer completamente el código de ProcessOrder.

1. Supervise el progreso del agente y proporcione asistencia cuando sea necesario.

    El agente de GitHub Copilot creará los métodos en la ubicación especificada y, después, solicitará permiso para ejecutar un comando de compilación en el terminal. Seleccione el botón **Continuar** cuando se le solicite (para permitir que el agente continúe).

    Si el agente encuentra un problema, debe notificarlo y, después, intentar corregirlo automáticamente. Siga proporcionando asistencia cuando sea necesario.

    Después de realizar la tarea de compilación, el agente debe informarle de que los nuevos métodos se han definido correctamente y que no hay errores de sintaxis.

1. Para aceptar las modificaciones, seleccione **Mantener**.

    Puede aceptar (o rechazar) modificaciones individualmente en el editor de código o todas a la vez en la interfaz de chat de GitHub Copilot.

1. Pídale al Agente de GitHub Copilot que refactorice el método ProcessOrder.

    La refactorización de métodos grandes funciona mejor cuando la tarea se puede dividir en fases administrables. En este caso, las fases se alinean con los métodos de proceso único que ya ha identificado. Se debe aplicar el mismo enfoque al usar un agente para refactorizar el código automáticamente. Escriba una tarea que indique al agente que refactorice una sección a la vez y, después, pruebe las actualizaciones antes de pasar a la sección siguiente.

    Pero trabajar con el agente de GitHub Copilot puede ser como tener un desarrollador disponible que pueda trabajar de forma independiente en una serie de asignaciones. En este caso, la serie de asignaciones consiste en refactorizar cada sección de código y probar las actualizaciones antes de pasar a la sección siguiente. En otras palabras, puede escribir una sola tarea (un mensaje) que pida al Agente de GitHub Copilot que refactorice cada una de las secciones de código y pruebe cada uno de los métodos de un solo propósito antes de pasar a la refactorización de la sección siguiente.

    Por ejemplo:

    ```text
    Review the current conversation. Examine the ProcessOrder method and identify the code sections that should be extracted into the single-purpose stub methods that you already created. Move the identified code sections into the associated single-purpose stub methods, constructing and testing the methods in the suggested order. Replace the extracted code sections with a call to the associated single-purpose method. Use local variables of the associated return value type to ensure that the ProcessOrder method maintains the same error handling behavior that's provided by the original code. As each method is updated, use a "dotnet run" command to ensure that the code features and error handling processes work correctly (including rollback features, like releasing inventory on payment failure). Also verify that the four test case scenarios generate the expected console output when the app is run (all test cases should pass). Continue extracting code into the new single-purpose methods (and testing the app) until all methods are complete and the application generates the expected console output for the four test case scenarios. Don't stop working on this task until all methods are constructed and tested. Display the step-by-step approach that you'll use to complete this task and then begin.
    ```

    > **NOTA**: Al trabajar en código de producción, es importante probarlo exhaustivamente después de operaciones de refactorización significativas. Esto implica compilar y probar la aplicación para comprobar que las características funcionan según lo previsto, se pasan las pruebas unitarias y la salida sigue siendo coherente con el comportamiento original. Para ahorrar tiempo durante este ejercicio de entrenamiento, recurrirá al agente para realizar pruebas incrementales. Completará una prueba adicional (una comprobación manual) una vez que se completen las tareas de refactorización de código.

1. Supervise el progreso del agente y proporcione asistencia cuando sea necesario.

    El agente de GitHub Copilot debe empezar por describir su plan para refactorizar cada sección del método ProcessOrder. El plan debe incluir un enfoque paso a paso para cada sección de código que incluya: mover código del método ProcessOrder al método de proceso único correspondiente, reemplazar el código extraído en ProcessOrder por una llamada de método y probar la aplicación para asegurarse de que el código refactorizado funciona según lo previsto.

    El agente también proporcionará actualizaciones en la vista Chat que describen su progreso, incluidos los problemas que encuentre. Puede interactuar con el agente para aclarar instrucciones o proporcionar contexto adicional según sea necesario.

    El Agente de GitHub Copilot normalmente solicita permiso para compilar o ejecutar la aplicación durante el proceso de refactorización. Cuando esto ocurra, seleccione el botón **Continuar** en la vista Chat para permitir que el agente continúe.

    > **IMPORTANTE**: Si el agente de GitHub Copilot deja de procesar la tarea asignada antes de que se refactoricen todas las secciones del método ProcessOrder, escriba un mensaje que indique al agente que continúe con la tarea de refactorización.

1. Una vez que se complete el proceso de refactorización, acepte los cambios.

    Seleccione el botón **Mantener** en la vista Chat para aceptar todos los cambios realizados por el agente.

1. Dedique un minuto a revisar la clase OrderProcessor actualizada.

    Una vez que el agente complete sus tareas de refactorización, la clase OrderProcessor debe contener varios métodos más pequeños y centrados que controlan aspectos específicos del procesamiento de pedidos. El método ProcessOrder debe ser significativamente más corto y legible, con cada paso del flujo de trabajo de procesamiento de pedidos claramente definido en su propio método.

    Por ejemplo, el método ProcessOrder actualizado debe tener un aspecto similar al siguiente:

    ```csharp
    public OrderResult ProcessOrder(Order order)
    {
        // Log the start of order processing for audit trail
        _auditLogger.LogOrderProcessingStarted(order.Id, order.CustomerEmail);

        try
        {
            // Validate order and perform security checks
            if (!ValidateOrderAndSecurity(order, out string? validationFailure))
            {
                return OrderResult.Failure(validationFailure ?? "Validation failed for unknown reasons");
            }

            Console.WriteLine($"Processing Order {order.Id} for {_securityValidator.MaskEmail(order.CustomerEmail)}...");
            Console.WriteLine($"Order contains {order.Items.Count} items, Total: ${order.TotalAmount:F2}");

            // Check inventory and reserve stock
            if (!CheckAndReserveInventory(order, out string? inventoryFailure))
            {
                return OrderResult.Failure(inventoryFailure ?? "Inventory check failed for unknown reasons");
            }
            Console.WriteLine("Inventory reserved successfully.");
            _auditLogger.LogInventoryReserved(order.Id, order.Items.Count);

            // Payment Processing with Enhanced Security
            Console.WriteLine("Processing payment...");
            // Process payment
            if (!ProcessPayment(order, out string? paymentFailure))
            {
                return OrderResult.Failure(paymentFailure ?? "Payment processing failed for unknown reasons");
            }

            // Shipping and Logistics Management
            Console.WriteLine("Scheduling shipping...");
            // Schedule shipping
            if (!ScheduleShipping(order, out string? shippingFailure))
            {
                return OrderResult.Failure(shippingFailure ?? "Shipping scheduling failed for unknown reasons");
            }

            // Customer Communication and Notifications
            Console.WriteLine("Sending notifications...");
            // Send notifications
            SendNotifications(order);

            // Order Finalization and Data Recording
            Console.WriteLine("Finalizing order...");
            order.Status = OrderStatus.Completed;
            order.CompletionDate = DateTime.UtcNow;
            order.ProcessingDuration = DateTime.UtcNow - order.OrderDate;

            // In a real app, this would update the order record in a database
            // _orderRepository.UpdateOrder(order);

            Console.WriteLine($"Order {order.Id} completed successfully in {order.ProcessingDuration.TotalSeconds:F1} seconds.");
            _auditLogger.LogOrderCompleted(order.Id, order.TotalAmount);

            // Finalize the order
            FinalizeOrder(order);

            return OrderResult.Success(order.Id, order.TrackingNumber ?? "");
        }
        catch (Exception ex)
        {
            HandleUnexpectedError(order, ex);
            return OrderResult.Failure("An unexpected error occurred during order processing");
        }
    }

    ```

El Agente de GitHub Copilot destaca en tareas de refactorización sistemáticas que requieren la comprensión del flujo de código, la lógica empresarial y los patrones de control de errores. Al dividir la refactorización en fases lógicas, se asegura de que cada cambio se puede administrar y probar, y mantiene el comportamiento original del sistema, a la vez que mejora significativamente la organización y el mantenimiento del código.

### Prueba del código de procesamiento de pedidos de comercio electrónico refactorizado

Las pruebas manuales y la comprobación garantizan que el código refactorizado mantenga la lógica de negocios y la funcionalidad previstas. Un proceso de refactorización correcto debe mejorar la estructura del código al tiempo que genera un comportamiento idéntico a la implementación original.

En esta tarea, probará el código refactorizado para comprobar que se ha conservado toda la lógica de negocios y que la refactorización ha logrado sus objetivos de mejora del mantenimiento y la legibilidad.

Realice los pasos siguientes para completar esta tarea:

1. Ejecute la aplicación refactorizada y compruebe el comportamiento esperado.

    Compare la salida con el comportamiento observado antes de la refactorización. La salida de la consola debe ser idéntica, incluido lo siguiente:

    - **Prueba 1 (Pedido válido)**: Se debe completar correctamente con el procesamiento de pagos, la programación de envíos y las notificaciones
    - **Prueba 2 (Correo electrónico no válido)**: Si se produce un error en la validación con el mismo mensaje de error
    - **Prueba 3 (Pago rechazado)**: Si se produce un error en el procesamiento de pagos y se desencadena la reversión del inventario
    - **Prueba 4 (Pedido sospechoso)**: Se debe marcar mediante la evaluación de seguridad y rechazar

    El código refactorizado debe generar exactamente los mismos resultados, lo que demuestra que la lógica de negocios se ha conservado en todo el proceso de refactorización.

1. Cree y pruebe escenarios de casos perimetrales adicionales para garantizar la solidez.

    Cree escenarios de prueba adicionales para comprobar que el control de errores funciona correctamente en varios casos perimetrales. Puede modificar temporalmente los casos de prueba en **Program.cs** para probar escenarios adicionales.

    Por ejemplo, puede agregar el siguiente fragmento de código antes del código que muestra el resumen de pruebas:

    ```csharp
    // Test with empty items list (should fail validation)
    System.Console.WriteLine("\n--- Test Case 5: Empty Order ---");
    var emptyOrder = CreateSampleOrder("ORD-EMPTY", "test@example.com", "123 Test St",
        new List<OrderItem>(),
        new PaymentInfo { CardNumber = "4111111111111111", CardCVV = "123", CardHolderName = "Test User", ExpiryMonth = "12", ExpiryYear = "2025", BillingAddress = "123 Test St" });

    var result5 = processor.ProcessOrder(emptyOrder);
    testResults.Add($"Test 5: {(result5.IsSuccess ? "FAILED" : "PASSED")} - Should reject empty order");

    // Test with invalid shipping address (should fail validation)
    System.Console.WriteLine("\n--- Test Case 6: Invalid Shipping Address ---");
    var invalidAddressOrder = CreateSampleOrder("ORD-ADDR", "user@example.com", "",
        new List<OrderItem> { new() { ProductId = "BOOK-001", Quantity = 1, Price = 15.99m } },
        new PaymentInfo { CardNumber = "4111111111111111", CardCVV = "123", CardHolderName = "Test User", ExpiryMonth = "12", ExpiryYear = "2025", BillingAddress = "123 Test St" });

    var result6 = processor.ProcessOrder(invalidAddressOrder);
    testResults.Add($"Test 6: {(result6.IsSuccess ? "FAILED" : "PASSED")} - Should reject invalid shipping address");
    ```

    Estas pruebas adicionales ayudan a comprobar que la lógica de validación refactorizada controla correctamente los casos perimetrales y que los mensajes de error siguen siendo coherentes con la implementación original.

1. Ejecute la aplicación y compruebe los resultados.

    Al ejecutar la aplicación, debería ver los resultados de las pruebas en la consola, lo que indica si cada caso de prueba se ha superado o no. Preste atención a los mensajes de error o registros que se generan durante las ejecuciones de prueba.

    Por ejemplo, si ha agregado los escenarios de prueba 5 y 6 enumerados antes, la nueva salida de prueba y el resumen actualizado deben tener un aspecto similar al siguiente:

    ```text

    --- Test Case 5: Empty Order ---
    [AUDIT] 2025-08-20 18:28:11.099 UTC | ORDER_PROCESSING_STARTED | Order: ORD-EMPTY | Started processing order for t***@example.com
    [AUDIT] 2025-08-20 18:28:11.100 UTC | VALIDATION_FAILURE | Order: ORD-EMPTY | Empty order items
    
    --- Test Case 6: Invalid Shipping Address ---
    [AUDIT] 2025-08-20 18:28:11.101 UTC | ORDER_PROCESSING_STARTED | Order: ORD-ADDR | Started processing order for u***@example.com
    [AUDIT] 2025-08-20 18:28:11.101 UTC | VALIDATION_FAILURE | Order: ORD-ADDR | Invalid shipping address
    
    === TEST SUMMARY ===
    Test 1: PASSED - ORD-001
    Test 2: PASSED - Should reject invalid email
    Test 3: PASSED - Should reject declined payment
    Test 4: PASSED - Should flag suspicious order
    Test 5: PASSED - Should reject empty order
    Test 6: PASSED - Should reject invalid shipping address

    ```

1. Vuelva a ejecutar la aplicación para comprobar que el registro de auditoría funciona correctamente.

    Compruebe el archivo **order_audit_log.txt** para asegurarse de que el registro de auditoría sigue funcionando correctamente en los métodos refactorizados. Los eventos más recientes se encuentran en la parte inferior del archivo.

    La pista de auditoría debe ser completa y demostrar que el registro se ha conservado en todos los métodos extraídos.

    > **SUGERENCIA**: El archivo order_audit_log.txt se crea o actualiza en el directorio de trabajo actual de la aplicación. En función de cómo decida ejecutar el proyecto ECommerce.Console, el directorio de trabajo podría ser "src/ECommerce.Console/bin/Debug/net9.0" en lugar de "src/ECommerce.Console". Para generar el archivo de auditoría en el directorio "src/ECommerce.Console", ejecute la aplicación desde el terminal mediante un comando de la CLI de .NET.

    Los siguientes tipos de eventos se pueden almacenar en el archivo de registro de auditoría de pedidos:

    - Eventos de procesamiento de pedidos:
        - LogOrderProcessingStarted(string orderId, string email)
        - LogOrderCompleted(string orderId, decimal amount)
    - Eventos de seguridad:
        - LogSecurityEvent(string eventType, string details)
    - Eventos de validación:
        - LogValidationFailure(string orderId, string reason)
    - Eventos de inventario:
        - LogInventoryIssue(string orderId, string productId, string issue)
        - LogInventoryReserved(string orderId, int itemCount)
    - Eventos de pago:
        - LogPaymentProcessed(string orderId, decimal amount, string reference)
        - LogPaymentFailure(string orderId, string reason)
    - Eventos de envío:
        - LogShippingScheduled(string orderId, string trackingNumber)
        - LogShippingFailure(string orderId, string reason)
    - Eventos de notificación:
        - LogNotificationSent(string orderId, string type)
        - LogNotificationFailure(string orderId, string reason)
    - Errores inesperados:
        - LogUnexpectedError(string orderId, string error)

Las pruebas manuales comprueban que los esfuerzos de refactorización han logrado correctamente el objetivo de mejorar la estructura del código mientras se mantiene la funcionalidad del sistema. El código refactorizado ahora proporciona una base mucho más fácil de mantener donde cada método tiene una responsabilidad clara y centrada, lo que facilita considerablemente la implementación de futuras mejoras y correcciones de errores.

## Resumen

En este ejercicio, ha aprendido a usar GitHub Copilot para refactorizar funciones grandes en una aplicación. Ha explorado el sistema de procesamiento de pedidos de comercio electrónico, ha identificado funciones grandes que necesitan refactorización y ha usado GitHub Copilot para dividir métodos monolíticos en funciones más pequeñas y centradas para mejorar el mantenimiento y la legibilidad.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Si ha realizado algún cambio, reviértalos según sea necesario. Si usa un equipo local como entorno de laboratorio, puede archivar o eliminar la carpeta de proyectos de ejemplo que ha creado para este ejercicio.
