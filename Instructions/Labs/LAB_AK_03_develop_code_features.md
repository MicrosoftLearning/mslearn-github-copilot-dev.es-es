---
lab:
  title: 'Ejercicio: Desarrollo de nuevas características de código mediante GitHub Copilot'
  description: Obtenga información sobre cómo acelerar el desarrollo de nuevas características de código mediante GitHub Copilot en Visual Studio Code.
---

# Desarrollo de nuevas características de código mediante GitHub Copilot

Las características de finalización de código y chat interactivo de GitHub Copilot ayudan a los desarrolladores a escribir código más rápido y con menos errores. Proporciona sugerencias para fragmentos de código, funciones e incluso clases completas basadas en el contexto del código que se está escribiendo. En este ejercicio, usará GitHub Copilot para acelerar el desarrollo de nuevas características de código en Visual Studio Code.

Este ejercicio debería tardar en completarse **30** minutos aproximadamente.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar su propia cuenta de GitHub y suscripción de GitHub Copilot. Si no tiene una cuenta de GitHub, puede <a href="https://github.com/" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

## Antes de comenzar

El entorno de laboratorio debe incluir lo siguiente: Git 2.48 o posterior, SDK de .NET 9.0 o posterior, Visual Studio Code con la extensión Kit de desarrollo de C# y acceso a una cuenta de GitHub con GitHub Copilot habilitado.

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

## Escenario del ejercicio

Es un desarrollador que trabaja en el departamento de TI de la comunidad local. Los sistemas de back-end que admiten la biblioteca pública se han perdido en un incendio. El equipo debe desarrollar una solución temporal para ayudar al personal de la biblioteca a administrar sus operaciones hasta que se pueda reemplazar el sistema. El equipo ha elegido GitHub Copilot para acelerar el proceso de desarrollo.

Los usuarios finales probaron una versión inicial de la aplicación de biblioteca y se solicitaron varias características adicionales. El equipo ha acordado trabajar con las siguientes características:

- Disponibilidad del libro: Habilite un bibliotecario para determinar el estado de disponibilidad de un libro. Esta característica debe mostrar un mensaje que indica si un libro está disponible para el préstamo o la fecha de vencimiento de devolución si el libro está actualmente en préstamo a otro patrón.

- Préstamos de libros: Permitir que un bibliotecario preste un libro a un patrón (si el libro está disponible). Esta característica debe mostrar la opción de que un cliente reciba un libro en préstamo, actualice Loans.json con el nuevo préstamo y muestre los detalles del préstamo para el patrón.

- Reservación de libros: Permitir que un bibliotecario reserve un libro para un patrón (a menos que el libro ya esté reservado). Esta característica debe implementar un nuevo proceso de reserva de libros. Esta característica puede requerir la creación de un nuevo archivo Reservations.json junto con las nuevas clases e interfaces necesarias para admitir el proceso de reserva.

Cada miembro del equipo trabajará en una de las nuevas características y, a continuación, volverá a reunirse. Trabajará en la característica para determinar el estado de disponibilidad de un libro. Su compañero de trabajo trabajará en la característica para prestar un libro a un patrón. La última característica, para reservar un libro para un patrón, se desarrollará después de que se completen las otras dos características.

Este ejercicio incluye las siguientes tareas:

1. Configurar la aplicación de biblioteca en Visual Studio Code.

1. Use Visual Studio Code para crear un repositorio de GitHub para la aplicación de biblioteca.

1. Cree una rama de "disponibilidad de libros" en el repositorio de código.

1. Desarrollar una nueva característica de "disponibilidad de libros".

    - Use sugerencias de GitHub Copilot para ayudar a implementar el código de forma más rápida y precisa.
    - Sincronice las actualizaciones del código a la rama "disponibilidad de libros" del repositorio remoto.

1. Combine las actualizaciones de "disponibilidad del libro" en la rama principal del repositorio.

## Configurar la aplicación de biblioteca en Visual Studio Code

Debe descargar la aplicación existente, extraer los archivos de código y, a continuación, abrir la solución en Visual Studio Code.

Siga estos pasos para configurar la aplicación de la biblioteca:

1. Abra una ventana del explorador en el entorno de laboratorio.

1. Para descargar un archivo ZIP con la aplicación de biblioteca, pegue la siguiente dirección URL en la barra de direcciones del explorador: [Laboratorio de GitHub Copilot: desarrollo de características de código](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/AZ2007LabAppM3.zip)

    El archivo ZIP se denomina **AZ2007LabAppM3.zip**.

1. Extraiga los archivos del archivo **AZ2007LabAppM3.zip**.

    Por ejemplo:

    1. Vaya a la carpeta de descargas del entorno de laboratorio.

    1. Haga clic con el botón derecho en **AZ2007LabAppM3.zip** y seleccione **Extraer todo**.

    1. Seleccione **Mostrar los archivos extraídos al completar** y, a continuación, **Extraer**.

1. Abra la carpeta de archivos extraídos y, después, copie la carpeta **AccelerateDevGHCopilot** en una ubicación que sea fácil de acceder, como la carpeta Escritorio de Windows.

1. Abra la carpeta **AccelerateDevGHCopilot** en Visual Studio Code.

    Por ejemplo:

    1. Abra Visual Studio Code en el entorno de laboratorio.

    1. En Visual Studio Code, en el menú **Archivo**, seleccione **Abrir archivo**.

    1. Vaya a la carpeta Escritorio de Windows, seleccione **AccelerateDevGHCopilot** y luego **Seleccionar carpeta**.

