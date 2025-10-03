---
lab:
  title: 'Ejercicio: Implementación de la generación de perfiles de rendimiento mediante GitHub Copilot'
  description: Aprenda a identificar y solucionar cuellos de botella de rendimiento e ineficacias de código mediante herramientas de GitHub Copilot.
---

# Implementación de la generación de perfiles de rendimiento mediante GitHub Copilot

La generación de perfiles de rendimiento es un aspecto importante del desarrollo de software que ayuda a identificar y abordar cuellos de botella de rendimiento e ineficacias del código.

En este ejercicio, revisará un proyecto existente que contiene código de bajo rendimiento e ineficaz, analizará las opciones para mejorar el rendimiento del código, lo refactorizará para solucionar los problemas identificados y probará el código refactorizado para garantizar que su rendimiento ha mejorado al tiempo que conserva la funcionalidad y la legibilidad. Usará GitHub Copilot en el modo Preguntar para comprender un proyecto de código existente y explorar las opciones para refactorizar los problemas identificados. Usará GitHub Copilot en modo Agente para refactorizar el código y mejorar el rendimiento. Probará el código original y refactorizado para medir el impacto de los cambios.

Este ejercicio debería tardar en completarse **30** minutos aproximadamente.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar su propia cuenta de GitHub y suscripción de GitHub Copilot. Si no tiene una cuenta de GitHub, puede <a href="https://github.com/" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

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

    1. Haga clic con el botón derecho en **GHCopilotEx10LabApps.zip** y **seleccione Extraer todo**.

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
            - Data.txt
            - DataAnalyzer.cs
            - FileLoader.cs
            - output.txt
            - Program.cs
            - README.md
            - ReportGenerator.cs

## Escenario del ejercicio

Es desarrollador de software y trabaja para una empresa de consultoría. Los clientes necesitan ayuda para implementar la generación de perfiles de rendimiento en aplicaciones heredadas. El objetivo es mejorar el rendimiento del código a la vez que se conserva la legibilidad y la funcionalidad existente. Se le asigna a la aplicación siguiente:

- ContosoOnlineStore: Se trata de una aplicación de comercio electrónico que procesa los pedidos de los clientes. La aplicación incluye la administración del catálogo de productos con funcionalidades de búsqueda, seguimiento de inventario con reservas de existencias, procesamiento de pedidos con validación y recibos, servicios de notificaciones por correo electrónico y validación de seguridad. La aplicación usa patrones modernos de arquitectura de .NET, como la inserción de dependencias, el registro estructurado y la administración de configuración, pero contiene cuellos de botella de rendimiento que reflejan escenarios reales.

> **NOTA**: Los cuellos de botella en el código incluyen ineficiencias e inconvenientes de rendimiento intencionales, así como retrasos simulados que aproximan el tiempo real de las dependencias externas. Los retrasos simulados deben conservarse cuando se refactoriza el código para permitir comparaciones de rendimiento de "antes y después".

Este ejercicio incluye las siguientes tareas:

1. Revise manualmente el código base de ContosoOnlineStore.
1. Identifique los cuellos de botella de rendimiento mediante GitHub Copilot Chat (modo Preguntar).
1. Refactorice el código crítico para el rendimiento mediante GitHub Copilot Chat (modo Agente).
1. Pruebe y compruebe el código refactorizado de ContosoOnlineStore.

### Revisión manual del código base de ContosoOnlineStore

El primer paso de cualquier esfuerzo de refactorización de código es comprender el código base existente, incluida la estructura del proyecto y la lógica de negocios. Al trabajar en mejoras de rendimiento, también es importante establecer métricas de rendimiento de línea base.

En esta tarea, examinará los componentes principales del proyecto ContosoOnlineStore, ejecutará la aplicación para establecer métricas de rendimiento de línea base e identificará posibles áreas para la optimización.

Realice los pasos siguientes para completar esta tarea:

1. Dedique un minuto a examinar la estructura del proyecto ContosoOnlineStore.

    El código base sigue los patrones modernos de arquitectura de .NET con una separación clara de preocupaciones. Los principales componentes arquitectónicos incluyen los siguientes:

    - **Configuración**: configuración fuertemente tipada con validación
    - **Servicios**: servicios empresariales con interfaces para la capacidad de prueba  
    - **Excepciones**: excepciones personalizadas específicas del dominio
    - **Puntos de referencia**: pruebas de rendimiento profesionales con BenchmarkDotNet
    - **Pruebas**: pruebas unitarias con un marco de trabajo ficticio

1. Dedique unos minutos a revisar las clases **ProductCatalog.cs**, **OrderProcessor.cs** e **InventoryManager.cs**.

    Estas clases contienen la lógica empresarial principal y probablemente son candidatas para la optimización del rendimiento.

    > **NOTA**: El código base incluye comentarios que ayudan a identificar problemas de rendimiento. Busque comentarios marcados como "Cuello de botella de rendimiento" o "Problema de rendimiento" que resalten las ineficacias intencionadas. Los retrasos simulados también se incluyen para aproximar el tiempo real de las dependencias externas (consultas lentas, llamadas de red, etc.). Estos retrasos se conservarán al refactorizar el código base para permitir comparaciones de rendimiento de "antes y después".

    - **ProductCatalog.cs**: la clase ProductCatalog proporciona métodos para recuperar, buscar y clasificar productos, así como para almacenar en caché los resultados de la búsqueda.

    - **OrderProcessor.cs**: la clase OrderProcessor controla la validación de pedidos, el cálculo total y la finalización, incluidas las actualizaciones de inventario y las notificaciones por correo electrónico.

    - **InventoryManager.cs**: la clase InventoryManager administra los niveles de existencias, las reservas y las alertas de existencias bajas.

1. Expanda las carpetas **Servicios** y **Configuración**.

    Estas carpetas contienen opciones de configuración y lógica de negocios adicionales que admiten la funcionalidad principal de la aplicación.

1. Dedique unos minutos a revisar los archivos **Program.cs** y **AppSettings.cs**.

    Examine la relación entre los archivos Program.cs y AppSettings.cs. Observe que el archivo Program.cs inicializa e inserta la configuración de AppSettings en los servicios de la aplicación, lo que permite un control centralizado y flexible sobre el comportamiento de la aplicación. La configuración de la aplicación está fuertemente tipada y validada en el arranque, lo que garantiza que todas las opciones necesarias estén presentes y tengan el formato correcto.

1. Dedique unos minutos a revisar los archivos **EmailService.cs** y **SecurityValidationService.cs**.

    Examine la implementación de estos servicios. Observe que proporcionan lógica de negocios con tiempos de espera configurables, reglas de validación de seguridad y flujos de trabajo de notificación por correo electrónico. Los servicios usan la inserción de dependencias y el registro, de acuerdo a patrones de desarrollo empresarial.

1. Ejecute la aplicación y observe el rendimiento de línea base.

    Puede ejecutar la aplicación desde el terminal integrado de Visual Studio Code; para ello, vaya a la carpeta del proyecto y ejecute el siguiente comando de la CLI de .NET:

    ```bash
    dotnet run
    ```

    La aplicación ejecutará una prueba de rendimiento completa que incluye lo siguiente:

    - Procesamiento de pedidos con medidas de tiempo.
    - Operaciones del catálogo de productos (búsqueda y filtrado de categorías).
    - Operaciones de administración de inventario.
    - Pruebas de operaciones simultáneas.
    - Simulación de notificación por correo electrónico.

1. Almacene las métricas de rendimiento de línea base en un archivo denominado **baseline_metrics.txt**.

    Use la vista EXPLORER para crear un archivo de texto denominado baseline_metrics.txt en la carpeta Benchmarks y, a continuación, copie la salida de la consola en el archivo baseline_metrics.txt.

1. Revise el archivo baseline_metrics.txt.

    Observe la información de tiempo mostrada en la sección *Ejecución del análisis de rendimiento*. Entre las métricas clave de rendimiento se incluyen las siguientes:

    - Rendimiento de la búsqueda de productos.
    - Rendimiento de la búsqueda.
    - Rendimiento del procesamiento de pedidos.
    - Rendimiento de las operaciones de inventario.
    - Rendimiento de operaciones simultáneas.

    La aplicación también ejecuta un conjunto de análisis de rendimiento completo que prueba varios detalles de tiempo de operaciones e informes.

