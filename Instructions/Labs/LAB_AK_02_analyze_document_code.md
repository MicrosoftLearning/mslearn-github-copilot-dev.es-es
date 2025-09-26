---
lab:
  title: 'Ejercicio: Análisis y documentación de código mediante GitHub Copilot'
  description: "Obtenga información sobre cómo analizar código nuevo o desconocido, y cómo generar documentación mediante GitHub\_Copilot en Visual\_Studio Code."
---

# Análisis y documentación de código mediante GitHub Copilot

GitHub Copilot puede ayudarle a comprender y documentar un código base mediante la generación de explicaciones y documentación. En este ejercicio, usará GitHub Copilot para analizar un código base y generar documentación para el proyecto.

Este ejercicio debería tardar aproximadamente **20** minutos en completarse.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar su propia cuenta de GitHub y suscripción de GitHub Copilot. Si no tiene una cuenta de GitHub, puede <a href="https://github.com/" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

## Antes de comenzar

El entorno de laboratorio debe incluir lo siguiente: Git 2.48 o posterior, SDK de .NET 9.0 o posterior, Visual Studio Code con la extensión Kit de desarrollo de C# y acceso a una cuenta de GitHub con GitHub Copilot habilitado.

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

## Escenario del ejercicio

Es un desarrollador que trabaja en el departamento de TI de la comunidad local. Los sistemas de back-end que admiten la biblioteca pública se han perdido en un incendio. El equipo debe desarrollar una solución temporal para ayudar al personal de la biblioteca a administrar sus operaciones hasta que se pueda reemplazar el sistema. El equipo ha elegido GitHub Copilot para acelerar el proceso de desarrollo.

Su compañero ha desarrollado una versión inicial de la aplicación de biblioteca, pero debido a restricciones de tiempo, no ha tenido la oportunidad de documentar el código. Debe analizar el código base y crear documentación para el proyecto.

Este ejercicio incluye las siguientes tareas:

- Configure la aplicación de biblioteca en Visual Studio Code.
- Use GitHub Copilot para explicar el código base de la aplicación de biblioteca.
- Usar GitHub Copilot para crear un archivo README.md para la aplicación de biblioteca.

## Configurar la aplicación de biblioteca en Visual Studio Code

Su compañero ha desarrollado una versión inicial de la aplicación de la biblioteca y la ha puesto a su disposición como archivo .zip. Debe descargar el archivo ZIP, extraer los archivos de código y, después, abrir la solución en Visual Studio Code.

Siga estos pasos para configurar la aplicación de la biblioteca:

1. Abra una ventana del explorador en el entorno de laboratorio.

1. Para descargar un archivo ZIP con la aplicación de biblioteca, pegue la siguiente dirección URL en la barra de direcciones del explorador: [Laboratorio de GitHub Copilot: Análisis y documentación de código](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/AZ2007LabAppM2.zip)

    El archivo ZIP denominado AZ2007LabAppM2.zip se descargará en el entorno de laboratorio.

1. Extraiga los archivos del archivo **AZ2007LabAppM2.zip**.

    Por ejemplo:

    1. Vaya a la carpeta de descargas del entorno de laboratorio.

    1. Haga clic con el botón derecho en **AZ2007LabAppM2.zip** y seleccione **Extraer todo**.

    1. Seleccione **Mostrar los archivos extraídos al completar** y, a continuación, **Extraer**.

1. Abra la carpeta de archivos extraídos y, después, copie la carpeta **AccelerateDevGHCopilot** en una ubicación que sea fácil de acceder, como la carpeta Escritorio de Windows.

1. Abra la carpeta **AccelerateDevGHCopilot** en Visual Studio Code.

    Por ejemplo:

    1. Abra Visual Studio Code en el entorno de laboratorio.

    1. En Visual Studio Code, en el menú **Archivo**, seleccione **Abrir archivo**.

    1. Vaya a la carpeta Escritorio de Windows, seleccione **AccelerateDevGHCopilot** y luego **Seleccionar carpeta**.

1. En la vista EXPLORADOR DE SOLUCIONES de Visual Studio Code, expanda la solución para mostrar la siguiente estructura de soluciones:

    - AccelerateDevGHCopilot\
        - src\
            - Library.ApplicationCore\
            - Library.Console\
            - Library.Infrastructure\
        - tests\
            - UnitTests\