1. En la vista EXPLORADOR DE SOLUCIONES de Visual Studio Code, compruebe la siguiente estructura de soluciones:

    - AccelerateDevGHCopilot\
        - src\
            - Library.ApplicationCore\
            - Library.Console\
            - Library.Infrastructure\
        - tests\
            - UnitTests\

1. Asegúrese de que la solución se compila correctamente.

    Por ejemplo, en la vista EXPLORADOR DE SOLUCIONES, haga clic con el botón derecho en **AccelerateDevGHCopilot**y, después, seleccione **Compilar**.

    Verá varias Advertencias, pero no debería haber ningún Errores.

## Creación del repositorio de GitHub para el código

La creación del repositorio de GitHub para el código le habilitará compartir su trabajo con otros usuarios y colaborar en el proyecto.

> **NOTA**: Use su propia cuenta de GitHub para crear un repositorio privado de GitHub para la aplicación de biblioteca.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Abra una ventana del explorador y navegue a la cuenta de GitHub.

    La página de inicio de sesión de GitHub es: [https://github.com/login](https://github.com/login).

1. Inicie sesión en su cuenta de GitHub.

1. Abra el menú de la cuenta de GitHub y seleccione **Los repositorios**.

1. Cambie a la ventana de Visual Studio Code.

1. En Visual Studio Code, abra la vista Control de código fuente.

1. Seleccione **Publicación en GitHub**.

1. Nombre del repositorio **AccelerateDevGHCopilot**.

    > **NOTA**: Si no ha iniciado sesión en GitHub en Visual Studio Code, se le pedirá que inicie sesión. Una vez que haya iniciado sesión, autorice Visual Studio Code con los permisos solicitados.

1. Seleccione **Publicar en el repositorio privado de GitHub**.

1. Observe que Visual Studio Code muestra los mensajes de estado durante el proceso de publicación.

    Cuando finalice el proceso de publicación, verá un mensaje que le informa de que el código se publicó correctamente en el repositorio de GitHub que especificó.

1. Cambie a la ventana del explorador de la cuenta de GitHub.

1. Abra el nuevo repositorio AccelerateDevGHCopilot en la cuenta de GitHub.

    Si no ve el repositorio AccelerateDevGHCopilot, actualice la página. Si sigue sin ver el repositorio, pruebe los pasos siguientes:

    1. Vaya a Visual Studio Code.
    1. Abra las notificaciones (se generó una notificación cuando se publicó el nuevo repositorio).
    1. Seleccione **Abrir en GitHub** para abrir el repositorio.

## Creación de una rama en el repositorio

Antes de empezar a desarrollar la nueva característica "disponibilidad de libros", debe crear una nueva rama en el repositorio. Esto le permite trabajar en la nueva característica sin afectar a la rama principal del repositorio. Puede combinar la nueva característica en la rama principal cuando el código esté listo.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Asegúrese de que tiene abierta la solución AccelerateDevGHCopilot en Visual Studio Code.

1. Seleccione la vista Control de código fuente y asegúrese de que el repositorio local está sincronizado con el repositorio remoto (Extracción o Sincronización).

1. En la esquina inferior izquierda de la ventana, seleccione **principal**.

1. Para crear una nueva rama, escribe **disponibilidad de libro** y después selecciona **+ Crear nueva rama**.

1. Para insertar la nueva rama en el repositorio remoto, seleccione **Publicar rama**.

## Desarrollar una nueva característica de "disponibilidad de libros"

En esta sección del ejercicio, usará GitHub Copilot para desarrollar una nueva característica para la aplicación de biblioteca. La característica solicitada permitirá a un bibliotecario comprobar si un libro está disponible para el préstamo, un escenario común que no es compatible actualmente con la aplicación de biblioteca actual.

Para implementar la característica de disponibilidad del libro, deberá completar las siguientes actualizaciones:

- Agregue una nueva acción **SearchBooks** a la enumeración **CommonActions** en CommonActions.cs.

- Actualice el método **WriteInputOptions** en ConsoleApp.cs.

    - Agregue compatibilidad con la nueva opción **CommonActions.SearchBooks**.
    - Muestra la opción para comprobar si hay un libro disponible para el préstamo.

- Actualice el método **ReadInputOptions** en ConsoleApp.cs.

    - Agregue compatibilidad con la nueva opción **CommonActions.SearchBooks**.

- Actualice el método **PatronDetails** en ConsoleApp.cs.

    - Agregue **CommonActions.SearchBooks** a **opciones** antes de llamar a **ReadInputOptions**.
    - Agregue otro **else if** para controlar la acción **SearchBooks**.
    - El bloque **else if** debe llamar a un nuevo método denominado **SearchBooks**.

- Crea un nuevo método **SearchBooks** en ConsoleApp.cs.

    - El método **SearchBooks** debe leer un título de libro proporcionado por el usuario.
    - Compruebe si un libro está disponible para préstamo y muestre un mensaje que indique:

        - "**book.title** está disponible para préstamo", o
        - "**book.title** está prestado a otro usuario. La fecha de vencimiento de la devolución es **loan.DueDate**".

GitHub Copilot Chat puede ayudarle a implementar las actualizaciones de código necesarias para completar la nueva característica.

- Puede usar sesiones de chat en línea para implementar actualizaciones de código más pequeñas y discretas en función de sus requisitos.
- Puede usar la vista Chat para trabajar en actualizaciones de código más grandes que pueden requerir un enfoque más conversacional e iterativo.

### Implementación de actualizaciones de "disponibilidad de libros" mediante chat en línea

Las sesiones de chat en línea le permiten interactuar con GitHub Copilot directamente en el editor de código. Puede usar el chat en línea para formular preguntas, solicitar sugerencias de código y obtener explicaciones para el código generado por GitHub Copilot.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Abra la vista EXPLORADOR DE SOLUCIONES.

1. Expanda el proyecto **Library.Console**.

1. Abre el archivo CommonActions.cs y selecciona la enumeracion **CommonActions**.

    Debes agregar una nueva acción **SearchBooks** a **CommonActions**.

1. Abra el chat en línea y escriba el siguiente símbolo del sistema:

    ```plaintext
    Update selection to include a new `SearchBooks` action.
    ```

    GitHub Copilot debe sugerir una actualización de código que agregue la nueva acción **SearchBooks** a la enumeración **CommonActions**.

1. Revise la actualización sugerida y seleccione **Aceptar**.

    El código actualizado debe tener un aspecto similar al siguiente fragmento de código:

    ```csharp

    public enum CommonActions
    {
        Repeat = 0,
        Select = 1,
        Quit = 2,
        SearchPatrons = 4,
        RenewPatronMembership = 8,
        ReturnLoanedBook = 16,
        ExtendLoanedBook = 32,
        SearchBooks = 64
    }

    ```

1. Abra el archivo ConsoleApp.cs.

1. Busca y selecciona el método **WriteInputOptions**.

    Debes agregar compatibilidad con la nueva opción **CommonActions.SearchBooks**. Si la opción **SearchBooks** está marcada, muestre la opción para comprobar si hay un libro disponible para el préstamo.

1. Abra el chat en línea y escriba el siguiente símbolo del sistema:

    ```plaintext
    Update selection to include an option for the `CommonActions.SearchBooks` action. Use the letter "b" and the message "to check for book availability".
    ```

    GitHub Copilot debe sugerir una actualización de código que agregue un nuevo bloque **if** para la acción **SearchBooks**.

1. Revise la actualización sugerida y seleccione **Aceptar**.

    La actualización sugerida debe ser similar al siguiente fragmento de código:

    ```csharp

    static void WriteInputOptions(CommonActions options)
    {
        Console.WriteLine("Input Options:");
        if (options.HasFlag(CommonActions.ReturnLoanedBook))
        {
            Console.WriteLine(" - \"r\" to mark as returned");
        }
        if (options.HasFlag(CommonActions.ExtendLoanedBook))
        {
            Console.WriteLine(" - \"e\" to extend the book loan");
        }
        if (options.HasFlag(CommonActions.RenewPatronMembership))
        {
            Console.WriteLine(" - \"m\" to extend patron's membership");
        }
        if (options.HasFlag(CommonActions.SearchPatrons))
        {
            Console.WriteLine(" - \"s\" for new search");
        }
        if (options.HasFlag(CommonActions.SearchBooks))
        {
            Console.WriteLine(" - \"b\" to check for book availability");
        }
        if (options.HasFlag(CommonActions.Quit))
        {
            Console.WriteLine(" - \"q\" to quit");
        }
        if (options.HasFlag(CommonActions.Select))
        {
            Console.WriteLine("Or type a number to select a list item.");
        }
    }

    ```

1. Desplácese hacia arriba ligeramente para buscar y, a continuación, seleccione el método **ReadInputOptions**.

    Una vez más, debe agregar compatibilidad con la nueva opción **CommonActions.SearchBooks**. Incluye un caso que controle que el usuario seleccione la acción **SearchBooks**.

1. Abra el chat en línea y escriba el siguiente símbolo del sistema:

    ```plaintext
    Update selection to include an option for the `CommonActions.SearchBooks` action.
    ```

    GitHub Copilot debe sugerir una actualización que agregue un nuevo **caso** que controle que el usuario seleccione la acción **SearchBooks**.

1. Revise la actualización sugerida y seleccione **Aceptar**.

    La actualización sugerida debe ser similar al siguiente fragmento de código:

    ```csharp

    static CommonActions ReadInputOptions(CommonActions options, out int optionNumber)
    {
        CommonActions action;
        optionNumber = 0;
        do
        {
            Console.WriteLine();
            WriteInputOptions(options);
            string? userInput = Console.ReadLine();

            action = userInput switch
            {
                "q" when options.HasFlag(CommonActions.Quit) => CommonActions.Quit,
                "s" when options.HasFlag(CommonActions.SearchPatrons) => CommonActions.SearchPatrons,
                "m" when options.HasFlag(CommonActions.RenewPatronMembership) => CommonActions.RenewPatronMembership,
                "e" when options.HasFlag(CommonActions.ExtendLoanedBook) => CommonActions.ExtendLoanedBook,
                "r" when options.HasFlag(CommonActions.ReturnLoanedBook) => CommonActions.ReturnLoanedBook,
                "b" when options.HasFlag(CommonActions.SearchBooks) => CommonActions.SearchBooks,
                _ when int.TryParse(userInput, out optionNumber) => CommonActions.Select,
                _ => CommonActions.Repeat
            };

            if (action == CommonActions.Repeat)
            {
                Console.WriteLine("Invalid input. Please try again.");
            }
        } while (action == CommonActions.Repeat);
        return action;
    }

    ```

1. Desplázate hacia abajo para buscar y después selecciona el método **PatronDetails**.

    Hay dos cosas que debe realizar:

    - Debes agregar **CommonActions.SearchBooks** a las **opciones** antes de llamar a **ReadInputOptions**.
    - También debes agregar un **else if** para controlar la acción **SearchBooks**. El bloque **else if** debe llamar a un nuevo método denominado **SearchBooks**.

    Puede abordar ambos requisitos con el mismo mensaje.

1. Abra el chat en línea y escriba el siguiente símbolo del sistema:

    ```plaintext
    Update selection to add `CommonActions.SearchBooks` to `options` before calling `ReadInputOptions`. Add an `else if` block to handle the `SearchBooks` action. The `else if` block should call a new method named `SearchBooks`.
    ```

    GitHub Copilot debe sugerir una actualización de código que agregue **CommonActions.SearchBooks** a las **opciones** antes de llamar a **ReadInputOptions**.

1. Revise la actualización sugerida y seleccione **Aceptar**.

    ```csharp

    async Task<ConsoleState> PatronDetails()
    {
        Console.WriteLine($"Name: {selectedPatronDetails.Name}");
        Console.WriteLine($"Membership Expiration: {selectedPatronDetails.MembershipEnd}");
        Console.WriteLine();
        Console.WriteLine("Book Loans:");
        int loanNumber = 1;
        foreach (Loan loan in selectedPatronDetails.Loans)
        {
            Console.WriteLine($"{loanNumber}) {loan.BookItem!.Book!.Title} - Due: {loan.DueDate} - Returned: {(loan.ReturnDate != null).ToString()}");
            loanNumber++;
        }

        CommonActions options = CommonActions.SearchPatrons | CommonActions.Quit | CommonActions.Select | CommonActions.RenewPatronMembership | CommonActions.SearchBooks;
        CommonActions action = ReadInputOptions(options, out int selectedLoanNumber);
        if (action == CommonActions.Select)
        {
            if (selectedLoanNumber >= 1 && selectedLoanNumber <= selectedPatronDetails.Loans.Count())
            {
                var selectedLoan = selectedPatronDetails.Loans.ElementAt(selectedLoanNumber - 1);
                selectedLoanDetails = selectedPatronDetails.Loans.Where(l => l.Id == selectedLoan.Id).Single();
                return ConsoleState.LoanDetails;
            }
            else
            {
                Console.WriteLine("Invalid book loan number. Please try again.");
                return ConsoleState.PatronDetails;
            }
        }
        else if (action == CommonActions.Quit)
        {
            return ConsoleState.Quit;
        }
        else if (action == CommonActions.SearchPatrons)
        {
            return ConsoleState.PatronSearch;
        }
        else if (action == CommonActions.RenewPatronMembership)
        {
            var status = await _patronService.RenewMembership(selectedPatronDetails.Id);
            Console.WriteLine(EnumHelper.GetDescription(status));
            // reloading after renewing membership
            selectedPatronDetails = (await _patronRepository.GetPatron(selectedPatronDetails.Id))!;
            return ConsoleState.PatronDetails;
        }
        else if (action == CommonActions.SearchBooks)
        {
            return await SearchBooks();
        }

        throw new InvalidOperationException("An input option is not handled.");
    }

    ```

    > **NOTA**: El código sugerido por el chat en línea puede incluir código auxiliar para el método **SearchBooks**. Puede aceptar ese código. Implementará el método **SearchBooks** en la sección siguiente.

### Implementación de un método SearchBooks mediante la vista Chat

Queda un paso para implementar las actualizaciones de "disponibilidad de libros", crear el método **SearchBooks**. El método **SearchBooks** leerá un título de libro proporcionado por el usuario, comprobará si un libro está disponible para préstamo y mostrará un mensaje que indica el estado de disponibilidad del libro. Usará la vista Chat para evaluar los requisitos e implementar el método **SearchBooks**.

La vista Chat de GitHub Copilot proporciona un entorno conversacional e interactivo que no está disponible al usar chat en línea. Puede usar la vista Chat para formular preguntas, solicitar sugerencias de código y obtener explicaciones para el código generado por GitHub Copilot. La vista Chat admite los tres modos siguientes:

- Modo de pregunta: El modo Preguntar se usa para comprender mejor su código base, ideas de lluvia de ideas y ayuda con las tareas de codificación. Las sugerencias de código generadas en el modo Preguntar se pueden implementar directamente en el código base o copiarlas en el Portapapeles.
- Modo de edición: El modo de edición se usa para realizar cambios en el código, como refactorizar o agregar nuevas características. El modo de edición puede realizar modificaciones en varios archivos del proyecto.
- Modo de agente: El modo de agente se usa para definir una tarea de alto nivel e iniciar una sesión de edición de código agente para realizar esa tarea. En el modo de agente, Copilot planea de forma autónoma el trabajo necesario y determina los archivos y el contexto pertinentes. El agente puede realizar cambios en el código, ejecutar pruebas e incluso implementar la aplicación.

Usará los modos Preguntar y Editar para implementar el método **SearchBooks**.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Dedica un minuto a tener en cuenta los requisitos de proceso del método **SearchBooks**.

    ¿Cuál es el proceso que necesita completar el método? ¿Cuál es el tipo de valor devuelto para este método? ¿Requiere parámetros?

    El método **SearchBooks** debe implementar el siguiente proceso:

    1. Pida al usuario un título de libro.
    1. Lea el título del libro proporcionado por el usuario.
    1. Compruebe si hay un libro disponible para el préstamo.
    1. Muestra un mensaje que indica una de las siguientes opciones:

        - "**{book.title}** está disponible para préstamo"
        - "**{book.title}** está prestado a otro usuario. La fecha de vencimiento de la devolución es **{loan.DueDate}**".

    Para compilar las opciones de mensaje, el código tendrá que acceder a los siguientes archivos JSON:

    - **Books.json** es necesario para encontrar el **Título** y el **BookId** coincidentes.
    - **Loans.json** es necesario para encontrar la **ReturnDate** y la **DueDate** del **BookItemId** correspondiente. **BookItemId** es el mismo que **BookId** en **Books.json**.

1. Asegúrate de que tienes el siguiente método **SearchBooks** creado en el archivo ConsoleApp.cs:

    ```csharp

    async Task<ConsoleState> SearchBooks()
    {

        return ConsoleState.PatronDetails;
    }

    ```

    > **NOTA**: Asegúrese de quitar los comentarios de código creados por GitHub Copilot. Los comentarios innecesarios e inexactos pueden influir negativamente en las sugerencias de GitHub Copilot.

1. Selecciona el método **SearchBooks**.

1. Abra la vista Chat y escriba el siguiente símbolo del sistema:

    ```plaintext
    Update selection to obtain a book title. Prompt the user to "Enter a book title to search for". Read the user input and ensure the book title isn't null.
    ```

1. Revise la actualización sugerida.

    La actualización sugerida debe ser similar al siguiente fragmento de código:

    ```csharp

    async Task<ConsoleState> SearchBooks()
    {
        string? bookTitle = null;
        while (string.IsNullOrWhiteSpace(bookTitle))
        {
            Console.Write("Enter a book title to search for: ");
            bookTitle = Console.ReadLine();
        }
    
        // Placeholder for further logic to search for the book
        Console.WriteLine($"Searching for the book titled \"{bookTitle}\"...");
    
        return ConsoleState.PatronDetails;
    }

    ```

1. Mantenga el puntero del ratón sobre el código sugerido y, a continuación, seleccione **Apply to src\\Library.Console\\ConsoleApp.cs**.

    El código sugerido debe estar visible en el editor de código, con opciones para **Mantener** o **Deshacer**.

1. En el editor de código, para aceptar el código sugerido, seleccione **Mantener**.

1. Selecciona el método **SearchBooks**.

1. Use las operaciones de arrastrar y colocar para agregar los siguientes archivos al contexto de chat:

    (desde el proyecto Library.Console)
    - ConsoleApp.cs
    - Program.cs
    - Books.json
    - Loans.json
    - BookItems.json

    (desde el proyecto Library.Infrastructure)
    - JsonData.cs
    - JsonLoanRepository.cs

1. Escriba lo siguiente:

    ```plaintext
    @workspace  Explain how to update the `SearchBooks` method and ConsoleApps class to find a matching book title in the `Books.json` file. Use the user supplied book title to find a matching book. If a book is found, use Loans.json to check if the book is available for loan. If the book has been returned, display a message stating "`book.title` is available for loan". If the book is on loan, display a message stating "`book.title` is on loan to another patron. The return due date is `loan.DueDate`".
    ```

1. Dedique un minuto a revisar las actualizaciones sugeridas.

    Tenga en cuenta lo siguiente:

    - La respuesta incluye una explicación detallada de las actualizaciones sugeridas.
    - La clase ConsoleApp requiere un objeto JsonData para acceder a Books.json y Loans.json. El código sugerido usa la inserción de dependencias para pasar el objeto JsonData al constructor de clase ConsoleApp.
    - El método SearchBooks debe actualizarse con lógica que determina la disponibilidad del título del libro y muestra un mensaje adecuado. El código sugerido usa consultas LINQ para comprobar el estado del préstamo.
    - El archivo Program.cs debe actualizarse para pasar el objeto JsonData a la clase ConsoleApp.

    La respuesta debe incluir la siguiente información:

    ```plaintext

    1. Dependency Injection:
    
        Added JsonData as a dependency to the ConsoleApp constructor to access the JSON data files.

    2. Book Search:
    
        Used FirstOrDefault to find a book in Books.json that matches the user-supplied title (case-insensitive).

    3. Book Item Lookup:
    
        Retrieved the corresponding BookItem using the BookId from BookItems.json.

    4. Loan Check:
    
        Checked Loans.json for an active loan (i.e., a loan with a null ReturnDate) for the BookItem.

    5. Output Messages:
    
        Displayed whether the book is available for loan or currently on loan with the due date.

    Integration in Program.cs

        Ensure that JsonData is registered in the dependency injection container in Program.cs:

    ```

    Puede usar el modo **Preguntar** de la vista chat para analizar las actualizaciones de código y, a continuación, usar el modo de **edición** para implementar las actualizaciones de código.

1. Use la respuesta de GitHub Copilot para construir un nuevo mensaje.

    Por ejemplo, puede usar la sección de explicación para crear la siguiente indicación:

    ```plaintext

    Add JsonData as a dependency to the ConsoleApp constructor to access the JSON data files. Use FirstOrDefault to find a book in Books.json that matches the user-supplied title (case-insensitive). Retrieve the corresponding BookItem using the BookId from BookItems.json. Check Loans.json for an active loan (loan.ReturnDate == null) for the BookItem. Display whether the book is available for loan or currently on loan with the due date. Ensure that JsonData is registered in the dependency injection container in Program.cs.

    ```

    Puede ajustar la solicitud para lograr requisitos específicos. Por ejemplo, si desea que se muestre un mensaje específico al usuario final, puede agregar el requisito a la indicación:

    ```plaintext

    Add JsonData as a dependency to the ConsoleApp constructor to access the JSON data files. Use FirstOrDefault to find a book in Books.json that matches the user-supplied title (case-insensitive). Retrieve the corresponding BookItem using the BookId from BookItems.json. Check Loans.json for an active loan (loan.ReturnDate == null) for the BookItem. Display whether the book is available for loan or currently on loan with the due date. Ensure that JsonData is registered in the dependency injection container in Program.cs. If the book has been returned, display a message stating "`book.title` is available for loan". If the book is on loan, display a message stating "`book.title` is on loan to another patron. The return due date is `loan.DueDate`".

    ```

1. Para cambiar la vista Chat al modo de edición, seleccione **Establecer modo** y, a continuación, seleccione **Editar**.

    Cuando se le pida que inicie una nueva sesión, seleccione **Sí**.

1. Use las operaciones de arrastrar y colocar para agregar los siguientes archivos al contexto de chat:

    (desde el proyecto Library.Console)
    - ConsoleApp.cs
    - Program.cs
    - Books.json
    - Loans.json
    - BookItems.json

    (desde el proyecto Library.Infrastructure)
    - JsonData.cs
    - JsonLoanRepository.cs

1. Selecciona el método **SearchBooks**.

1. Escriba lo siguiente:

    ```plaintext

    Add JsonData as a dependency to the ConsoleApp constructor to access the JSON data files. Use FirstOrDefault to find a book in Books.json that matches the user-supplied title (case-insensitive). Retrieve the corresponding BookItem using the BookId from BookItems.json. Check Loans.json for an active loan (loan.ReturnDate == null) for the BookItem. Display whether the book is available for loan or currently on loan with the due date. Ensure that JsonData is registered in the dependency injection container in Program.cs. If the book has been returned, display a message stating "`book.title` is available for loan". If the book is on loan, display a message stating "`book.title` is on loan to another patron. The return due date is `loan.DueDate`".

    ```

1. Dedique un minuto a revisar las actualizaciones sugeridas en el archivo ConsoleApp.cs.

    Puede usar **Anterior** y **Siguiente** para navegar por las actualizaciones de código sugeridas, o bien puede desplazarse manualmente por el archivo.

    **ConsoleApp.cs**

    Las actualizaciones de código que agregan la dependencia **JsonData** al constructor **ConsoleApp** se pueden encontrar cerca de la parte superior de la clase ConsoleApp.

    ```csharp

    JsonData _jsonData;

    public ConsoleApp(ILoanService loanService, IPatronService patronService, IPatronRepository patronRepository, ILoanRepository loanRepository, JsonData jsonData)
    {
        _patronRepository = patronRepository;
        _loanRepository = loanRepository;
        _loanService = loanService;
        _patronService = patronService;
        _jsonData = jsonData;
    }

    ```

    Las actualizaciones de código que comprueban si hay un libro disponible para el préstamo se pueden encontrar en el método **SearchBooks**.

    ```csharp

    async Task<ConsoleState> SearchBooks()
    {
        string? bookTitle = null;
        while (string.IsNullOrWhiteSpace(bookTitle))
        {
            Console.Write("Enter a book title to search for: ");
            bookTitle = Console.ReadLine();
        }

        await _jsonData.EnsureDataLoaded();

        var book = _jsonData.Books!.FirstOrDefault(b => string.Equals(b.Title, bookTitle, StringComparison.OrdinalIgnoreCase));
        if (book == null)
        {
            Console.WriteLine($"No book found with the title \"{bookTitle}\".");
            return ConsoleState.PatronDetails;
        }

        var bookItem = _jsonData.BookItems!.FirstOrDefault(bi => bi.BookId == book.Id);
        if (bookItem == null)
        {
            Console.WriteLine($"No book item found for the title \"{book.Title}\".");
            return ConsoleState.PatronDetails;
        }

        var loan = _jsonData.Loans!.FirstOrDefault(l => l.BookItemId == bookItem.Id && l.ReturnDate == null);
        if (loan == null)
        {
            Console.WriteLine($"\"{book.Title}\" is available for loan.");
        }
        else
        {
            Console.WriteLine($"\"{book.Title}\" is on loan to another patron. The return due date is {loan.DueDate}.");
        }

        return ConsoleState.PatronDetails;
    }

    ```

    **Program.cs**

    El código para registrar JsonData y ConsoleApp para la inserción de dependencias ya estaba disponible en el archivo Program.cs.

    ```csharp

    services.AddSingleton<JsonData>();
    services.AddSingleton<ConsoleApp>();

    ```

1. En la vista Chat, para mantener todas las modificaciones, seleccione **Mantener**.

    Revise siempre las sugerencias de GitHub Copilot antes de aceptar actualizaciones.

    Si no está seguro de las actualizaciones sugeridas, puede aceptar los cambios y, a continuación, pedir a GitHub Copilot una explicación. Puede revertir las modificaciones si decide que no quiere las actualizaciones.

    > **NOTA**: Si GitHub Copilot sugiere dar formato a la fecha de devolución mediante un formato específico de la referencia cultural, asegúrese de que se agrega una instrucción `using System.Globalization;` al principio del archivo ConsoleApp.cs.

1. Asegúrese de que ha aceptado actualizaciones en los archivos ConsoleApp.cs y Program.cs.

1. Desplácese hasta la parte superior del archivo ConsoleApp.cs y busque la siguiente línea de código:

    ```csharp

    JsonData _jsonData;

    ```

1. Si JsonData no se reconoce en la clase ConsoleApp, agregue la siguiente instrucción using encima de la clase ConsoleApp.

    ```csharp
    
    using Library.Infrastructure.Data;
    
    ```

1. Abra la vista EXPLORADOR DE SOLUCIONES de Visual Studio Code.

1. Compile la solución y asegúrese de que el código no introdujo ningún error.

    Verá mensajes de advertencia, pero no debería haber ningún error.

    Para compilar la solución mediante la vista EXPLORADOR DE SOLUCIONES, haga clic con el botón derecho en **AccelerateDevGHCopilot** y, a continuación, seleccione **Compilar**.

## Combinar las actualizaciones de "disponibilidad del libro" en la rama principal del repositorio

Es importante probar el código antes de combinarlo en la rama principal del repositorio. Las pruebas garantizan que el código funciona según lo previsto y no presenta ningún problema nuevo. En este ejercicio, usará pruebas manuales para comprobar que la característica "disponibilidad de libros" funciona según lo previsto.

En esta sección del ejercicio, completará las siguientes tareas:

1. Pruebe la característica "disponibilidad del libro".
1. Sincronice los cambios con el repositorio remoto.
1. Cree una solicitud de incorporación de cambios para combinar los cambios en la rama principal del repositorio.

### Prueba de la característica "disponibilidad del libro"

Las pruebas manuales se pueden usar para comprobar que la nueva característica funciona según lo previsto. El uso de un origen de datos que se puede comprobar es importante. En este caso, se usan los archivos **Books.json** y **Loans.json** para comprobar que la nueva característica informa correctamente del estado de disponibilidad de un libro.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Para ejecutar la aplicación, haga clic con el botón derecho en **Library.Console**, seleccione **Depurar** y, a continuación, seleccione **Iniciar nueva instancia**.

1. Cuando se le solicite un nombre de patrón, escriba **One** y presione Entrar.

    Debería ver una lista de clientes que coinciden con la consulta de búsqueda.

1. En el símbolo del sistema "Opciones de entrada", escriba **2** y presione Entrar.

    Al escribir **2**, se selecciona el segundo patrón de la lista.

    Debería ver el nombre del patrón y el estado de suscripción seguido de los detalles del préstamo del libro.

1. En el símbolo del sistema "Opciones de entrada", escriba **b** y presione Entrar.

    Al escribir **b** selecciona la opción para buscar el estado de disponibilidad de un libro.

    Debería ver un mensaje para escribir un título de libro.

1. Escriba **Book One** y presione Entrar.

    En los datos originales que descargó, **Book One** está actualmente en préstamo para **Patron Forty-Nine**, por lo que no debería estar disponible.

1. Compruebe que la aplicación muestra un mensaje que indica que el libro está en préstamo a otro patrón.

1. En el símbolo del sistema "Opciones de entrada", escriba **b** y presione Entrar.

1. Escriba **Book Nineteen** y presione Entrar.

1. Compruebe que la aplicación muestra un mensaje que indica que el libro está disponible para el préstamo.

1. En el símbolo del sistema "Opciones de entrada", escriba **q** y presione Entrar.

1. Detenga la sesión de depuración.

1. Use la vista EXPLORADOR para buscar y abrir el archivo **Loans.json**.

    El archivo Loans.json se usa para realizar un seguimiento del estado de préstamo de cada libro. Puedes usar el archivo Loans.json para comprobar que el estado de disponibilidad de Book One y Book Nineteen es correcto.

    El archivo Loans.json actualizado debe encontrarse en la carpeta **Library.Console\bin\Debug\net8.0\Json** o en la carpeta **Library.Console\Json**.

    - Si usas el depurador de Visual Studio Code para ejecutar la aplicación, el archivo Loans.json actualizado debe encontrarse en la carpeta **Library.Console\bin\Debug\net8.0\Json**.

    - Si usas un comando **dotnet run** de la carpeta **AccelerateDevGHCopilot\src\Library.Console** para ejecutar la aplicación, el archivo Loans.json actualizado debe encontrarse en la carpeta **Library.Console\Json**.

1. Comprueba que el Id. de préstamo 37 y el Id. de préstamo 46 son ambos para el Book One (**"BookItemId": 1**).

    Los identificadores de préstamo se enumeran secuencialmente en el archivo Loans.json.

    - El id. de préstamo 37 debe tener un valor **ReturnDate** de **2024-01-17**, lo que indica que el libro se devolvió en esa fecha.
    - El id. de préstamo 46 debe tener un valor **ReturnDate** **nulo**, lo que indica que el libro está actualmente en préstamo (prestado en **2024-07-09**, pero no devuelto).

    El valor **ReturnDate** se usa para determinar si el libro está actualmente en préstamo. Si el valor **ReturnDate** es **null**, el libro está actualmente en préstamo.

1. Compruebe que el id. de préstamo 34 es para el Book Nineteen (**"BookItemId": 19**) y que se le ha asignado un valor **ReturnDate**.

### Sincronización de los cambios con el repositorio remoto

1. Seleccione la vista Control de código fuente.

1. Asegúrese de que los archivos que ha actualizado se enumeran en **Cambios**.

    Debería ver los archivos CommonActions.cs y ConsoleApp.cs que aparecen en **Cambios**. También se puede enumerar el archivo Program.cs.

1. Use GitHub Copilot para generar un mensaje para el **Confirmar**.

    ![Captura de pantalla que muestra el botón Generar mensaje de confirmación con Copilot.](./Media/m03-github-copilot-commit-message.png)

1. Para almacenar provisionalmente y confirmar los cambios, seleccione **Confirmar** y, a continuación, seleccione **Sí**.

1. Para sincronizar los cambios en el repositorio remoto, seleccione **Sincronizar cambios**.

### Creación de una solicitud de incorporación de cambios para combinar los cambios en la rama principal

Ha implementado la característica que permite a un bibliotecario determinar el estado de disponibilidad de un libro. Ahora debe combinar los cambios en la rama principal del repositorio. Puede crear una solicitud de incorporación de cambios para combinar los cambios en la rama principal.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Abra el repositorio de GitHub en un explorador web.

    Para abrir el repositorio de GitHub desde Visual Studio Code:

    1. En la esquina inferior izquierda de la ventana de Visual Studio Code, seleccione **book-availability**.
    1. En el menú contextual, a la derecha de la rama **book-availability**, seleccione el icono **Abrir en GitHub**.

1. En la página del repositorio de GitHub, seleccione la pestaña **Comparar y solicitud de cambios**.

1. Asegúrese de que **Base** especifica **main**, **compare** especifica **book-availability** y **Able to merge** está marcado.

1. En **Agregar una descripción**, seleccione el botón Acciones de Copilot (el icono de GitHub Copilot) y, a continuación, seleccione la opción para generar un resumen.

    > **NOTA**: El plan Gratuito de GitHub Copilot no admite la característica de resumen de solicitudes de incorporación de cambios en este momento.

    Si usa el plan Gratis de GitHub Copilot, puede escribir su propio resumen o usar el resumen siguiente para completar la solicitud de incorporación de cambios.

    ```plaintext

    This pull request introduces a new feature to the library console application: the ability to search for books and check their availability. It also includes updates to dependency injection and the CommonActions enumeration to support this functionality. Below are the most important changes grouped by theme.

    New Feature: Book Search

    Added a new SearchBooks action to the CommonActions enumeration (src/Library.Console/CommonActions.cs).

    Updated PatronDetails method to handle the SearchBooks action, including a new SearchBooks method that allows users to search for a book by title and check its availability (src/Library.Console/ConsoleApp.cs).

    Modified ReadInputOptions and WriteInputOptions methods to include the new SearchBooks option (src/Library.Console/ConsoleApp.cs).

    Dependency Injection Updates

    Added JsonData as a dependency in the ConsoleApp constructor and ensured it is registered in the DI container before ConsoleApp (src/Library.Console/ConsoleApp.cs, src/Library.Console/Program.cs).

    ```

1. Una vez generado el resumen, seleccione **Vista previa**.

1. Dedique un minuto a revisar el resumen.

    El resumen de la solicitud de incorporación de cambios generado por GitHub Copilot debe ser similar al ejemplo siguiente:

    ![Captura de pantalla que muestra un resumen de la solicitud de incorporación de cambios generado mediante una cuenta de GitHub Copilot Enterprise.](./Media/m03-github-copilot-pull-request-summary.png)

1. Seleccione **Crear solicitud de incorporación de cambios**.

1. Si se pasan todas las comprobaciones y no hay conflictos con la rama base, seleccione **Combinar solicitud de incorporación de cambios** y, a continuación, seleccione **Confirmar combinación**.

    Ten en cuenta que puedes eliminar la rama **book-availability** después de combinar los cambios. Para eliminar la rama, seleccione **Eliminar rama**.

1. Vuelva a la ventana de Visual Studio Code.

1. Cambie a la rama **principal** del repositorio.

1. Abra la vista Control de código fuente y, a continuación, **extraiga** los cambios del repositorio remoto.

1. Compruebe que la característica de disponibilidad de la reserva está disponible en la rama **principal**.

## Resumen

En este ejercicio, ha aprendido a usar GitHub Copilot para desarrollar una nueva característica de código para una aplicación de C#. Ha desarrollado la característica en una nueva rama mediante la vista de chat y chat en línea de GitHub Copilot, ha probado el código y, a continuación, ha combinado los cambios en la rama principal del repositorio. También ha usado GitHub Copilot para generar un mensaje de confirmación y un resumen de la solicitud de incorporación de cambios.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Si ha realizado algún cambio, reviértalos ahora.