1. Dedique un minuto a examinar las funcionalidades de punto de referencia de rendimiento proporcionadas por el archivo OrderProcessingBenchmarks.cs.

    La aplicación incluye puntos de referencia profesionales mediante BenchmarkDotNet. Para ejecutar puntos de referencia de rendimiento detallados, ejecute lo siguiente:

    ```bash
    dotnet run -c Release -- benchmark
    ```

    Al ejecutar este comando, se generarán informes de rendimiento detallados, incluidos patrones de asignación de memoria y análisis estadístico. Si lo desea, puede guardar los informes detallados de pruebas comparativas de rendimiento para compararlos más tarde.

Comprender la arquitectura existente y las métricas de rendimiento de línea base sirve de preparación a la manera de identificar oportunidades de optimización.

### Identificación de cuellos de botella de rendimiento mediante GitHub Copilot Chat (modo Preguntar)

El modo Preguntar de GitHub Copilot Chat es una excelente herramienta para analizar bases de código complejas e identificar cuellos de botella de rendimiento. En el modo Preguntar, Copilot puede analizar los patrones de código, identificar algoritmos ineficaces y sugerir estrategias de optimización basadas en procedimientos recomendados.

En esta tarea, usará GitHub Copilot para analizar sistemáticamente la aplicación ContosoOnlineStore e identificar oportunidades específicas de mejora del rendimiento.

Realice los pasos siguientes para completar esta tarea:

1. Abra la vista Chat de GitHub Copilot y, después, configure el modo **Preguntar** y el modelo **GPT-4o**.

    Para abrir la vista Chat, seleccione el icono **Activar/desactivar chat** en la parte superior de la ventana de Visual Studio Code.

    > **NOTA**: El modelo GPT-4o proporciona excelentes funcionalidades de análisis de código y se incluye con el plan Gratis de GitHub Copilot. Elegir un modelo diferente puede producir resultados diferentes.

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

1. Revise el análisis generado por GitHub Copilot para la clase ProductCatalog.

    El análisis debe identificar problemas como:

    - Rendimiento de búsqueda lineal en GetProductById para determinadas condiciones.
    - Generación de claves de caché ineficaz en SearchProducts.
    - Faltan estructuras de datos optimizadas para el filtrado de categorías en GetProductsByCategory.
    - Procesamiento secuencial con retrasos artificiales en varios de los métodos.

1. Pida a GitHub Copilot que evalúe las optimizaciones sugeridas para detectar posibles riesgos.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```text
    Do any of the suggested optimizations include security risks or introduce other adverse effects?
    ```

    > **IMPORTANTE**: La adopción ciega de sugerencias de refactorización de código puede introducir riesgos de seguridad y otros problemas. Es importante evaluar las optimizaciones sugeridas e identificar los posibles problemas. Por ejemplo, las optimizaciones que implican el almacenamiento en caché o el procesamiento paralelo pueden presentar problemas de seguridad de subprocesos o problemas de coherencia de datos. Se recomienda revisar el código manualmente para asegurarse de que las optimizaciones sugeridas por IA no ponen en peligro la seguridad ni la funcionalidad. Las revisiones y pruebas de seguridad periódicas deben formar parte de cualquier trabajo de refactorización de código.

1. Revise el análisis de riesgos generado por GitHub Copilot.

    El análisis de riesgos debe resaltar las posibles vulnerabilidades de seguridad u otros problemas asociados a las optimizaciones sugeridas. Esta información le ayuda a tomar decisiones fundamentadas sobre qué optimizaciones implementar al refactorizar el código.

1. Pídale a GitHub Copilot que identifique problemas de rendimiento en la clase OrderProcessor y sugiera optimizaciones.

    Por ejemplo, envíe el mensaje siguiente:

    ```text
    Examine the OrderProcessor class, particularly the CalculateOrderTotal and FinalizeOrderAsync methods. What performance problems do you see and what optimization strategies would you recommend?
    ```