1. Asegúrese de que la solución se compila correctamente.

    Por ejemplo, en la vista EXPLORADOR DE SOLUCIONES, haga clic con el botón derecho en **AccelerateDevGHCopilot**y, después, seleccione **Compilar**.

    Verá varias Advertencias, pero no debería haber Errores.

## Uso de GitHub Copilot para explicar el código base de la aplicación de biblioteca

GitHub Copilot puede ayudarle a comprender un código base desconocido mediante la generación de explicaciones en los niveles de solución, archivo y líneas de código.

### Análisis de código mediante mensajes en la vista Chat

La vista Chat de GitHub Copilot incluye una interfaz basada en chat que le permite interactuar con GitHub Copilot mediante mensajes en lenguaje natural. Al evaluar un código base existente por primera vez, puede crear mensajes que generen una explicación en el nivel de área de trabajo o proyecto, o en el de bloques o líneas de código. Para ayudarle a especificar el contexto del mensaje, GitHub Copilot proporciona participantes de chat, variables de chat y comandos de barra diagonal.

- Los participantes de chat se usan para establecer el ámbito del mensaje en un dominio específico.
- Las variables de chat se usan para incluir contexto específico en el mensaje.
- Los comandos de barra diagonal se usan a fin de evitar escribir mensajes complejos para escenarios comunes.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Asegúrese de que la solución AccelerateDevGHCopilot está abierta en Visual Studio Code.

1. Abra la vista Chat de GitHub Copilot.

    Para abrir la vista Chat, seleccione el botón **Alternar chat** en la parte superior de la ventana de Visual Studio Code.

    ![Recorte de pantalla en el que se muestra el menú de estado de GitHub Copilot.](./Media/m02-github-copilot-toggle-chat.png)

    También puede abrir la vista Chat mediante el método abreviado de teclado **Ctrl+Alt+I**.

1. En la vista Chat, escriba una indicación que use el participante de chat **@workspace** de GitHub Copilot para generar una descripción del proyecto.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```plaintext
    @workspace describe this project
    ```

    Use participantes de chat, como **@workspace**, para mejorar las respuestas generadas por GitHub Copilot. Los participantes de chat son como expertos de dominio que pueden ayudarte en áreas especializadas. Use **@workspace** cuando quiera que GitHub Copilot tenga en cuenta la estructura del proyecto, cómo interactúan las distintas partes del código o los modelos de diseño del proyecto.

    Para ver una lista de todos los participantes de chat disponibles, escriba **@** en el cuadro de mensaje del chat.

1. Dedique un minuto a comparar la respuesta de GitHub Copilot con los archivos de proyecto reales.

    Debería ver una respuesta que describa cada uno de los proyectos de la solución:

    - **Library.ApplicationCore**
    - **Library.Console**
    - **Library.Infrastructure**
    - **UnitTests**

1. Use la vista EXPLORADOR DE SOLUCIONES para expandir las carpetas del proyecto.

1. Localice y abra el archivo **ConsoleApp.cs**.

    El archivo ConsoleApp.cs se encuentra en la carpeta **src/Library.Console**.

1. Dedique un momento a revisar el archivo de código.

1. Escriba una indicación en la vista Chat que genere una descripción de la clase **ConsoleApp**.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```plaintext
    @workspace #usages How is the ConsoleApp class used?
    ```

    Use variables de chat, como **#usages**, para incluir contexto específico en la indicación. Para ver una lista de todas las variables de chat disponibles, escriba **#** en el cuadro de mensaje del chat.

    > **NOTA**: GitHub Copilot tiene en cuenta el historial de chat y los archivos de código que tiene abiertos en Visual Studio Code al crear un contexto para el mensaje y generar una respuesta.

1. Dedique un minuto a comprobar la precisión de la respuesta de GitHub Copilot.

    Debería ver una respuesta que describe dónde se define la clase **ConsoleApp** y cómo se usa en el código base. Se hace referencia a los archivos ConsoleApp.cs y Program.cs en la respuesta, junto con números de línea.

1. Abra el archivo **Program.cs** y examine el código.

