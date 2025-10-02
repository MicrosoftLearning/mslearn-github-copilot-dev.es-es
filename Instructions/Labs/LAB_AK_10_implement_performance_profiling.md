<!-- ---
lab:
    title: 'Exercise - Implement performance profiling using GitHub Copilot'
    description: 'Learn how to identify and address performance bottlenecks and code inefficiencies using GitHub Copilot tools.'
--- -->

# Implementación de la generación de perfiles de rendimiento mediante GitHub Copilot

La generación de perfiles de rendimiento es un aspecto importante del desarrollo de software que ayuda a identificar y abordar cuellos de botella de rendimiento e ineficacias del código.

En este ejercicio, revisará un proyecto existente que contiene código de bajo rendimiento e ineficaz, analizará las opciones para mejorar el rendimiento del código, lo refactorizará para solucionar los problemas identificados y probará el código refactorizado para garantizar que su rendimiento ha mejorado al tiempo que conserva la funcionalidad y la legibilidad. Usará GitHub Copilot en el modo Preguntar para comprender un proyecto de código existente y explorar las opciones para refactorizar los problemas identificados. Usará GitHub Copilot en modo Agente para refactorizar el código y mejorar el rendimiento. Probará el código original y refactorizado para medir el impacto de los cambios.

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

1. Para descargar un archivo ZIP que contenga los proyectos de aplicación de ejemplo, abra la URL siguiente en el explorador: [Laboratorio de GitHub Copilot: Implementación de la generación de perfiles de rendimiento](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/GHCopilotEx10LabApps.zip)

    El archivo ZIP se denomina **GHCopilotEx10LabApps.zip**.

1. Extraiga los archivos del archivo **GHCopilotEx10LabApps.zip**.

    Por ejemplo:

    1. Vaya a la carpeta de descargas del entorno de laboratorio.

    1. Haga clic con el botón derecho en *GHCopilotEx10LabApps.zip* y **seleccione Extraer todo**.

    1. Seleccione **Mostrar los archivos extraídos al completar** y, a continuación, **Extraer**.

1. Copia la carpeta **GHCopilotEx10LabApps** en una ubicación que sea fácil de acceder, como la carpeta Escritorio de Windows.

1. Abra la carpeta **GHCopilotEx10LabApps** en Visual Studio Code.

    Por ejemplo:

    1. Abra Visual Studio Code en el entorno de laboratorio.

    1. En Visual Studio Code, en el menú **Archivo**, seleccione **Abrir archivo**.

    1. Vaya a la carpeta Escritorio de Windows, seleccione **GHCopilotEx10LabApps** y luego **Seleccionar carpeta**.

1. En la vista EXPLORADOR DE SOLUCIONES de Visual Studio Code, compruebe la siguiente estructura del proyecto:

    - GHCopilotEx10LabApps\
        - ContosoOnlineStore\
            - Benchmarks\
            - Configuration\
            - Exceptions\
            - Services\
            - appsettings.json
            - InventoryManager.cs
            - Orders.cs
            - OrderItem.cs
            - OrderProcessor.cs
            - PERFORMANCE_GUIDE.md
            - Product.cs
            - ProductCatalog.cs
            - Program.cs
            - README.md
        - ContosoOnlineStore.Tests\
            - ContosoOnlineStoreTests.cs
            - Usings.cs
        - DataAnalyzerReporter\

## Escenario del ejercicio

Es desarrollador de software y trabaja para una empresa de consultoría. Los clientes necesitan ayuda para implementar la generación de perfiles de rendimiento en aplicaciones heredadas. El objetivo es mejorar el rendimiento del código a la vez que se conserva la legibilidad y la funcionalidad existente. Se le asigna a la aplicación siguiente:

- ContosoOnlineStore: Se trata de una aplicación de comercio electrónico que procesa los pedidos de los clientes con una complejidad empresarial realista. La aplicación incluye la administración del catálogo de productos con funcionalidades de búsqueda, seguimiento de inventario con reservas de existencias, procesamiento de pedidos con validación y recibos, servicios de notificaciones por correo electrónico y validación de seguridad. La aplicación usa patrones modernos de arquitectura de .NET, como la inserción de dependencias, el registro estructurado y la administración de configuración, pero contiene cuellos de botella de rendimiento que reflejan escenarios reales.