1. Revise el análisis generado por GitHub Copilot para la clase OrderProcessor.

    El análisis debe identificar problemas como:

    - Búsquedas de productos individuales en bucles (patrón de consulta N+1).
    - Cálculo redundante de impuestos y envíos.
    - Procesamiento secuencial de elementos de pedido.
    - Operaciones de bloqueo que se podrían convertir en asincrónicas.

1. Pida a GitHub Copilot que evalúe las optimizaciones sugeridas para detectar posibles riesgos.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```text
    Do any of the suggested optimizations include security risks or introduce other adverse effects?
    ```

1. Revise el análisis de riesgos generado por GitHub Copilot.

1. Pídale a GitHub Copilot que identifique problemas de rendimiento en la clase InventoryManager y sugiera optimizaciones.

    Por ejemplo, use este mensaje para examinar las operaciones de inventario:

    ```text
    Review the InventoryManager class, especially the GetLowStockProducts and UpdateStockLevels methods. What are the performance concerns and how could the inventory operations be improved?
    ```

1. Revise el análisis generado por GitHub Copilot para la clase InventoryManager.

    El análisis debe identificar problemas como:

    - Simulación de consulta de base de datos individual en bucles.
    - Implementación de registro ineficaz con operaciones de bloqueo.
    - Falta compatibilidad con la operación por lotes.
    - Retrasos innecesarios de los subprocesos en las comprobaciones de nivel de existencias.

1. Pida a GitHub Copilot que evalúe las optimizaciones sugeridas para detectar posibles riesgos.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```text
    Do any of the suggested optimizations include security risks or introduce other adverse effects?
    ```

1. Revise el análisis de riesgos generado por GitHub Copilot.

1. Pídale a GitHub Copilot que identifique problemas de rendimiento en la clase EmailService y sugiera optimizaciones.

    Por ejemplo, envíe este mensaje para analizar el servicio de correo electrónico:

    ```text
    Analyze the EmailService class for performance issues. How does the email sending process impact overall application performance and what improvements could be made?
    ```

1. Revise el análisis generado por GitHub Copilot para la clase EmailService.

    El análisis debe identificar problemas como:

    - Generación secuencial de contenido de correo electrónico con operaciones de bloqueo.
    - Búsquedas de productos individuales dentro de plantillas de correo electrónico.
    - Operaciones de validación sincrónicas.
    - Faltan oportunidades de paralelización para varios destinatarios.

1. Pida a GitHub Copilot que evalúe las optimizaciones sugeridas para detectar posibles riesgos.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```text
    Do any of the suggested optimizations include security risks or introduce other adverse effects?
    ```

1. Revise el análisis de riesgos generado por GitHub Copilot.

Con las funcionalidades de análisis de GitHub Copilot, ha identificado cuellos de botella de rendimiento en la aplicación ContosoOnlineStore. El análisis proporciona una hoja de ruta para los esfuerzos de optimización y se centra en mejoras algorítmicas, estrategias de almacenamiento en caché y patrones de procesamiento asincrónicos. El análisis de las optimizaciones de código sugeridas por IA ayuda a identificar los riesgos asociados a posibles mejoras de rendimiento. Las revisiones manuales de código, las revisiones de seguridad y las pruebas deben formar parte de cualquier trabajo de refactorización de código.

### Refactorización del código crítico para el rendimiento mediante GitHub Copilot Chat (modo Agente)

El modo Agente de GitHub Copilot proporciona un agente autónomo que ayuda en las tareas de programación. Los desarrolladores asignan tareas de alto nivel al agente y, a continuación, inician una sesión de edición de código de agente para completar la tarea. El agente de GitHub Copilot evalúa de forma autónoma el trabajo necesario, determina los archivos y el contexto pertinentes y planea cómo completar la tarea. El agente puede realizar cambios en el código, ejecutar pruebas e incluso implementar la aplicación.

En el modo Agente, GitHub Copilot puede generar implementaciones de código optimizadas, sugerir mejoras arquitectónicas y ayudar a implementar mejoras de rendimiento.

En esta tarea, usará el modo Agente de GitHub Copilot para abordar sistemáticamente los cuellos de botella de rendimiento identificados en la tarea anterior.