1. Escriba una indicación en la vista Chat que genere una explicación del archivo Program.cs.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```plaintext
    @workspace /explain Explain the Program.cs file
    ```

    Use comandos de barra diagonal, como **/explain**, a fin de evitar escribir indicaciones complejas para escenarios comunes. Para ver una lista de todos los comandos de barra diagonal disponibles, escriba **/** en el cuadro de mensaje del chat. Los comandos de barra oblicua disponibles pueden variar en función de tu entorno y del contexto del chat.

1. Dedique un minuto a revisar la respuesta detallada generada por GitHub Copilot.

    Debería ver una respuesta que incluye información general y un desglose que explica cómo se usa el archivo dentro de la aplicación.

1. Cierre el archivo Program.cs.

### Mejora de las respuestas de chat mediante la incorporación de contexto

GitHub Copilot usa el contexto para generar respuestas más relevantes.

Abrir archivos en el editor de código es una manera de establecer contexto, pero también puede agregar archivos al contexto de chat mediante operaciones de arrastrar y colocar, o mediante el botón **Asociar contexto** de la vista Chat.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Expanda el proyecto **Library.Infrastructure** y después expanda la carpeta **Data**.

1. Use una operación de arrastrar y soltar para agregar los siguientes archivos desde la vista EXPLORADOR DE SOLUCIONES al contexto de chat: **JsonData.cs**, **JsonLoanRepository.cs** y **JsonPatronRepository.cs**.

    GitHub Copilot usa el contexto de Chat para comprender los archivos de código que son relevantes para el mensaje. Puede agregar archivos al contexto de Chat mediante operaciones de arrastrar y colocar, o bien puede usar el botón **Asociar contexto** en la vista Chat.

    En lugar de agregar archivos individuales de forma manual, puede permitir que Copilot encuentre automáticamente los archivos correctos en el código base. Esto puede ser útil cuando no sabe qué archivos son relevantes para la pregunta.

    Para permitir que Copilot busque automáticamente los archivos correctos, agregue #codebase en el mensaje o seleccione Código base en la lista de tipos de contexto.

1. Escriba un mensaje en la vista Chat que genera una explicación de las clases de acceso a datos.

    Por ejemplo, escriba el siguiente símbolo del sistema en la vista Chat:

    ```plaintext
    @workspace /explain Explain how the data access classes work
    ```

1. Dedique un par de minutos a revisar la respuesta.

    Debería ver una respuesta que describe cada una de las clases de acceso a datos (**JsonData**, **JsonLoanRepository** y **JsonPatronRepository**) y cómo funcionan de manera conjunta para administrar el acceso a datos en la aplicación. Los métodos clave, como **LoadData**, **SaveLoans** y **SavePatrons**, se deben mencionar en la respuesta.

1. Dedique un minuto a examinar los archivos de datos JSON que se usan para simular los registros de la biblioteca.

    Los archivos de datos JSON se encuentran en la carpeta **src/Library.Console/Json**.

    Los archivos de datos usan propiedades de identificador para vincular entidades. Por ejemplo, un objeto **Préstamo** tiene una propiedad **PatronId** que se vincula a un objeto **Patron** con el mismo Id. Los archivos JSON contienen datos para autores, libros, artículos de libros, patrones y préstamos.

    > **NOTA**: Tenga en cuenta que los nombres de autor, los títulos de los libros y los nombres de usuario se han anonimizado para los fines de este entrenamiento.

### Compilación y ejecución de la aplicación

La ejecución de la aplicación le ayuda a comprender la interfaz de usuario, las características clave de la aplicación y cómo interactúan sus componentes.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Asegúrese de que tiene abierta la vista del** Explorador de soluciones **.

    La vista Explorador de soluciones no es la misma que la vista explorador. La vista Explorador de soluciones usa archivos de proyecto y solución como nodos "directorio" para mostrar la estructura de la solución.

1. Para ejecutar la aplicación, haga clic con el botón derecho en **Library.Console**, seleccione **Depurar**y, a continuación, seleccione **Iniciar nueva instancia**.

    Si no se muestran las opciones **Depurar** y **Iniciar nueva instancia**, asegúrese de que usa la vista Explorador de soluciones y no la vista Explorador.

    Los pasos siguientes le guían a través de un caso de uso sencillo.

1. Cuando se le solicite un nombre de patrón, escriba **Uno** y presione Entrar.

    Debería ver una lista de clientes que coinciden con la consulta de búsqueda.

    > **NOTA**: La aplicación usa un proceso de búsqueda que distingue mayúsculas de minúsculas.

1. En el símbolo del sistema "Opciones de entrada", escriba **2** y presione Entrar.

    Al escribir **2**, se selecciona el segundo patrón de la lista.

    Debería ver el nombre del patrón y el estado de suscripción seguido de los detalles del préstamo del libro.

1. En el símbolo del sistema "Opciones de entrada", escriba **1** y presione Entrar.

    Al escribir **1**, se selecciona el primer libro de la lista.

    Debería ver los detalles del libro en la lista, incluida la fecha de vencimiento y el estado de devolución.

1. En el símbolo del sistema "Opciones de entrada", escriba **r** y presione Entrar.

    Al escribir **r**, se devuelve el libro.

1. Comprueba que se muestra el mensaje "Libro devuelto correctamente". .

    El mensaje "Libro devuelto correctamente." debe ir seguido de los detalles del libro. Los libros devueltos se marcan con **Returned: True**.

1. Para iniciar una nueva búsqueda, escriba **s** y presione Entrar.

1. Cuando se le solicite un nombre de patrón, escriba **Uno** y presione Entrar.

1. En el símbolo del sistema "Opciones de entrada", escriba **2** y presione Entrar.

1. Comprueba que el primer préstamo de libros está marcado como **Returned: True**.

1. En el símbolo del sistema "Opciones de entrada", escriba **q** y presione Entrar.

1. Detenga la sesión de depuración.

## Creación de la documentación del proyecto para el archivo LÉAME

Los archivos Léame proporcionan a los colaboradores del proyecto y a las partes interesadas información esencial sobre un repositorio de código. Ayudan a los usuarios a comprender el propósito del proyecto, cómo usarlo y cómo colaborar. Un archivo LÉAME bien estructurado puede mejorar significativamente la facilidad de uso y el mantenimiento de un proyecto.

Necesita un archivo LÉAME que incluya las secciones siguientes:

- **Título del proyecto**: un título breve y claro del proyecto.
- **Descripción**: una explicación detallada de lo que es el proyecto y lo que hace.
- **Estructura del proyecto**: Desglose de la estructura del proyecto, incluidas las carpetas de claves y los archivos.
- **clases clave e interfaces**: Lista de clases e interfaces clave del proyecto.
- **Uso**: instrucciones sobre cómo usar el proyecto, a menudo se incluyen ejemplos de código.
- **Licencia**: la licencia en la que está el proyecto.

En esta sección del ejercicio, usará GitHub Copilot para crear la documentación del proyecto y agregarla a un archivo **README.md**.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Agregue un nuevo archivo denominado **README.md** a la carpeta raíz de la solución **AccelerateDevGHCopilot**.

1. Abra la vista Chat.

1. Para generar documentación del proyecto para el archivo LÉAME, escriba el siguiente símbolo del sistema:

    ```plaintext

    @workspace Generate the contents of a README.md file for a code repository. Use "Library App" as the project title. The README file should include the following sections: Description, Project Structure, Key Classes and Interfaces, Usage, License. Format all sections as raw markdown. Use a bullet list with indents to represent the project structure. Do not include ".gitignore" or the ".github", "bin", and "obj" folders.

    ```

    > **NOTA**: Con varias solicitudes, una para cada sección del archivo LÉAME generaría más Resultados detallados En este ejercicio se usa una simple solicitud para simplificar el proceso.

1. Revise la respuesta para asegurarse de que cada sección tiene el formato markdown.

    Puede actualizar secciones individualmente para proporcionar información más detallada o si no tienen el formato correcto. También puede copiar la respuesta de GitHub Copilot al archivo LÉAME y, a continuación, realizar correcciones directamente en el archivo markdown.

1. Copie la documentación sugerida y, después, péguela en el archivo README.md.

    Para copiar toda la respuesta, desplácese hasta la parte inferior de la respuesta, haga clic con el botón derecho en el espacio vacío a la derecha del icono "pulgar hacia arriba" y seleccione **Copiar**

1. Dé formato al archivo README.md según sea necesario.

    Puede actualizar la configuración de GitHub Copilot para habilitar el formato markdown y, después, usar GitHub Copilot para ayudarle a actualizar las secciones del archivo README.md.

    Cuando haya terminado, debe tener un archivo README.md que incluya cada una de las secciones especificadas, con un nivel de detalle adecuado.

## Resumen

En este ejercicio, ha aprendido a usar GitHub Copilot para analizar y documentar un código base. Ha usado GitHub Copilot para generar explicaciones de la estructura del proyecto, clases clave y clases de acceso a datos. También ha usado GitHub Copilot para crear un archivo README.md para el proyecto.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Si ha realizado algún cambio, reviértalos ahora.