Este ejercicio incluye las siguientes tareas:

1. Revise manualmente el código base de ContosoOnlineStore.
1. Identifique los cuellos de botella de rendimiento mediante GitHub Copilot Chat (modo Preguntar).
1. Refactorice el código crítico para el rendimiento mediante GitHub Copilot Chat (modo Agente).
1. Pruebe y compruebe el código refactorizado de ContosoOnlineStore.

### Revisión manual del código base de ContosoOnlineStore

El primer paso de cualquier esfuerzo de refactorización de código es comprender el código base existente, incluida la estructura del proyecto y la lógica de negocios. Al trabajar en mejoras de rendimiento, también es importante establecer métricas de rendimiento de línea base.

En esta tarea, examinará los componentes principales del proyecto ContosoOnlineStore, ejecutará la aplicación para establecer métricas de rendimiento de línea base e identificará posibles áreas para la optimización.

Realice los pasos siguientes para completar esta tarea:

1. Dedique unos minutos a revisar la estructura del proyecto ContosoOnlineStore.

    El código base sigue los patrones modernos de arquitectura de .NET con una separación clara de preocupaciones. Los principales componentes arquitectónicos incluyen los siguientes:

    - **Configuración**: configuración fuertemente tipada con validación
    - **Servicios**: servicios empresariales con interfaces para la capacidad de prueba  
    - **Excepciones**: excepciones personalizadas específicas del dominio
    - **Puntos de referencia**: pruebas de rendimiento profesionales con BenchmarkDotNet
    - **Pruebas**: pruebas unitarias con un marco de trabajo ficticio

1. Examine las principales clases de lógica de negocios.

    Abra **ProductCatalog.cs**, **OrderProcessor.cs** e **InventoryManager.cs**. Estas clases contienen la lógica empresarial principal y probablemente son candidatas para la optimización del rendimiento.

    Observe la lista de datos de productos (20 productos con categorías y descripciones), el flujo de trabajo complejo de procesamiento de pedidos y la administración del inventario con reservas de existencias.

    > **NOTA**: El código base incluye comentarios que ayudan a identificar problemas de rendimiento. Busque comentarios marcados como "Cuello de botella de rendimiento" o "Problema de rendimiento" que resalten las ineficacias intencionadas.

1. Revise la capa de servicios y la configuración.

    Vaya a la carpeta **Services** y examine **EmailService.cs** y **SecurityValidationService.cs**. Revise también el archivo **Configuration/AppSettings.cs**.

    Observará que estos servicios implementan lógica de negocios realista con tiempos de espera configurables, reglas de validación de seguridad y flujos de trabajo de notificación por correo electrónico. Los servicios usan la inserción de dependencias y el registro, de acuerdo a patrones de desarrollo empresarial.

1. Ejecute la aplicación y observe el rendimiento de línea base.

    Puede ejecutar la aplicación desde el terminal integrado de Visual Studio Code; para ello, vaya a la carpeta del proyecto y ejecute el siguiente comando de la CLI de .NET:

    ```bash
    dotnet run
    ```

    La aplicación ejecutará una prueba de rendimiento completa que incluye lo siguiente:

    - Procesamiento de pedidos con medidas de tiempo
    - Operaciones del catálogo de productos (búsqueda y filtrado de categorías)
    - Operaciones de administración de inventario
    - Pruebas de operaciones simultáneas
    - Simulación de notificación por correo electrónico

1. Almacene las métricas de rendimiento de línea base en un archivo denominado **baseline_metrics.txt**.

    Cree un archivo de texto denominado baseline_metrics.txt. Copie la salida de la consola en el archivo baseline_metrics.txt.

    Preste atención a la información de tiempo mostrada en la salida de la consola, como:

    - Tiempo de procesamiento de pedidos (normalmente 2000-3000 ms para un solo pedido)
    - Rendimiento de búsqueda de productos (tiempo de operación individual)
    - Duración de la operación de búsqueda
    - Intervalos de comprobación de inventario
    - Rendimiento de operaciones simultáneas

    La aplicación también ejecuta un conjunto de análisis de rendimiento completo que prueba varios detalles de tiempo de operaciones e informes.

