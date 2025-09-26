---
lab:
  title: "Ejercicio: Refactorización del código existente mediante GitHub\_Copilot (Python)"
  description: "Obtenga información sobre cómo refactorizar y mejorar las secciones de código existentes mediante GitHub\_Copilot en Visual\_Studio Code."
---

# Refactorización de código existente mediante GitHub Copilot

GitHub Copilot se puede usar para evaluar todo el código base y sugerir actualizaciones que le ayuden a refactorizar y mejorar el código. En este ejercicio, usará GitHub Copilot para refactorizar secciones especificadas de una aplicación de Python mientras realiza mejoras en la calidad, la confiabilidad, el rendimiento y la seguridad del código.

Este ejercicio debería tardar en completarse **30** minutos aproximadamente.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar su propia cuenta de GitHub y suscripción de GitHub Copilot. Si no tiene una cuenta de GitHub, puede <a href="https://go.microsoft.com/fwlink/?linkid=2320148" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

## Antes de comenzar

El entorno de laboratorio debe incluir lo siguiente: Git 2.48 o posterior, Python 3.10 o posterior, Visual Studio Code con la extensión Python de Microsoft y acceso a una cuenta de GitHub con GitHub Copilot habilitado.

Si usa un equipo local como entorno de laboratorio para este ejercicio:

- Para obtener ayuda a fin de configurar el equipo local como entorno de laboratorio, abra el siguiente vínculo en un explorador: <a href="https://microsoftlearning.github.io/mslearn-github-copilot-dev/Instructions/Labs/LAB_AK_00_configure_lab_environment_py.html" target="_blank">Configure los recursos de entorno de laboratorio</a>.

- Para obtener ayuda a fin de habilitar la suscripción de GitHub Copilot en Visual Studio Code, abra el siguiente vínculo en un explorador: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

Si usa un entorno de laboratorio hospedado para este ejercicio:

- Para obtener ayuda a fin de habilitar la suscripción de GitHub Copilot en Visual Studio Code, pegue la siguiente dirección URL en la barra de navegación del sitio de un explorador: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

- Abra un terminal de comandos y luego ejecute los siguientes comandos:

    A fin de asegurarse de que Visual Studio Code está configurado para usar la versión correcta de Python, compruebe que la instalación de Python sea la versión 3.10 o posterior:

    ```bash
    python --version
    ```

    Para asegurarse de que Git está configurado para usar el nombre y la dirección de correo electrónico, actualice los siguientes comandos con la información y, después, ejecute los comandos:

    ```bash

    git config --global user.name "John Doe"

    ```

    ```bash

    git config --global user.email johndoe@example.com

    ```

## Escenario del ejercicio

Es un desarrollador que trabaja en el departamento de TI de la comunidad local. Los sistemas de back-end que admiten la biblioteca pública se han perdido en un incendio. El equipo debe desarrollar un proyecto temporal para ayudar al personal de la biblioteca a administrar sus operaciones hasta que se pueda reemplazar el sistema. El equipo ha elegido GitHub Copilot para acelerar el proceso de desarrollo.

Ha entregado una versión inicial de la aplicación de biblioteca para su revisión. El equipo de revisión ha identificado oportunidades para mejorar la calidad, el rendimiento, la legibilidad, el mantenimiento y la seguridad del código.

Este ejercicio incluye las siguientes tareas:

1. Configurar la aplicación de biblioteca en Visual Studio Code.
1. Analizar y refactorizar el código mediante la vista Chat en los modos Preguntar y Editar.
1. Refactorizar el código mediante chat en línea y la vista Chat en los modos Editar y Agente.

## Configurar la aplicación de biblioteca en Visual Studio Code

Debe descargar la aplicación existente, extraer los archivos de código y, a continuación, abrir el proyecto en Visual Studio Code.

Siga estos pasos para configurar la aplicación de la biblioteca:

1. Abra una ventana del explorador en el entorno de laboratorio.

1. Para descargar un archivo ZIP con la aplicación de biblioteca, pegue la siguiente dirección URL en la barra de direcciones del explorador: [Laboratorio de GitHub Copilot: Refactorización de código existente](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/AZ2007LabAppM5Python.zip)

    El archivo ZIP se denomina **AZ2007LabAppM5Python.zip**.

1. Extraiga los archivos del archivo **AZ2007LabAppM5Python.zip**.

    Por ejemplo:

    1. Vaya a la carpeta de descargas del entorno de laboratorio.

    1. Haga clic con el botón derecho en **AZ2007LabAppM5Python.zip** y **seleccione Extraer todo**.

    1. Seleccione **Mostrar los archivos extraídos al completar** y, a continuación, **Extraer**.

1. Abra la carpeta de archivos extraídos y, después, copie la carpeta **AccelerateDevGHCopilot** en una ubicación que sea fácil de acceder, como la carpeta Escritorio de Windows.

1. Abra la carpeta **AccelerateDevGHCopilot** en Visual Studio Code.

    Por ejemplo:

    1. Abra Visual Studio Code en el entorno de laboratorio.

    1. En Visual Studio Code, en el menú **Archivo**, seleccione **Abrir archivo**.

    1. Vaya a la carpeta Escritorio de Windows, seleccione **AccelerateDevGHCopilot** y luego **Seleccionar carpeta**.

1. En la vista EXPLORADOR de Visual Studio Code, compruebe la siguiente estructura del proyecto:

    - AccelerateDevGHCopilot/library   ├── application_core   ├── console   ├── infrastructure   └── tests