Realice los pasos siguientes para completar esta tarea:

1. Configure GitHub Copilot Chat para el modo Agente.

    En la vista Chat, cambie el modo de **Preguntar** a **Agente**. El modo Agente proporciona funcionalidades de generación y modificación de código más dirigidas.

1. Abra el archivo **ProductCatalog.cs** y, a continuación, seleccione el método **GetProductById**.

1. Asigne una tarea al agente que optimice el método GetProductById.

    Por ejemplo, escriba la siguiente tarea en la vista Chat:

    ```text
    Review the current chat session. Optimize the GetProductById method to improve performance. Consider using a dictionary lookup instead of linear search and implement proper caching mechanisms. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Dedique un minuto a revisar las modificaciones sugeridas por GitHub Copilot y, a continuación, acepte los cambios.

    La versión optimizada debe incluir lo siguiente:

    - Búsquedas de productos basadas en diccionarios para el rendimiento de O(1).
    - Inicialización y administración de caché adecuadas.
    - Operaciones redundantes reducidas.

    Puede revisar y aceptar (o rechazar) modificaciones individuales en el editor de código, o bien puede aceptar todos los cambios a la vez seleccionando **Conservar** en la vista Chat.

    > **NOTA**: Cuando complete esta sección del ejercicio, tenga en cuenta las vulnerabilidades de seguridad y otros problemas identificados en la tarea anterior. Los desarrolladores deben asegurarse de que no se introduzcan nuevas vulnerabilidades durante el proceso de optimización. En un entorno de producción, las revisiones manuales de código, las revisiones de seguridad y las pruebas deben formar parte del proceso.

1. En el editor de código, seleccione el método **SearchProducts**.

1. Asigne una tarea al agente que mejore la eficacia del método SearchProducts.

    Por ejemplo, escriba la siguiente tarea en la vista Chat:

    ```text
    Review the current chat session. Refactor the SearchProducts method to eliminate performance bottlenecks. Optimize the search algorithm while maintaining search functionality. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Dedique un minuto a revisar las modificaciones sugeridas por GitHub Copilot y, a continuación, acepte los cambios.

    La versión optimizada debe incluir lo siguiente:

    - Algoritmos eficaces de coincidencia de cadenas.
    - Procesamiento paralelo para varios criterios de búsqueda.
    - Generación optimizada de claves de caché.

1. Guarde y cierre el archivo **ProductCatalog.cs**.

1. Abra el archivo **OrderProcessor.cs** y, a continuación, seleccione el método **CalculateOrderTotal**.

1. Asigne una tarea al agente que mejore el rendimiento del método CalculateOrderTotal.

    Por ejemplo, escriba la siguiente tarea en la vista Chat:

    ```text
    Review the current chat session. Optimize the CalculateOrderTotal method to reduce redundant product lookups and improve calculation performance. Consider batch operations and caching strategies. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Dedique un minuto a revisar las modificaciones sugeridas por GitHub Copilot y, a continuación, acepte los cambios.

    La versión optimizada debe incluir lo siguiente:

    - Recuperación de productos por lotes para eliminar los patrones de consulta N+1.
    - Información del producto en caché durante el procesamiento de pedidos.
    - Cálculos optimizados de impuestos y envíos.

1. En el editor de código, seleccione el método **FinalizeOrderAsync**.

1. Asigne una tarea al agente que mejore el rendimiento del método FinalizeOrderAsync.

    Por ejemplo, escriba la siguiente tarea en la vista Chat:

    ```text
    Review the current chat session. Refactor the FinalizeOrderAsync method to improve async performance. Focus on parallel processing where possible and optimizing await patterns. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Dedique un minuto a revisar las modificaciones sugeridas por GitHub Copilot y, a continuación, acepte los cambios.

    La versión optimizada debe incluir lo siguiente:

    - Procesamiento paralelo de operaciones independientes
    - Uso optimizado de async/await
    - Mejor control de excepciones en contextos asincrónicos

1. Guarde y cierre el archivo **OrderProcessor.cs**.

1. Abra el archivo **InventoryManager.cs** y seleccione el método **UpdateStockLevels**.