1. Dedique un minuto a examinar las funcionalidades de punto de referencia de rendimiento proporcionadas por el archivo OrderProcessingBenchmarks.cs.

    La aplicación incluye puntos de referencia profesionales mediante BenchmarkDotNet. Para ejecutar puntos de referencia de rendimiento detallados, ejecute lo siguiente:

    ```bash
    dotnet run -c Release -- benchmark
    ```

    Esto generará informes de rendimiento detallados, incluidos los patrones de asignación de memoria y el análisis estadístico.

Comprender la arquitectura existente y las métricas de rendimiento de línea base proporciona la base para identificar oportunidades de optimización. La aplicación muestra desafíos realistas de rendimiento del comercio electrónico que abordará en las tareas posteriores.

### Identificación de cuellos de botella de rendimiento mediante GitHub Copilot Chat (modo Preguntar)

El modo Preguntar de GitHub Copilot Chat es una excelente herramienta para analizar bases de código complejas e identificar cuellos de botella de rendimiento. En el modo Preguntar, Copilot puede analizar los patrones de código, identificar algoritmos ineficaces y sugerir estrategias de optimización basadas en procedimientos recomendados.

En esta tarea, usará GitHub Copilot para analizar sistemáticamente la aplicación ContosoOnlineStore e identificar oportunidades específicas de mejora del rendimiento.

Realice los pasos siguientes para completar esta tarea:

1. Abra la vista Chat de GitHub Copilot y, después, configure el modo Preguntar y el modelo GPT-4o.

    Si la vista Chat aún no está abierta, seleccione el icono **Chat** situado en la parte superior de la ventana de Visual Studio Code. Asegúrese de que el modo de chat está establecido en **Preguntar** y use el modelo **GPT-4o**.

    > **NOTA**: El modelo GPT-4o proporciona excelentes funcionalidades de análisis de código y se recomienda para esta tarea de análisis de rendimiento.

1. Cierre todos los archivos que haya abierto en el editor.

    GitHub Copilot usa archivos que se abren en el editor para establecer el contexto. Tener abiertos solo los archivos de destino ayuda a centrar el análisis en el código que se quiere optimizar.

1. Agregue los archivos **InventoryManager.cs**, **OrderProcessor.cs** y **ProductCatalog.cs** al contexto de Chat.

    Use una operación de arrastrar y colocar para agregar **InventoryManager.cs**, **OrderProcessor.cs** y **ProductCatalog.cs** desde el EXPLORADOR DE SOLUCIONES al contexto de Chat.

    Agregar archivos al contexto de chat indica a GitHub Copilot que los incluya al analizar los mensajes, lo que mejora la precisión y relevancia de su análisis.

1. Pídale a GitHub Copilot que identifique cuellos de botella de rendimiento en la clase ProductCatalog y sugiera optimizaciones.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```text
    Analyze the ProductCatalog class for performance bottlenecks. Focus on the GetProductById, SearchProducts, and GetProductsByCategory methods. What are the main inefficiencies and how could they be optimized?
    ```

    Revise el análisis de GitHub Copilot, que debe identificar problemas como los siguientes:

    - Rendimiento de búsqueda lineal en GetProductById para determinadas condiciones.
    - Generación de claves de caché ineficaz en SearchProducts.
    - Faltan estructuras de datos optimizadas para el filtrado de categorías en GetProductsByCategory.
    - Procesamiento secuencial con retrasos artificiales en varios de los métodos.