1. Asegúrese de que el código inicial se ejecuta mediante pruebas correctamente en la sección siguiente. Opcionalmente, ejecute la aplicación si está familiarizado con los laboratorios anteriores de la carpeta **\library** en la terminal utilizando **`python console\main.py`**.

### Habilitar Pytest

En comparación con Unittest, Pytest algunas ventajas, como la sintaxis concisa, características como accesorios y parametrización, y un mejor informe de errores. Pytest facilita la escritura y el mantenimiento de pruebas de Pytest y ejecuta casos de prueba Unittest.

1. Pytest está habilitado desde la instalación de la <a href="https://marketplace.visualstudio.com/items?itemName=ms-python.python" target="_blank">extensión</a> de Microsoft Python de Visual Studio, instale si es necesario.

1. Seleccione el icono de flask.  ![Recorte de pantalla que muestra el icono de flask de prueba.](./Media/m04-pytest-flask-py.png) en la barra de herramientas una vez detectadas las pruebas. Si el icono no está presente, revise las instrucciones anteriores.

1. Elija "Configurar pruebas de Python" o si se configuró anteriormente:

1. Si las pruebas no se han configurado o están probando el proyecto correcto, vaya al paso siguiente. Si necesita cambiar el proyecto de prueba, continúe con:
    - `Ctrl+Shift+P` para abrir la paleta de comandos.
    - escriba **"Python: Configure pruebas"**.
    - Seleccione "pytest".
    - Seleccione el directorio para el código de Python.
    - Seleccione el icono de reproducción para ejecutar pruebas.

1. Seleccione Pytest en las opciones.