1. Asigne una tarea al agente que mejore el rendimiento del método UpdateStockLevels.

    Por ejemplo, escriba la siguiente tarea en la vista Chat:

    ```text
    Review the current chat session. Optimize the UpdateStockLevels method to support batch operations and reduce individual update overhead. Implement efficient logging, but retain any existing artificial delays for performance comparison. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Dedique un minuto a revisar las modificaciones sugeridas por GitHub Copilot y, a continuación, acepte los cambios.

    La versión optimizada debe incluir lo siguiente:

    - Actualizaciones de nivel de existencias por lotes
    - Estrategias de registro eficaces
    - Reducción de operaciones de bloqueo

1. Guarde y cierre el archivo **OrderProcessor.cs**.

1. Abra el archivo **EmailService.cs**.

1. Asigne una tarea al agente que mejore el rendimiento de los métodos de envío de correo electrónico.

1. Mejore el procesamiento asincrónico de EmailService.

    Por ejemplo, escriba la siguiente tarea en la vista Chat:

    ```text
    Review the current chat session. Optimize the email service methods to support parallel email processing and improve async performance. Consider implementing email queuing and batch operations. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Dedique un minuto a revisar las modificaciones sugeridas por GitHub Copilot y, a continuación, acepte los cambios.

    La versión optimizada debe incluir lo siguiente:

    - Generación de contenido de correo electrónico en paralelo
    - Operaciones asincrónicas de envío de correo electrónico
    - Mejora del control de errores y la lógica de reintento

A lo largo de este proceso de refactorización, el modo Agente de GitHub Copilot actúa como asociado de colaboración, lo que proporciona mejoras de código específicas y estrategias de optimización. La clave es revisar cuidadosamente cada sugerencia y adaptarla para ajustarla a los requisitos específicos y estándares de codificación.

### Prueba y comprobación del código refactorizado de ContosoOnlineStore

Después de implementar las optimizaciones de rendimiento, es fundamental validar que los cambios mejoran el rendimiento al tiempo que mantienen la corrección funcional. Esta tarea se centra en la realización de pruebas completas y la medición del rendimiento.

Realice los pasos siguientes para completar esta tarea:

1. Compile y ejecute la aplicación refactorizada.

    Ejecute el comando siguiente en el terminal de Visual Studio Code para asegurarse de que la aplicación se compila correctamente:

    ```bash
    dotnet build
    ```

    Solucione los errores de compilación que se puedan haber introducido durante el proceso de refactorización.

1. Ejecute el conjunto de pruebas de rendimiento.

    Ejecute el siguiente comando en el terminal de Visual Studio Code para generar métricas de rendimiento para el código refactorizado:

    ```bash
    dotnet run
    ```

1. Guarde las nuevas métricas de rendimiento en un archivo denominado **optimized_metrics.txt**.

    Use la vista EXPLORER para crear un archivo de texto denominado optimized_metrics.txt en la carpeta Benchmarks y, a continuación, copie la salida de la consola en el archivo optimized_metrics.txt.

1. Dedique un minuto a comparar manualmente las métricas de rendimiento optimizadas con las medidas de línea base de la primera tarea.

    Debe observar las siguientes mejoras de rendimiento:

    - Operaciones de búsqueda de productos bastante más rápidas.
    - Rendimiento de búsqueda mejorado.
    - Tiempo de procesamiento de pedidos reducido.
    - Rendimiento mejorado de las operaciones simultáneas.

    Compruebe la corrección funcional del código refactorizado.

    - Compruebe que los totales de pedidos se calculan correctamente.
    - Confirme que los niveles de inventario se actualizan correctamente.
    - Compruebe que las notificaciones por correo electrónico se envían correctamente.
    - Compruebe que la validación de seguridad todavía funciona.