1. Pídale a GitHub Copilot que identifique problemas de rendimiento en la clase OrderProcessor y sugiera optimizaciones.

    Por ejemplo, envíe el mensaje siguiente:

    ```text
    Examine the OrderProcessor class, particularly the CalculateOrderTotal and FinalizeOrderAsync methods. What performance problems do you see and what optimization strategies would you recommend?
    ```

    GitHub Copilot debe identificar problemas, incluidos los siguientes:

    - Búsquedas de productos individuales en bucles (patrón de consulta N+1).
    - Cálculo redundante de impuestos y envíos.
    - Procesamiento secuencial de elementos de pedido.
    - Operaciones de bloqueo que se podrían convertir en asincrónicas.

1. Pídale a GitHub Copilot que identifique problemas de rendimiento en la clase InventoryManager y sugiera optimizaciones.

    Por ejemplo, use este mensaje para examinar las operaciones de inventario:

    ```text
    Review the InventoryManager class, especially the GetLowStockProducts and UpdateStockLevels methods. What are the performance concerns and how could the inventory operations be improved?
    ```

    El análisis debe revelar lo siguiente:

    - Simulación de consulta de base de datos individual en bucles.
    - Implementación de registro ineficaz con operaciones de bloqueo.
    - Falta compatibilidad con la operación por lotes.
    - Retrasos innecesarios de los subprocesos en las comprobaciones de nivel de existencias.

1. Pídale a GitHub Copilot que identifique problemas de rendimiento en la clase EmailService y sugiera optimizaciones.

    Por ejemplo, envíe este mensaje para analizar el servicio de correo electrónico:

    ```text
    Analyze the EmailService class for performance issues. How does the email sending process impact overall application performance and what improvements could be made?
    ```

    GitHub Copilot debe identificar lo siguiente:

    - Generación secuencial de contenido de correo electrónico con operaciones de bloqueo.
    - Búsquedas de productos individuales dentro de plantillas de correo electrónico.
    - Operaciones de validación sincrónicas.
    - Faltan oportunidades de paralelización para varios destinatarios.

Con las funcionalidades analíticas de GitHub Copilot, ha identificado los principales cuellos de botella de rendimiento en la aplicación ContosoOnlineStore. El análisis proporciona una hoja de ruta para los esfuerzos de optimización y se centra en mejoras algorítmicas, estrategias de almacenamiento en caché y patrones de procesamiento asincrónicos.

### Refactorización del código crítico para el rendimiento mediante GitHub Copilot Chat (modo Agente)

El modo Agente de GitHub Copilot proporciona un agente autónomo que ayuda en las tareas de programación. Los desarrolladores asignan tareas generales y, después, inician una sesión de edición de código con agente para realizar la tarea. En el modo de agente, Copilot planea de forma autónoma el trabajo necesario y determina los archivos y el contexto pertinentes. El agente puede realizar cambios en el código, ejecutar pruebas e incluso implementar la aplicación.

En el modo Agente, GitHub Copilot puede generar implementaciones de código optimizadas, sugerir mejoras arquitectónicas y ayudar a implementar mejoras de rendimiento.

En esta tarea, usará el modo Agente de GitHub Copilot para abordar sistemáticamente los cuellos de botella de rendimiento identificados en la tarea anterior.

Realice los pasos siguientes para completar esta tarea:

1. Configure GitHub Copilot Chat para el modo Agente.

    En la vista Chat, cambie el modo de **Preguntar** a **Agente**. El modo Agente proporciona funcionalidades de generación y modificación de código más dirigidas.

1. Asigne una tarea al agente que optimice el método GetProductById de la clase ProductCatalog.

    Abra **ProductCatalog.cs** y seleccione el método **GetProductById**. Use el mensaje siguiente en Chat:

    ```text
    Optimize this GetProductById method to improve performance. Consider using a dictionary lookup instead of linear search and implement proper caching mechanisms. Retain any existing artificial/simulated delays for "before and after" performance comparisons.
    ```

    Revise las mejoras sugeridas de GitHub Copilot e implemente los cambios. La versión optimizada debe incluir lo siguiente:

    - Búsquedas de productos basadas en diccionarios para el rendimiento de O(1).
    - Inicialización y administración de caché adecuadas.
    - Operaciones redundantes reducidas.