1. Elija la carpeta (`library\`) que contiene el código de prueba.

1. Seleccione el icono de reproducción para ejecutar pruebas.
    ![Recorte de pantalla que muestra los resultados de pytest.](./Media/m04-pytest-configure-results-py.png)

1. Opcionalmente, ejecute el comando ptytest desde la ruta de acceso `library` en el terminal:

    ```plaintext
    pytest -v
    ```

## Análisis y refactorización de código mediante la vista Chat en modo Preguntar y Editar

La reflexión es una característica eficaz que permite inspeccionar y manipular objetos en tiempo de ejecución. Sin embargo, la reflexión puede ser lenta y hay posibles riesgos de seguridad asociados a la reflexión que se deben tener en cuenta.

Necesita:

1. Analice el área de trabajo e investigue cómo abordar la tarea asignada.
1. Refactorice el uso de Python Enum en una clase enum_helper para usar diccionarios estáticos en lugar de reflexión y python integrados en Enum.

### Analizar el uso de enumeración con la vista Chat en modo Preguntar

La vista chat de GitHub Copilot tiene tres modos: **Preguntar**, **Editar** y **Agente**. Cada modo está diseñado para diferentes tipos de interacciones con GitHub Copilot.

- **Pregunta**: Use este modo para hacer preguntas de GitHub Copilot sobre el código base. Puede pedirle a GitHub Copilot que explique el código, sugiera cambios o proporcione información sobre el código base.
- **Editar**: Use este modo para editar los archivos de código seleccionados. Puede usar GitHub Copilot para refactorizar el código, agregar comentarios o realizar otros cambios en el código.
- **Agente**: Use este modo para ejecutar GitHub Copilot como agente. Puede GitHub Copilot para ejecutar comandos, ejecutar código o realizar otras tareas en el área de trabajo.

En esta sección del ejercicio, usará la vista Chat en modo **Preguntar** para analizar la asignación de programación.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. En la vista EXPLORADOR, para expandir la carpeta **, seleccione **.

1. Abra la vista GitHub Copilot Chat.

    La vista Chat proporciona una interfaz de conversación administrada para interactuar con GitHub Copilot.

    Puede alternar la vista Chat entre abierta y cerrada mediante el botón **Alternar chat**, que se encuentra en la parte superior de la ventana de Visual Studio Code, justo a la derecha del cuadro de texto de búsqueda.

    ![Recorte de pantalla en el que se muestra el botón Alternar chat de Copilot.](./Media/m01-github-copilot-toggle-chat.png)

    También puede usar el método abreviado de teclado **Ctrl+Alt+I** para alternar la vista Chat.

1. Observe que la vista Chat se abre en modo **Preguntar** de manera predeterminada.

    El modo de Chat actual se muestra cerca de la esquina inferior derecha de la vista Chat. Las respuestas de chat se muestran en la vista Chat cuando trabaja en el modo **Preguntar**.

1. Revise y después envíe el mensaje siguiente:

    ```plaintext
    @workspace Provide an explanation of how the current Python code can be improved with code refactoring to:
    - avoid reflection
    - avoid repeated `if/elif`
    - make the code more explicit and efficient.
    Then provide suggestion for refactoring this Python project to implement the improvement suggestions.
    ```

1. Dedique un minuto a revisar la respuesta, como esta, con sugerencias de código eliminadas:

    >**NOTA** Es normal ver una respuesta muy diferente, pero debe haber temas similares.

    -----

    >### Explicación de la mejora del código
    >
    > Para mejorar el código actual, tenga en cuenta las siguientes estrategias de refactorización:
    >
    > 1. **Evitar reflexión**:  
    >    La reflexión puede ser lenta y propensa a errores. En su lugar, use llamadas explícitas a métodos, interfaces o diccionarios para asignar acciones a funciones. Esto hace que el código sea más fácil de mantener y realizar.
    >
    > 2. **Evite repetir `if/elif` cadenas**:  
    >    Las cadenas largas `if/elif` son difíciles de leer y mantener. Reemplácelas por un diccionario (en Python) o una expresión switch (en C# 8+) o use polimorfismo (diseño orientado a objetos) para delegar el comportamiento.
    >
    > 3. **Hacer que el código sea más explícito y eficaz**:  
    >    El código explícito es más fácil de entender y depurar. Use nombres de variables claros, evite cadenas o números mágicos y lógica de estructura para que la intención sea obvia. La eficacia a menudo se puede mejorar reduciendo las comprobaciones o búsquedas innecesarias.
    >
    >#### Sugerencias de refactorización
    >
    > Supongamos que tiene código similar al siguiente (ejemplo de Python):
    >
    > ```python
    > # ...existing code...
    > def handle_action(action, data):
    >     if action == "create":
    >         return create_item(data)
    >     elif action == "update":
    >         return update_item(data)
    >     elif action == "delete":
    >         return delete_item(data)
    >     else:
    >         raise ValueError("Unknown action")
    > # ...existing code...
    > ```
    >
    > **Versión refactorizado (evita reflexión e if/elif, más explícito)**
    >
    > ```python
    > # ...existing code...
    > def handle_action(action, data):
    >     action_map = {
    >         "create": create_item,
    >         "update": update_item,
    >         "delete": delete_item,
    >     }
    >     try:
    >         return action_map[action](data)
    >     except KeyError:
    >         raise ValueError(f"Unknown action: {action}")
    > # ...existing code...
    > ```
    >
    > **Ventajas:**
    >
    > - No se usa ninguna reflexión.
    > - No se repite `if/elif`.
    > - La asignación es explícita y fácil de extender.
    > - Más eficaz debido a la búsqueda directa de funciones.
    >
    >### Resumen
    >
    > - Use diccionarios o expresiones switch en lugar de cadenas de reflexión o `if/elif` largas.
    > - Hacer que las asignaciones sean explícitas para mantener y mejorar la eficacia.
    > - Use el control de errores claros para casos desconocidos.
    >
    > Estos cambios harán que el código base sea más fácil de mantener, más eficaz y menos propenso a errores.

1. Revise y después envíe el mensaje siguiente:

    ```plaintext
    @workspace which Python files in this workspace use reflection or long `if/elif` chains?
    ```

    La respuesta debería indicarle **console/console_app.py**  (`getattr`) y que **console/console_app.py** también utiliza cadenas largas `if/elif` para el manejo de comandos y entradas.

1. Añada el archivo **console/console_app.py** al contexto Chat:

    Puede usar una operación de arrastrar y soltar para agregar los archivos desde la vista Explorador de Visual Studio Code a la vista Chat. También puede usar el botón **Agregar contexto** en la vista Chat para agregar archivos y otros recursos.

    > **NOTA**: Agregar archivos al contexto de Chat garantiza que GitHub Copilot los tenga en cuenta al generar una respuesta. La relevancia y la precisión de las respuestas aumentan cuando GitHub Copilot comprende el contexto asociado a los mensajes.

1. Revise y después envíe el mensaje siguiente:

    ```plaintext

    @workspace I need to refactor the `library\console\console_app.py` Python file to: Use dictionaries or switch expressions instead of reflection or long `if/elif` chains; Make mappings explicit for maintainability and efficiency; Use clear error handling for unknown cases; Provide refactored code to apply.

    ```

    Al escribir cualquier mensaje, la claridad y el contexto son importantes. El uso de participantes de chat, comandos de barra diagonal y variables de chat ayuda a definir el contexto de una manera que GitHub Copilot pueda comprender.

    Para obtener un mensaje que pregunte a GitHub Copilot cómo resolver un problema, comience con el problema que está intentando resolver. Use oraciones concisas para describir detalles, especificar restricciones e identificar recursos. Por último, asegúrese de indicarle a GitHub Copilot qué incluir en la respuesta.

    En este caso, el mensaje comienza con una descripción del problema u objetivo. Indique a GitHub Copilot que necesita refactorizar el archivo `library\console\console_app.py` en:

    - Use diccionarios o expresiones switch en lugar de cadenas de reflexión o `if/elif` largas.
    - Hacer que las asignaciones sean explícitas para mantener y mejorar la eficacia.
    - Use el control de errores claros para casos desconocidos.

    Para mayor claridad, para finalizar el mensaje, proporcione la instrucción para "proporcionar código refactorizado que se va a aplicar".

1. Dedique un minuto a revisar la respuesta proporcionada por GitHub Copilot. En este paso no **aplique las modificaciones**.

    > ### Explicación de la mejora del código
    >
    > Para mejorar el código actual, tenga en cuenta las siguientes estrategias de refactorización:
    >
    > 1. **Evitar reflexión**:  
    >    La reflexión puede ser lenta y propensa a errores. En su lugar, use llamadas explícitas a métodos, interfaces o diccionarios para asignar acciones a funciones. Esto hace que el código sea más fácil de mantener y realizar.
    >
    > 2. **Evite repetir `if/elseif` cadenas**:  
    >    Las cadenas largas `if/elseif` son difíciles de leer y mantener. Reemplácelas por un diccionario (en Python) o una expresión switch (en C# 8+) o use polimorfismo (diseño orientado a objetos) para delegar el comportamiento.
    >
    > 3. **Hacer que el código sea más explícito y eficaz**:  
    >    El código explícito es más fácil de entender y depurar. Use nombres de variables claros, evite cadenas o números mágicos y lógica de estructura para que la intención sea obvia. La eficacia a menudo se puede mejorar reduciendo las comprobaciones o búsquedas innecesarias.
    >
    >
    > ### Sugerencias de refactorización
    >
    > Supongamos que tiene código similar al siguiente (ejemplo de Python):
    >
    > ```python
    > # ...existing code...
    >    def _handle_patron_details_selection(self, selection, patron, valid_loans):
    >        if selection == 'q':
    >            return ConsoleState.QUIT
    >        elif selection == 's':
    >            return ConsoleState.PATRON_SEARCH
    >        elif selection == 'm':
    >            status = self._patron_service.renew_membership(patron.id)
    >            print(status)
    >            self.selected_patron_details = self._patron_repository.get_patron(patron.id)
    >            return ConsoleState.PATRON_DETAILS
    > # ...existing code...
    > ```
    >
    > #### Versión refactorizado (evita reflexión e if/elif, más explícito)
    >
    > ```python
    > # ...existing code...
    >    def _handle_patron_details_selection(self, selection, patron, valid_loans):
    >        def renew_membership():
    >           status = self._patron_service.renew_membership(patron.id)
    >           print(status)
    >           self.selected_patron_details = self._patron_repository.get_patron(patron.id)
    >           return ConsoleState.PATRON_DETAILS
    > # ...existing code...
    > ```
    >
    > **Ventajas:**
    >
    > - No se usa ninguna reflexión.
    > - No se repite `if/elif`.
    > - La asignación es explícita y fácil de extender.
    > - Más eficaz debido a la búsqueda directa de funciones.
    >
    >
    > ### Resumen
    >
    > - Use diccionarios o expresiones switch en lugar de cadenas de reflexión o `if/elseif` largas.
    > - Hacer que las asignaciones sean explícitas para mantener y mejorar la eficacia.
    > - Use el control de errores claros para casos desconocidos.
    >
    > Estos cambios harán que el código base sea más fácil de mantener, más eficaz y menos propenso a errores.

1. En la vista Chat, mantenga el puntero del mouse sobre el ejemplo de código incluido en la respuesta.

1. Observe los tres botones que aparecen en la esquina superior derecha del fragmento de código.

1. Mantenga el puntero sobre cada uno de los botones para ver una información sobre herramientas que describe la acción.

    Los dos primeros botones copian el código en el editor. El tercer botón copia el código en el Portapapeles. En este paso no **aplique las modificaciones**.

> **NOTA**: Puede usar el modo Preguntar para actualizar el código. Pero el modo Editar refactoriza el código directamente dentro del editor de código y proporciona más opciones para aceptar actualizaciones.

### Refactorización del archivo de la clase ConsoleApp (console/console_app.py) mediante la Vista de chat en modo Edición.

El modo Editar de la vista Chat está diseñado para editar código en el área de trabajo. Puede usar el modo Editar para refactorizar el código, agregar comentarios o realizar otros cambios en el código.

1. En la vista Chat, seleccione **Establecer modo** y, después, **Editar**.

    Cuando se le pida que inicie una nueva sesión en el modo Editar, seleccione **Sí**.

    En el modo **Editar**, GitHub Copilot muestra respuestas como sugerencias de actualización de código en el editor de código. El modo Editar se usa generalmente al implementar una nueva característica, corregir un error o refactorizar código.

1. Añada el archivo console/console_app.py al contexto Chat:

1. Revise y después envíe el mensaje siguiente:

    ```plaintext

    @codebase I need to refactor the ConsoleApp class. Use static dictionaries to supply enum description attributes. Use dictionaries or switch expressions instead of reflection or long `if/elif` chains. Make mappings explicit for maintainability and efficiency. Use clear error handling for unknown cases.

    ```

    La respuesta del agente del modo de edición debe proponer actualizaciones en la clase `ConsoleApp` y proporcionar una respuesta similar a la siguiente:

    ```plaintext
    The ConsoleApp class has been refactored to use static dictionaries for enum descriptions, explicit dictionaries for state and input handling, and clear error handling for unknown cases, improving maintainability and efficiency.
    ```

1. Dedique un minuto a revisar las actualizaciones de código sugeridas en **console_app.py**. Los resultados deben completar lo siguiente:

    - Se introdujeron diccionarios estáticos para descripciones de enumeración (`CONSOLE_STATE_DESCRIPTIONS` y `COMMON_ACTIONS_DESCRIPTIONS`) para reemplazar las cadenas de reflexión y `if/elif` largas.
    - Se ha refactorizado `write_input_options` para usar el diccionario estático para mostrar las opciones de entrada.
    - Sustituyó el bucle de estado principal en `run` por una búsqueda de controlador basada en diccionarios para mejorar la capacidad de mantenimiento y la eficacia.
    - Se ha agregado un control explícito de errores para los estados desconocidos y los estados siguientes.
    - Todas las asignaciones de acciones de los controladores de entrada ahora son diccionarios explícitos para mayor claridad y mantenimiento.

1. En la vista Chat, para aceptar todas las actualizaciones, seleccione **Mantener**.

    También puede usar la barra de herramientas de ediciones de chat cerca de la parte inferior de la pestaña del editor de código para aceptar o rechazar actualizaciones de código.

1. Dedique un minuto a revisar el método **ejecutar** actualizado.

    GitHub Copilot debe haber actualizado el método **ejecutar** para reemplazar la cadena long if/elif por un diccionario de state_handlers que asigna cada ConsoleState a su función de controlador correspondiente. El método actualizado debe ser similar a uno de los siguientes:

    ```python

    def run(self) -> None:
        state_handlers = {
            ConsoleState.PATRON_SEARCH: self.patron_search,
            ConsoleState.PATRON_SEARCH_RESULTS: self.patron_search_results,
            ConsoleState.PATRON_DETAILS: self.patron_details,
            ConsoleState.LOAN_DETAILS: self.loan_details,
            ConsoleState.QUIT: lambda: ConsoleState.QUIT
        }
        while True:
            handler = state_handlers.get(self._current_state)
            if handler is None:
                print(f"Unknown state: {self._current_state}")
                break
            next_state = handler()
            if next_state == ConsoleState.QUIT:
                print("Exiting application.")
                break
            if next_state not in state_handlers:
                print(f"Unknown next state: {next_state}")
                break
            self._current_state = next_state
    ```

    Este código utiliza el diccionario `state_handlers` que asigna cada `ConsoleState` a su función de controlador correspondiente. Ahora recupera el controlador del diccionario, genera un error para estados desconocidos y actualiza el estado actual en función del valor devuelto del controlador.

1. Ejecute Pytest y pruebe manualmente para asegurarse de que no se han introducido errores.

    Verá las mismas advertencias que ha visto al principio de este ejercicio, pero no debería haber ningún mensaje de error.

## Refactorización del código mediante chat en línea y la vista Chat en los modos Editar y Agente

Al adoptar las **comprensiones de listas**, las **expresiones generadoras** y las **funciones integradas** de Python, como `any()`, `all()`, `sum()`, `map()`, `filter()` y `sorted()`, el código base puede volverse más conciso, expresivo y eficiente, reduciendo el código repetitivo y los posibles errores asociados con la iteración manual y el procesamiento de datos.

En esta sección del ejercicio se incluyen las siguientes tareas:

- **Chat insertado: Refactorización de expresiones del generador**
- **Chat en modo edición: Lista de comprensiones de listas y refactorización de métodos integrados de Python**
- **Modo de agente: Refactorización de funciones integradas**

### Refactorización de expresiones de generador mediante Chat insertado

1. En la vista EXPLORADOR, expanda el proyecto **infrastructure/json_patron_repository.py** y, a continuación, abra el archivo **json_loan_repository.py** y examine la clase **`JsonLoanRepository`**.

1. Para elegir la clase **`JsonLoanRepository`**, resalte toda la clase.

    ```python

    class JsonPatronRepository(IPatronRepository):
        def __init__(self, json_data: JsonData):
            self._json_data = json_data
    
        def get_patron(self, patron_id: int) -> Optional[Patron]:
            for patron in self._json_data.patrons:
                if patron.id == patron_id:
                    return patron
            return None
    
        def search_patrons(self, search_input: str) -> List[Patron]:
            results = []
            for p in self._json_data.patrons:
                if search_input.lower() in p.name.lower():
                    results.append(p)
            n = len(results)
            for i in range(n):
                for j in range(0, n - i - 1):
                    if results[j].name > results[j + 1].name:
                        results[j], results[j + 1] = results[j + 1], results[j]
            return results
    
        def update_patron(self, patron: Patron) -> None:
            for idx in range(len(self._json_data.patrons)):
                if self._json_data.patrons[idx].id == patron.id:
                    self._json_data.patrons[idx] = patron
                    self._json_data.save_patrons(self._json_data.patrons)
                    return
    
        def add_patron(self, patron: Patron) -> None:
            self._json_data.patrons.append(patron)
            self._json_data.save_patrons(self._json_data.patrons)
            self._json_data.load_data()
    
        def get_all_patrons(self) -> List[Patron]:
            return self._json_data.patrons
    
        def find_patrons_by_name(self, name: str) -> List[Patron]:
            result = []
            for patron in self._json_data.patrons:
                if patron.name.lower() == name.lower():
                    result.append(patron)
            return result
    
        def get_all_books(self):
            return self._json_data.books
    
        def get_all_book_items(self):
            return self._json_data.book_items

    ```

1. Abra un chat Copilot insertado y, a continuación, introduzca un mensaje que refactorice el método.

    ```plaintext
    #selection Refactor any manual aggregation or search over loans in this method to use generator expressions with built-in functions like any(), all(), sum(), or max() for improved readability and performance.
    ```

1. Dedique un minuto a revisar la actualización sugerida.

    Las actualizaciones sugeridas deben ser similares al siguiente código:

    ```python
    # --code continues-- 
    def get_patron(self, patron_id: int) -> Optional[Patron]:
        return next((patron for patron in self._json_data.patrons if patron.id == patron_id), None)

    def search_patrons(self, search_input: str) -> List[Patron]:
        results = [p for p in self._json_data.patrons if search_input.lower() in p.name.lower()]
        results.sort(key=lambda p: p.name)
        return results

    def update_patron(self, patron: Patron) -> None:
        for idx, existing_patron in enumerate(self._json_data.patrons):
            if existing_patron.id == patron.id:
                self._json_data.patrons[idx] = patron
                self._json_data.save_patrons(self._json_data.patrons)
                return

    # --code continues--    
    def find_patrons_by_name(self, name: str) -> List[Patron]:
        return [patron for patron in self._json_data.patrons if patron.name.lower() == name.lower()]
    # --code continues-- 
    ```

1. Para aceptar la actualización sugerida, seleccione **Aceptar**.

#### Utilice **la acción inteligente “Explicar” del Chat insertado** para examinar un método.

1. Utilice la acción inteligente **Explicar** para ver una explicación del método `search_patrons`.

1. Seleccione las siguientes líneas de código (después del comentario) del método `search_patrons`:

    ```python
    # def search_patrons(self, search_input: str) -> List[Patron]:
        results = [p for p in self._json_data.patrons if search_input.lower() in p.name.lower()]
        results.sort(key=lambda p: p.name)
    ```

    Para abrir la acción inteligente **Explicar**, seleccione el código del método `search_patrons` en el editor, haga clic con el botón derecho del ratón en el código seleccionado, seleccione Copilot y, a continuación, seleccione **Explicar**. La acción inteligente **Explicar**proporciona una explicación detallada del código seleccionado.

    Por ejemplo, la explicación podría tener este aspecto:

    ```plaintext

    The `search_patrons` method is responsible for finding patrons whose names contain a given search string, regardless of case. It takes a single argument, `search_input`, which is the string to search for. The method iterates over all patrons stored in `self._json_data.patrons` and uses a list comprehension to filter those whose `name` attribute contains the `search_input` substring. Both the patron's name and the search input are converted to lowercase to ensure the search is case-insensitive.
    
    After collecting the matching patrons, the method sorts the results alphabetically by the patron's name using the `sort()` method with a key function that extracts the `name` attribute from each patron. Finally, the sorted list of matching patrons is returned. This ensures that users receive a case-insensitive, alphabetically ordered list of patrons matching their search criteria.
    
    A potential consideration is that the search will match any part of the name, not just the beginning, which may lead to more results than expected. Also, the sorting is done in-place on a new list,

    ```

1. Pruebe y ejecute  su proyecto para asegurarse de que no se hayan introducido errores.

#### Continúe la refactorización de la expresión generadora utilizando el Chat insertado.

1. A continuación, continúe con el proceso de refactorización para **loan_service.py**.

1. En la vista EXPLORADOR, expanda el proyecto **application_core\services\loan_service.py** y, a continuación, abra el archivo **loan_service.py** y examine la clase **`LoanService`**.

1. Para seleccionar la clase **`LoanService`**, resalte toda la clase y examine el método `checkout_book`.

    ```python

    class LoanService(ILoanService):
        EXTEND_BY_DAYS = 14
    
        def __init__(self, loan_repository: ILoanRepository):
            self._loan_repository = loan_repository
    
        def return_loan(self, loan_id: int) -> LoanReturnStatus:
            loan = self._loan_repository.get_loan(loan_id)
            if loan is None:
                return LoanReturnStatus.LOAN_NOT_FOUND
            if loan.return_date is not None:
                return LoanReturnStatus.ALREADY_RETURNED
            loan.return_date = datetime.now()
            try:
                self._loan_repository.update_loan(loan)
                return LoanReturnStatus.SUCCESS
            except Exception:
                return LoanReturnStatus.ERROR
    
        def extend_loan(self, loan_id: int) -> LoanExtensionStatus:
            loan = self._loan_repository.get_loan(loan_id)
            if loan is None:
                return LoanExtensionStatus.LOAN_NOT_FOUND
            if loan.patron and loan.patron.membership_end < datetime.now():
                return LoanExtensionStatus.MEMBERSHIP_EXPIRED
            if loan.return_date is not None:
                return LoanExtensionStatus.LOAN_RETURNED
            if loan.due_date < datetime.now():
                return LoanExtensionStatus.LOAN_EXPIRED
            try:
                loan.due_date = loan.due_date + timedelta(days=self.EXTEND_BY_DAYS)
                self._loan_repository.update_loan(loan)
                return LoanExtensionStatus.SUCCESS
            except Exception:
                return LoanExtensionStatus.ERROR
    
        def checkout_book(self, patron, book_item, loan_id=None) -> None:
            from ..entities.loan import Loan
            from datetime import datetime, timedelta
            # Generate a new loan ID if not provided
            if loan_id is None:
                all_loans = getattr(self._loan_repository, 'get_all_loans', lambda: [])()
                max_id = 0
                for l in all_loans:
                    if l.id > max_id:
                        max_id = l.id
                loan_id = max_id + 1 if all_loans else 1
            now = datetime.now()
            due = now + timedelta(days=14)
            new_loan = Loan(
                id=loan_id,
                book_item_id=book_item.id,
                patron_id=patron.id,
                patron=patron,
                loan_date=now,
                due_date=due,
                return_date=None,
                book_item=book_item
            )
            self._loan_repository.add_loan(new_loan)
            return new_loan

    ```

1. Abra un Chat isertado y escriba un mensaje que refactorice el método.

    ```plaintext
    #selection Refactor any manual aggregation or search over loans in this method to use generator expressions with built-in functions like any(), all(), sum(), or max() for improved readability and performance.
    ```

1. Dedique un minuto a revisar la actualización sugerida con el código agregado en el método `checkout_book`:

    ```python

            loan_id = max((l.id for l in all_loans), default=0) + 1 if all_loans else 1
    ```

    El método `checkout_book` final será similar al código siguiente.

    ```python
    # --code continues-- 

    def checkout_book(self, patron, book_item, loan_id=None) -> None:
            from ..entities.loan import Loan
            from datetime import datetime, timedelta
            if loan_id is None:
                all_loans = getattr(self._loan_repository, 'get_all_loans', lambda: [])()
                loan_id = max((l.id for l in all_loans), default=0) + 1 if all_loans else 1
            now = datetime.now()
            due = now + timedelta(days=14)
            new_loan = Loan(
                id=loan_id,
                book_item_id=book_item.id,
                patron_id=patron.id,
                patron=patron,
                loan_date=now,
                due_date=due,
                return_date=None,
                book_item=book_item
            )
            self._loan_repository.add_loan(new_loan)
            return new_loan
    ```

    La refactorización para usar expresiones de generador reemplaza la iteración manual por construcciones concisas y eficientes en memoria que *funcionan sin problemas con funciones* integradas como `max()`, `any()` y `sum()`. Esto no solo reduce el código reutilizable y los posibles errores, sino que también mejora el rendimiento, especialmente cuando se procesan grandes conjuntos de datos, ya que las expresiones de generador no crean listas intermedias en la memoria. En general, estos cambios hacen que el código base sea más Pythonic, legible y fácil de mantener.

### Refactorización de la clase JsonPatronRepository mediante la vista Chat en modo Editar

La clase **JsonPatronRepository** incluye los tres métodos siguientes:

- SearchPatrons: el método SearchPatrons está diseñado para buscar usuarios por nombre. Este método devuelve una lista ordenada de usuarios.
- GetPatron: el método GetPatron se usa para recuperar un usuario por identificador. Este método devuelve un objeto de usuario rellenado.
- UpdatePatron: el método UpdatePatron se usa para actualizar la información de un usuario. Este método actualiza el usuario existente con los nuevos datos y guarda la colección de usuarios actualizada.

En cada uno de los tres métodos se usa un bucle foreach para iterar los usuarios y buscar coincidencias en función de la entrada o el identificador de búsqueda.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Abra el **archivo json_loan_repository.py**.

    La clase **JsonPatronRepository** está diseñada para administrar los clientes de la biblioteca.

1. Dedique un minuto a revisar algunos de los métodos incluidos en la clase **JsonPatronRepository**.

    El método **SearchPatrons** está diseñado para buscar usuarios por nombre.

    ```python

    #  ----code continues----   
    class JsonLoanRepository(ILoanRepository):
        def **init**(self, json_data: JsonData):
            self._json_data = json_data
    
        #  ----code continues----   
        def get_loans_by_patron_id(self, patron_id: int):
            result = []
            for loan in self._json_data.loans:
                if loan.patron_id == patron_id:
                    result.append(loan)
            return result
    
        #  ----code continues----  
        def get_overdue_loans(self, current_date):
            overdue = []
            for loan in self._json_data.loans:
                if loan.return_date is None and loan.due_date < current_date:
                    overdue.append(loan)
            return overdue
    
        def sort_loans_by_due_date(self):
            # Manual bubble sort for demonstration
            n = len(self._json_data.loans)
            for i in range(n):
                for j in range(0, n - i - 1):
                    if self._json_data.loans[j].due_date > self._json_data.loans[j + 1].due_date:
                        self._json_data.loans[j], self._json_data.loans[j + 1] = self._json_data.loans[j + 1], self._json_data.loans[j]
            return self._json_data.loans

        #  ----code continues----  
    ```

1. En la vista Chat, seleccione **Establecer modo** y, después, **Editar**.

    Cuando se le pida que inicie una nueva sesión en el modo Editar, seleccione **Sí**.

    En el modo **Editar**, GitHub Copilot muestra respuestas como sugerencias de actualización de código en el editor de código. El modo Editar se usa generalmente al implementar una nueva característica, corregir un error o refactorizar código.

1. Escriba la solicitud

    ```plaintext
    @codebase Refactor methods in the JsonLoanRepository class with for-loops to use list comprehensions 
    or Python built-in methods to improve code clarity, conciseness, and efficiency.
    ```

1. Observe en el código actualizado que sigue que los métodos `get_loans_by_patron_id` y `get_overdue_loans` ahora utilizan comprensiones de listas y que el método `sort_loans_by_due_date` ahora utiliza una función `sorted` integrada en Python.

    ```python
    #  ----code continues----

    def get_loan(self, loan_id: int) -> Optional[Loan]:
        return next((loan for loan in self._json_data.loans if loan.id == loan_id), None)

    def update_loan(self, loan: Loan) -> None:
        idx = next((i for i, l in enumerate(self._json_data.loans) if l.id == loan.id), None)
        if idx is not None:
            self._json_data.loans[idx] = loan
            self._json_data.save_loans(self._json_data.loans)
            return

    #  ----code continues----
    def get_loans_by_patron_id(self, patron_id: int):
        return [loan for loan in self._json_data.loans if loan.patron_id == patron_id]
    
    #  ----code continues----
    def get_overdue_loans(self, current_date):
        return [loan for loan in self._json_data.loans if loan.return_date is None and loan.due_date < current_date]

    def sort_loans_by_due_date(self):
        # Use built-in sorted for clarity and efficiency
        self._json_data.loans = sorted(self._json_data.loans, key=lambda l: l.due_date)
        return self._json_data.loans
    ```

    Las comprensiones de lista y las funciones integradas reemplazaron los bucles “for” manuales para filtrar y ordenar, lo que hace que el código sea más corto, más claro y eficaz.

### Refactorización de la clase JsonPatronRepository mediante la Vista de chat en modo Agente

1. En la vista Chat, cambie el modo a **Agente**

    El modo Agente está diseñado para ejecutar GitHub Copilot como agente. Puede usar lenguaje natural para especificar una tarea general. El agente evaluará la tarea asignada, planeará el trabajo necesario y aplicará los cambios en el código base.

    El modo Agente usa una combinación de la edición de código y la invocación de herramientas para realizar la tarea especificada. A medida que procesa la solicitud, supervisa el resultado de las ediciones y las herramientas, e itera para resolver los problemas que surjan. Si el agente no puede resolver un problema, le pedirá que intervenga. Por ejemplo, si el agente usa varias iteraciones que funcionan para resolver el mismo problema, pausará el proceso y le pedirá que proporcione contexto adicional para aclarar la solicitud o cancelar el proceso.

    > **IMPORTANTE**: Cuando se usa la vista Chat en modo Agente, GitHub Copilot puede realizar varias solicitudes premium para completar una sola tarea. Las solicitudes premium se pueden usar en mensajes iniciados por el usuario y acciones de seguimiento que Copilot realiza en su nombre. El número total de solicitudes premium usadas se basa en la complejidad de la tarea, el número de pasos implicados y el modelo seleccionado.

1. Dedique un minuto a tener en cuenta la tarea que necesita asignar al agente.

    La tarea consiste en refactorizar las clases **JsonLoanRepository** & **JsonPatronRepository**. El objetivo es localizar bucles manuales para refactorizar con **Funciones integradas de Python** que produzcan el mismo resultado que el código foreach original.

    Puede usar su experiencia con la refactorización anterior para ayudarle a escribir la tarea para el agente.

1. Para asignar la tarea al agente, introduzca el siguiente comando utilizando **modo AGENTE**:

    ```plaintext

    #codebase Review the manual loop code used in the methods of the JsonLoanRepository and JsonPatronRepository classes to make them more pythonic. Refactor with Built-in Python Functions that produce the same result as the original foreach code.

    ```

    Este mensaje indica al agente que refactorice la clase **JsonPatronRepository**. Especifica que los bucles foreach deben reemplazarse por Funciones integradas de Python.

1. Supervise el progreso del agente a medida que refactoriza el código.

    Observe que el agente completa la tarea en varias iteraciones. Cada paso de edición de código va seguido de un paso de revisión que comprueba si hay problemas. Si el agente encuentra un problema, refactorizará el código para resolverlo. Si el agente no puede resolver un problema, le pedirá que intervenga.

1. Una vez que finalice el agente, dedique un minuto a revisar las actualizaciones sugeridas.

    Los cambios realizados en JsonLoanRepository deben ser: - `update_patron` ahora utiliza `next` con `enumerate` para una búsqueda eficiente en el índice.
        - `search_patrons` usa una expresión generadora y `sorted` para obtener un código conciso y legible.
        - Se han quitado todas las burbujas manuales y el código redundante.

    > **NOTA:** No se necesitaban cambios para JsonPatronRepository, ya que ya usa funciones integradas y comprensiones para filtrar y buscar.

    Las actualizaciones sugeridas deben ser similares al siguiente código:

    ```python
    #  ----code continues----
    def search_patrons(self, search_input: str) -> List[Patron]:
        return sorted(
            (p for p in self._json_data.patrons if search_input.lower() in p.name.lower()),
            key=lambda patron: patron.name
        )

    def update_patron(self, patron: Patron) -> None:
        idx = next((i for i, existing_patron in enumerate(self._json_data.patrons) if existing_patron.id == patron.id), None)
        if idx is not None:
            self._json_data.patrons[idx] = patron
            self._json_data.save_patrons(self._json_data.patrons)

        #  ----code continues----

    ```

1. Para aceptar todas las actualizaciones, seleccione **Mantener**.

Estas actualizaciones hacen que el código sea más conciso, legible y Pythonic, al tiempo que conserva el comportamiento original.

### Ejecutar y probar la aplicación

Ahora que ha refactorizado el código, es hora de probar y ejecutar la aplicación para asegurarse de que todo funciona correctamente. También probará la aplicación para asegurarse de que el código refactorizado funciona según lo previsto.

1. Para ejecutar la aplicación en Visual Studio Code con Python, abra **console/ main.py** en el editor, presione **CTRL+Mayús+D** para abrir el panel Ejecutar y depurar, elija **Python: Archivo actual** u otra configuración de depuración y, después, presione **F5** para iniciar la depuración.

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

## Resumen

En este ejercicio, el enfoque se centraba en la refactorización y mejora del código existente con la ayuda de GitHub Copilot. Ha mejorado sistemáticamente el código base reemplazando los bucles manuales y los patrones repetitivos por construcciones pythonicas, como las comprensiones de lista, las expresiones de generador y las funciones integradas. Ha usado los distintos modos de GitHub Copilot (Preguntar, Insertado, Editar y Agente) para analizar código, generar sugerencias de refactorización y aplicar mejoras directamente en Visual Studio Code. Estos cambios mejoran la legibilidad, el mantenimiento y el rendimiento del código. Con estas aptitudes, ahora puede refactorizar y modernizar proyectos de Python con confianza, lo que hace que el código base sea más sólido y eficaz a medida que continúa desarrollando nuevas características.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Si ha realizado cambios no deseados, reviertalos ahora.