1. Compile y ejecute el proyecto de prueba unitaria.

    Por ejemplo, en el terminal de Visual Studio Code, vaya a la carpeta **ContosoOnlineStore.Tests** y ejecute el siguiente comando:

    ```bash
    dotnet test
    ```

    Todas las pruebas deben superarse, lo que confirma que el código refactorizado mantiene el comportamiento esperado.

    La salida debe tener una apariencia similar a la siguiente:

    ```plaintext
    Restore complete (0.6s)
      ContosoOnlineStore succeeded (0.6s) → C:\Users\cahowd\Desktop\GHCopilotEx10LabApps\ContosoOnlineStore\bin\Debug\net9.0\ContosoOnlineStore.dll
      ContosoOnlineStore.Tests succeeded (0.2s) → bin\Debug\net9.0\ContosoOnlineStore.Tests.dll
    [xUnit.net 00:00:00.00] xUnit.net VSTest Adapter v2.4.5+1caef2f33e (64-bit .NET 9.0.9)
    [xUnit.net 00:00:02.94]   Discovering: ContosoOnlineStore.Tests
    [xUnit.net 00:00:03.02]   Discovered:  ContosoOnlineStore.Tests
    [xUnit.net 00:00:03.02]   Starting:    ContosoOnlineStore.Tests
    [xUnit.net 00:00:03.18]   Finished:    ContosoOnlineStore.Tests
      ContosoOnlineStore.Tests test succeeded (4.7s)
    
    Test summary: total: 16, failed: 0, succeeded: 16, skipped: 0, duration: 4.7s
    Build succeeded in 7.0s
    ```

1. Pida a GitHub Copilot que ayude a analizar las mejoras de rendimiento.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```text
    Compare the baseline_metrics.txt and optimized_metrics.txt files. Summarize the performance improvements achieved through the optimizations. Review the codebase and calculate the time associated with simulated delays for each performance test. Subtract the time associated with simulated delays from the performance data and summarize the impact of code optimizations.
    ```

1. Dedique un minuto a revisar el análisis (mejoras de rendimiento) generado por GitHub Copilot.

    El análisis debe resaltar las mejoras de rendimiento específicas logradas a través de las optimizaciones, excepto el impacto de los retrasos simulados. Esto proporciona una imagen más clara de la eficacia de los cambios en el código.

1. Opcional: si ejecutó el conjunto de pruebas comparativas de rendimiento detalladas al principio de este ejercicio y guardó los resultados, puede volver a ejecutar la prueba comparativa de rendimiento detallada y pedir a GitHub Copilot que compare los resultados.

    Para ejecutar las pruebas comparativas de rendimiento detalladas, ejecute el siguiente comando en el terminal de Visual Studio Code:

    ```bash
    dotnet run -c Release -- benchmark
    ```

    Pida a GitHub Copilot que le ayude a revisar los informes de BenchmarkDotNet.

El proceso de prueba y comprobación confirma que los esfuerzos de optimización del rendimiento se han realizado correctamente. La aplicación ContosoOnlineStore ahora muestra un rendimiento mejorado al tiempo que conserva sus requisitos funcionales y la integridad de la arquitectura.

## Resumen

En este ejercicio, ha usado correctamente GitHub Copilot para identificar y resolver cuellos de botella de rendimiento en una aplicación compleja de comercio electrónico. Entre los principales logros se incluyen los siguientes:

- **Análisis de rendimiento**: Se ha usado el modo Preguntar de GitHub Copilot para analizar sistemáticamente el código e identificar cuellos de botella
- **Optimización estratégica**: Se han aplicado optimizaciones dirigidas que abordan patrones de consulta N+1, algoritmos ineficaces y operaciones de bloqueo
- **Refactorización colaborativa**: Se ha aprovechado el modo Agente de GitHub Copilot para implementar mejoras de rendimiento
- **Validación**: Se han confirmado las mejoras de rendimiento y la corrección funcional mediante pruebas completas

La aplicación ContosoOnlineStore optimizada muestra mejoras de rendimiento significativas al tiempo que mantiene los procedimientos recomendados de calidad de código y arquitectura. Este enfoque muestra cómo las herramientas de desarrollo con tecnología de inteligencia artificial pueden acelerar los esfuerzos de optimización del rendimiento y ayudar a los desarrolladores a realizar mejoras controladas por datos en aplicaciones complejas.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Si ha realizado algún cambio, reviértalos según sea necesario. Si usa un equipo local como entorno de laboratorio, puede archivar o eliminar la carpeta de proyectos de ejemplo que ha creado para este ejercicio.