1. Asigne una tarea al agente que mejore la eficacia del método SearchProducts.

    Seleccione el método **SearchProducts** en **ProductCatalog.cs** y use este mensaje:

    ```text
    Refactor the SearchProducts method to eliminate performance bottlenecks. Optimize the search algorithm and remove unnecessary delays while maintaining search functionality. Retain any existing artificial/simulated delays for "before and after" performance comparisons.
    ```

    Aplique las sugerencias de GitHub Copilot para implementar lo siguiente:

    - Algoritmos eficaces de coincidencia de cadenas.
    - Procesamiento paralelo para varios criterios de búsqueda.
    - Generación optimizada de claves de caché.

1. Asigne una tarea al agente que mejore el rendimiento del método CalculateOrderTotal en la clase OrderProcessor.

    Abra **OrderProcessor.cs** y seleccione el método **CalculateOrderTotal**. Envíe este mensaje:

    ```text
    Optimize the CalculateOrderTotal method to reduce redundant product lookups and improve calculation performance. Consider batch operations and caching strategies. Retain any existing artificial/simulated delays for "before and after" performance comparisons.
    ```

    Implemente las mejoras sugeridas, que deben incluir lo siguiente:

    - Recuperación de productos por lotes para eliminar los patrones de consulta N+1.
    - Información del producto en caché durante el procesamiento de pedidos.
    - Cálculos optimizados de impuestos y envíos.

1. Optimice el método FinalizeOrderAsync.

    Seleccione el método **FinalizeOrderAsync** en **OrderProcessor.cs** y use este mensaje:

    ```text
    Refactor the FinalizeOrderAsync method to improve async performance. Focus on parallel processing where possible and optimizing await patterns. Retain any existing artificial/simulated delays for "before and after" performance comparisons.
    ```

    Aplique los cambios sugeridos para conseguir lo siguiente:

    - Procesamiento paralelo de operaciones independientes
    - Uso optimizado de async/await
    - Mejor control de excepciones en contextos asincrónicos

1. Mejore las operaciones por lotes de InventoryManager.

    Abra **InventoryManager.cs** y seleccione el método **UpdateStockLevels**. Use este mensaje:

    ```text
    Optimize the UpdateStockLevels method to support batch operations and reduce individual update overhead. Implement efficient logging, but retain any existing artificial delays for performance comparison.
    ```

    Implemente las mejoras para incluir los siguientes:

    - Actualizaciones de nivel de existencias por lotes
    - Estrategias de registro eficaces
    - Reducción de operaciones de bloqueo

1. Mejore el procesamiento asincrónico de EmailService.

    Abra **Services/EmailService.cs** y seleccione los métodos de envío de correo electrónico. Envíe este mensaje:

    ```text
    Optimize the email service to support parallel email processing and improve async performance. Consider implementing email queuing and batch operations. Retain any existing artificial/simulated delays for "before and after" performance comparisons.
    ```

    Aplique las optimizaciones sugeridas para lo siguiente:

    - Generación de contenido de correo electrónico en paralelo
    - Operaciones asincrónicas de envío de correo electrónico
    - Mejora del control de errores y la lógica de reintento

A lo largo de este proceso de refactorización, el modo Agente de GitHub Copilot actúa como asociado de colaboración, lo que proporciona mejoras de código específicas y estrategias de optimización. La clave es revisar cuidadosamente cada sugerencia y adaptarla para ajustarla a los requisitos específicos y estándares de codificación.

### Prueba y comprobación del código refactorizado de ContosoOnlineStore

Después de implementar las optimizaciones de rendimiento, es fundamental validar que los cambios mejoran el rendimiento al tiempo que mantienen la corrección funcional. Esta tarea se centra en la realización de pruebas completas y la medición del rendimiento.

Realice los pasos siguientes para completar esta tarea:

1. Compile y pruebe la aplicación refactorizada.

    Ejecute los siguientes comandos en el terminal de Visual Studio Code para asegurarse de que la aplicación se compila correctamente:

    ```bash
    dotnet build
    ```

    Solucione los errores de compilación que se puedan haber introducido durante el proceso de refactorización.

1. Ejecute el conjunto de pruebas de rendimiento.

    Ejecute la aplicación para medir las mejoras de rendimiento:

    ```bash
    dotnet run
    ```

    Compare las nuevas métricas de rendimiento con las medidas de línea base de la primera tarea. Debería observar lo siguiente:

    - Tiempo de procesamiento de pedidos significativamente reducido (de 2000-3000 ms a menos de 500 ms)
    - Operaciones de búsqueda de productos más rápidas
    - Rendimiento de búsqueda mejorado
    - Mejores tiempos de respuesta de administración de inventario

1. Ejecute el conjunto de puntos de referencia completo.

    Ejecute los puntos de referencia detallados para obtener medidas precisas:

    ```bash
    dotnet run -c Release -- benchmark
    ```

    Revise los informes de BenchmarkDotNet, que proporcionan estadísticas detalladas, entre las que se incluyen las siguientes:

    - Tiempos de ejecución medios con intervalos de confianza
    - Patrones de asignación de memoria
    - Medidas de rendimiento
    - Importancia estadística de las mejoras

1. Valide la corrección funcional.

    Asegúrese de que las optimizaciones no han introducido regresiones funcionales:

    - Comprobación de que los totales de pedidos se calculan correctamente
    - Confirmación de que los niveles de inventario se actualizan correctamente
    - Prueba de que las notificaciones por correo electrónico se envían correctamente
    - Comprobación de que la validación de seguridad sigue funcionando

1. Ejecute el conjunto de pruebas unitarias.

    Ejecute las pruebas unitarias existentes para garantizar la corrección del código:

    ```bash
    dotnet test
    ```

    Todas las pruebas deben superarse, lo que confirma que el código refactorizado mantiene el comportamiento esperado.

1. Documente las mejoras de rendimiento.

    Use GitHub Copilot para ayudar a documentar los cambios. Envíe este mensaje en Chat:

    ```text
    Help me create a summary of the performance optimizations implemented in this ContosoOnlineStore project. Include before/after metrics and the main optimization strategies used.
    ```

    Cree un informe de mejora del rendimiento que incluya lo siguiente:

    - Métricas de rendimiento optimizadas frente a las de línea base
    - Técnicas de optimización de claves aplicadas
    - Áreas de mejora más significativas
    - Recomendaciones para futuras mejoras

El proceso de prueba y comprobación confirma que los esfuerzos de optimización del rendimiento se han realizado correctamente. La aplicación ContosoOnlineStore ahora muestra un rendimiento significativamente mejorado mientras mantiene sus requisitos funcionales e integridad arquitectónica.

A través de este ejercicio, ha aprendido a usar GitHub Copilot como una herramienta eficaz para el análisis y la optimización del rendimiento, lo que demuestra el valor del desarrollo asistido por IA para abordar desafíos complejos de rendimiento.

## Resumen

En este ejercicio, ha usado correctamente GitHub Copilot para identificar y resolver cuellos de botella de rendimiento en una aplicación compleja de comercio electrónico. Entre los principales logros se incluyen los siguientes:

- **Análisis de rendimiento**: Se ha usado el modo Preguntar de GitHub Copilot para analizar sistemáticamente el código e identificar cuellos de botella
- **Optimización estratégica**: Se han aplicado optimizaciones dirigidas que abordan patrones de consulta N+1, algoritmos ineficaces y operaciones de bloqueo
- **Refactorización colaborativa**: Se ha aprovechado el modo Agente de GitHub Copilot para implementar mejoras de rendimiento
- **Validación**: Se han confirmado las mejoras de rendimiento y la corrección funcional mediante pruebas completas

La aplicación ContosoOnlineStore optimizada muestra mejoras de rendimiento significativas al tiempo que mantiene los procedimientos recomendados de calidad de código y arquitectura. Este enfoque muestra cómo las herramientas de desarrollo con tecnología de inteligencia artificial pueden acelerar los esfuerzos de optimización del rendimiento y ayudar a los desarrolladores a realizar mejoras controladas por datos en aplicaciones complejas.
