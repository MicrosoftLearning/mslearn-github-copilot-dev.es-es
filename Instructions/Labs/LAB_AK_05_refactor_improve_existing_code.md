---
lab:
  title: "Ejercicio: Refactorización de código existente mediante GitHub\_Copilot"
  description: "Obtenga información sobre cómo refactorizar y mejorar las secciones de código existentes mediante GitHub\_Copilot en Visual\_Studio Code."
---

# Refactorización de código existente mediante GitHub Copilot

GitHub Copilot se puede usar para evaluar todo el código base y sugerir actualizaciones que le ayuden a refactorizar y mejorar el código. En este ejercicio, usará GitHub Copilot para refactorizar secciones especificadas de una aplicación de C# mientras realiza mejoras en la calidad, la confiabilidad, el rendimiento y la seguridad del código.

Este ejercicio debería tardar en completarse **30** minutos aproximadamente.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar una cuenta de GitHub y una suscripción de GitHub Copilot propias. Si no tiene una cuenta de GitHub, puede <a href="https://github.com/" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

## Antes de comenzar

El entorno de laboratorio debe incluir lo siguiente: Git 2.48 o posterior, SDK de .NET 9.0 o posterior, Visual Studio Code con la extensión Kit de desarrollo de C# y acceso a una cuenta de GitHub con GitHub Copilot habilitado.

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

## Escenario del ejercicio

Es un desarrollador que trabaja en el departamento de TI de la comunidad local. Los sistemas de back-end que admiten la biblioteca pública se han perdido en un incendio. El equipo debe desarrollar una solución temporal para ayudar al personal de la biblioteca a administrar sus operaciones hasta que se pueda reemplazar el sistema. El equipo ha elegido GitHub Copilot para acelerar el proceso de desarrollo.

Ha entregado una versión inicial de la aplicación de biblioteca para su revisión. El equipo de revisión ha identificado oportunidades para mejorar la calidad, el rendimiento, la legibilidad, el mantenimiento y la seguridad del código.

Se le han asignado las siguientes actualizaciones:

1. Refactorizar la clase EnumHelper para usar diccionarios estáticos en lugar de la reflexión.

    - El uso de diccionarios estáticos mejorará el rendimiento (al reducir la sobrecarga de reflexión).
    - La eliminación de la reflexión también mejora la legibilidad, el mantenimiento y la seguridad del código.

1. Refactorizar los métodos de acceso a datos para usar LINQ (Language Integrated Query) en lugar de bucles foreach.

    - El uso de LINQ proporciona una manera más concisa y legible de consultar colecciones, bases de datos y documentos XML.
    - El uso de LINQ puede mejorar la legibilidad, el mantenimiento y el rendimiento del código.

Este ejercicio incluye las siguientes tareas:

1. Configurar la aplicación de biblioteca en Visual Studio Code.
1. Analizar y refactorizar el código mediante la vista Chat en los modos Preguntar y Editar.
1. Refactorizar el código mediante chat en línea y la vista Chat en los modos Editar y Agente.

## Configurar la aplicación de biblioteca en Visual Studio Code

Debe descargar la aplicación existente, extraer los archivos de código y, después, abrir la solución en Visual Studio Code.

Siga estos pasos para configurar la aplicación de la biblioteca:

1. Abra una ventana del explorador en el entorno de laboratorio.

1. Para descargar un archivo ZIP con la aplicación de biblioteca, pegue la siguiente dirección URL en la barra de direcciones del explorador: [Laboratorio de GitHub Copilot: Refactorización de código existente](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/AZ2007LabAppM5.zip)

    El archivo ZIP se denomina **AZ2007LabAppM5.zip**.

1. Extraiga los archivos del archivo **AZ2007LabAppM5.zip**.

    Por ejemplo:

    1. Vaya a la carpeta de descargas del entorno de laboratorio.

    1. Haga clic con el botón derecho en **AZ2007LabAppM5.zip** y seleccione **Extraer todo**.

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

## Análisis y refactorización de código mediante la vista Chat en modo Preguntar y Editar

La reflexión es una característica eficaz que permite inspeccionar y manipular objetos en tiempo de ejecución. Sin embargo, la reflexión puede ser lenta y hay posibles riesgos de seguridad asociados a la reflexión que se deben tener en cuenta.

Necesita:

1. Analice el área de trabajo e investigue cómo abordar la tarea asignada.
1. Refactorizar la clase EnumHelper para usar diccionarios estáticos en lugar de la reflexión.

### Análisis de la clase EnumHelper mediante la vista Chat en modo Preguntar

La vista chat de GitHub Copilot tiene tres modos: **Preguntar**, **Editar** y **Agente**. Cada modo está diseñado para diferentes tipos de interacciones con GitHub Copilot.

- **Preguntar**: Use este modo para hacer preguntas a GitHub Copilot sobre el código base. Puede pedirle a GitHub Copilot que explique el código, sugiera cambios o proporcione información sobre el código base.
- **Editar**: Use este modo para editar los archivos de código seleccionados. Puede usar GitHub Copilot para refactorizar el código, agregar comentarios o realizar otros cambios en el código.
- **Agente**: Use este modo para ejecutar GitHub Copilot como un agente. Puede GitHub Copilot para ejecutar comandos, ejecutar código o realizar otras tareas en el área de trabajo.

En esta sección del ejercicio, usará la vista Chat en modo Preguntar para analizar la asignación de programación.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. En la vista EXPLORADOR DE SOLUCIONES, expanda la carpeta **Library.ApplicationCore** y después la carpeta **Enums**.

1. Abra el archivo EnumHelper.cs y revise el código existente.

    ```csharp
    using System.ComponentModel;
    using System.Reflection;
    
    namespace Library.ApplicationCore.Enums;
    
    public static class EnumHelper
    {
        public static string GetDescription(Enum value)
        {
            if (value == null)
                return string.Empty;
    
            FieldInfo fieldInfo = value.GetType().GetField(value.ToString())!;
    
            DescriptionAttribute[] attributes =
                (DescriptionAttribute[])fieldInfo.GetCustomAttributes(typeof(DescriptionAttribute), false);
    
            if (attributes != null && attributes.Length > 0)
            {
                return attributes[0].Description;
            }
            else
            {
                return value.ToString();
            }
        }
    }
    ```

1. Abra la vista GitHub Copilot Chat.

    La vista Chat proporciona una interfaz de conversación administrada para interactuar con GitHub Copilot.

    Puede alternar la vista Chat entre abierta y cerrada mediante el botón **Alternar chat**, que se encuentra en la parte superior de la ventana de Visual Studio Code, justo a la derecha del cuadro de texto de búsqueda.

    ![Recorte de pantalla en el que se muestra el botón Alternar chat de Copilot.](./Media/m01-github-copilot-toggle-chat.png)

    También puede usar el método abreviado de teclado **Ctrl+Alt+I** para alternar la vista Chat.

1. Observe que la vista Chat se abre en modo **Preguntar** de manera predeterminada.

    El modo de Chat actual se muestra cerca de la esquina inferior derecha de la vista Chat. Las respuestas de chat se muestran en la vista Chat cuando trabaja en el modo **Preguntar**.

1. Seleccione el código en el archivo EnumHelper.cs.

1. Revise y después envíe el mensaje siguiente:

    ```plaintext
    @workspace Explain how the GetDescription method uses reflection to assign the return value.
    ```

1. Dedique un minuto a revisar la respuesta.

    El método **GetDescription** usa la reflexión para recuperar el atributo description de un parámetro de enumeración denominado **value**.

    El método comprueba si el parámetro **value** es null. Si lo es, el método devuelve una matriz vacía. De lo contrario, usa la reflexión para obtener la información de campo del valor de enumeración y recupera los atributos de tipo **DescriptionAttribute**. Si se encuentran atributos, devuelve la descripción; de lo contrario, devuelve la representación de cadena del valor de enumeración.

1. Revise y después envíe el mensaje siguiente:

    ```plaintext
    @workspace Which files in this workspace are used to store the enum values passed to the GetDescription method?
    ```

    La respuesta debe indicarle que compruebe la carpeta Enums. Los valores de enumeración se definen en los archivos **LoanExtensionStatus**, **LoanReturnStatus** y **MembershipRenewalStatus**.

1. Agregue los siguientes archivos al contexto de Chat:

    - EnumHelper.cs
    - LoanExtensionStatus.cs
    - LoanReturnStatus.cs
    - MembershipRenewalStatus.cs

    Puede usar una operación de arrastrar y soltar para agregar los archivos desde la vista Explorador de Visual Studio Code a la vista Chat. También puede usar el botón **Agregar contexto** en la vista Chat para agregar archivos y otros recursos.

    > **NOTA**: Agregar archivos al contexto de Chat garantiza que GitHub Copilot los tenga en cuenta al generar una respuesta. La relevancia y la precisión de las respuestas aumentan cuando GitHub Copilot comprende el contexto asociado a los mensajes.

1. Revise y después envíe el mensaje siguiente:

    ```plaintext

    @workspace I need to refactor the `EnumHelper` class and remove any code that uses reflection. Use static dictionaries to supply enum description attributes. Use a separate dictionary for each enum. The dictionaries should use values from the `LoanExtensionStatus.cs`, `LoanReturnStatus.cs`, and `MembershipRenewalStatus.cs` files. Explain how to update the EnumHelper class using dictionaries and show me the updated code.

    ```

    Al escribir cualquier mensaje, la claridad y el contexto son importantes. El uso de participantes de chat, comandos de barra diagonal y variables de chat ayuda a definir el contexto de una manera que GitHub Copilot pueda comprender.

    Al escribir un mensaje que le pida a GitHub Copilot cómo resolver un problema, comience con el problema que intenta resolver. Use oraciones concisas para describir detalles, especificar restricciones e identificar recursos. Por último, asegúrese de indicarle a GitHub Copilot qué incluir en la respuesta.

    En este caso, el mensaje comienza con una descripción del problema u objetivo. Indique a GitHub Copilot que necesita refactorizar la clase **EnumHelper** y quitar cualquier código que use reflexiones. Indique a GitHub Copilot que quiere usar diccionarios para proporcionar atributos de descripción de enumeración. Especifique que quiere un diccionario independiente para cada enumeración e indique a GitHub Copilot que los valores de enumeración deben obtenerse de los archivos que mencione. Para terminar, pídale a GitHub Copilot que explique cómo actualizar la clase **EnumHelper** y pídale un ejemplo de código que contenga el código actualizado.

1. Dedique un minuto a revisar la respuesta proporcionada por GitHub Copilot.

    La respuesta debe ser similar a las siguientes muestras de código y markdown:

    ```markdown

    To refactor the EnumHelper class and remove reflection, you can create static dictionaries for each enum type. These dictionaries will map each enum value to its description. The dictionaries will be initialized with the descriptions defined in the Description attributes of the enums.

    Here's how to update the **EnumHelper** class:

    1. Create a static dictionary for each enum (LoanExtensionStatus, LoanReturnStatus, and MembershipRenewalStatus).
    2. Populate these dictionaries with the enum values as keys and their descriptions as values.
    3. Update the GetDescription method to retrieve the description from the appropriate dictionary based on the enum type.

    Here’s the updated code:

    ```

    ```csharp

    using System.Collections.Generic;
    
    namespace Library.ApplicationCore.Enums;
    
    public static class EnumHelper
    {
        private static readonly Dictionary<LoanExtensionStatus, string> LoanExtensionStatusDescriptions = new()
        {
            { LoanExtensionStatus.Success, "Book loan extension was successful." },
            { LoanExtensionStatus.LoanNotFound, "Loan not found." },
            { LoanExtensionStatus.LoanExpired, "Cannot extend book loan as it already has expired. Return the book instead." },
            { LoanExtensionStatus.MembershipExpired, "Cannot extend book loan due to expired patron's membership." },
            { LoanExtensionStatus.LoanReturned, "Cannot extend book loan as the book is already returned." },
            { LoanExtensionStatus.Error, "Cannot extend book loan due to an error." }
        };
    
        private static readonly Dictionary<LoanReturnStatus, string> LoanReturnStatusDescriptions = new()
        {
            { LoanReturnStatus.Success, "Book was successfully returned." },
            { LoanReturnStatus.LoanNotFound, "Loan not found." },
            { LoanReturnStatus.AlreadyReturned, "Cannot return book as the book is already returned." },
            { LoanReturnStatus.Error, "Cannot return book due to an error." }
        };
    
        private static readonly Dictionary<MembershipRenewalStatus, string> MembershipRenewalStatusDescriptions = new()
        {
            { MembershipRenewalStatus.Success, "Membership renewal was successful." },
            { MembershipRenewalStatus.PatronNotFound, "Patron not found." },
            { MembershipRenewalStatus.TooEarlyToRenew, "It is too early to renew the membership." },
            { MembershipRenewalStatus.LoanNotReturned, "Cannot renew membership due to an outstanding loan." },
            { MembershipRenewalStatus.Error, "Cannot renew membership due to an error." }
        };
    
        public static string GetDescription<TEnum>(TEnum value) where TEnum : Enum
        {
            return value switch
            {
                LoanExtensionStatus loanExtensionStatus => LoanExtensionStatusDescriptions[loanExtensionStatus],
                LoanReturnStatus loanReturnStatus => LoanReturnStatusDescriptions[loanReturnStatus],
                MembershipRenewalStatus membershipRenewalStatus => MembershipRenewalStatusDescriptions[membershipRenewalStatus],
                _ => value.ToString()
            };
        }
    }

    ```

    ```markdown

    Explanation:
    
    1. Static Dictionaries: Each dictionary is specific to an enum type and maps enum values to their descriptions.
    2. Generic Method: The GetDescription method is now generic and uses a switch expression to determine which dictionary to use based on the enum type.
    3. No Reflection: The use of reflection is completely removed, improving performance and type safety.
    
    This approach ensures that the descriptions are statically defined and avoids the runtime overhead of reflection.

    ```

1. En la vista Chat, mantenga el puntero del mouse sobre el ejemplo de código incluido en la respuesta.

1. Observe los tres botones que aparecen en la esquina superior derecha del fragmento de código.

1. Mantenga el puntero sobre cada uno de los botones para ver una información sobre herramientas que describe la acción.

    Los dos primeros botones copian el código en el editor. El tercer botón copia el código en el Portapapeles.

> **NOTA**: Puede usar el modo Preguntar para actualizar la clase **EnumHelper**. Pero el modo Editar refactoriza el código directamente dentro del editor de código y proporciona más opciones para aceptar actualizaciones.

### Refactorización de la clase EnumHelper mediante la vista Chat en modo Editar

El modo Editar de la vista Chat está diseñado para editar código en el área de trabajo. Puede usar el modo Editar para refactorizar el código, agregar comentarios o realizar otros cambios en el código.

1. En la vista Chat, seleccione **Establecer modo** y, después, **Editar**.

    Cuando se le pida que inicie una nueva sesión en el modo Editar, seleccione **Sí**.

    En el modo **Editar**, GitHub Copilot muestra respuestas como sugerencias de actualización de código en el editor de código. El modo Editar se usa generalmente al implementar una nueva característica, corregir un error o refactorizar código.

1. Agregue los siguientes archivos al contexto de Chat:

    - EnumHelper.cs
    - LoanExtensionStatus.cs
    - LoanReturnStatus.cs
    - MembershipRenewalStatus.cs

1. Revise y después envíe el mensaje siguiente:

    ```plaintext

    #codebase I need to refactor the `EnumHelper` class and remove any code that uses reflection. Use static dictionaries to supply enum description attributes. Use a separate dictionary for each enum. The dictionaries should use values from the `LoanExtensionStatus.cs`, `LoanReturnStatus.cs`, and `MembershipRenewalStatus.cs` files.

    ```

    Este mensaje indica a GitHub Copilot que refactorice la clase **EnumHelper** mediante diccionarios en lugar de la reflexión para asignar atributos de descripción de enumeración. Especifica que se debe usar un diccionario independiente para cada enumeración y que los valores de enumeración se deben obtener de archivos específicos.

1. Dedique un minuto a revisar las actualizaciones de código sugeridas.

    Revise las actualizaciones sugeridas para asegurarse de que los valores de enumeración provienen de los archivos **LoanExtensionStatus.cs**, **LoanReturnStatus.cs** y **MembershipRenewalStatus.cs**.

    Puede abrir cada uno de los archivos de enumeración para comprobar que los valores de enumeración de los diccionarios son correctos. Si encuentra discrepancias, haga que GitHub Copilot actualice los diccionarios de cada enumeración individualmente. Por ejemplo, puede usar el mensaje siguiente para la enumeración **LoanExtensionStatus**:

    ```plaintext

    #codebase Use the description values in LoanExtensionStatus.cs to update the LoanExtensionStatus dictionary in the EnumHelper class. Provide the updated code for the LoanExtensionStatus dictionary in the EnumHelper class.

    ```

1. En la vista Chat, para aceptar todas las actualizaciones, seleccione **Mantener**.

    También puede usar la barra de herramientas de ediciones de chat cerca de la parte inferior de la pestaña del editor de código para aceptar o rechazar actualizaciones de código.

1. Dedique un minuto a revisar el método **GetDescription**.

    GitHub Copilot debe haber actualizado el método **GetDescription** para usar la coincidencia de patrones y diccionarios estáticos en lugar de la reflexión. El método actualizado debe ser similar a uno de los ejemplos siguientes:

    ```csharp

    public static string GetDescription(Enum value)
    {
        if (value == null)
            return string.Empty;

        // Use type checks to select the correct dictionary
        if (value is LoanExtensionStatus les && LoanExtensionStatusDescriptions.TryGetValue(les, out var lesDesc))
            return lesDesc;
        if (value is LoanReturnStatus lrs && LoanReturnStatusDescriptions.TryGetValue(lrs, out var lrsDesc))
            return lrsDesc;
        if (value is MembershipRenewalStatus mrs && MembershipRenewalStatusDescriptions.TryGetValue(mrs, out var mrsDesc))
            return mrsDesc;

        return value.ToString();
    }

    ```

    o

    ```csharp

    public static string GetDescription<TEnum>(TEnum value) where TEnum : Enum
    {
        return value switch
        {
            MembershipRenewalStatus status => MembershipRenewalDescriptions.TryGetValue(status, out var description) ? description : status.ToString(),
            LoanReturnStatus status => LoanReturnDescriptions.TryGetValue(status, out var description) ? description : status.ToString(),
            LoanExtensionStatus status => LoanExtensionDescriptions.TryGetValue(status, out var description) ? description : status.ToString(),
            _ => value.ToString()
        };
    }

    ```

    Este código usa la coincidencia de patrones para determinar el tipo de enumeración y recuperar la descripción del diccionario adecuado. La instrucción **switch** comprueba el tipo de **value** de enumeración y devuelve la descripción correspondiente del diccionario. Si el valor de enumeración no se encuentra en el diccionario, el método vuelve a llamar a ToString() en el valor de enumeración, que devuelve el nombre del miembro de enumeración como una cadena.

    Si hace que GitHub Copilot refactorice el método GetDescription para eliminar las expresiones lambda, la lógica subyacente es más fácil de seguir:

    ```csharp

    public static string GetDescription<TEnum>(TEnum value) where TEnum : Enum
    {
        switch (value)
        {
            case MembershipRenewalStatus status:
                string membershipDescription;
                if (MembershipRenewalDescriptions.TryGetValue(status, out membershipDescription))
                {
                    return membershipDescription;
                }
                return status.ToString();

            case LoanReturnStatus status:
                string loanReturnDescription;
                if (LoanReturnDescriptions.TryGetValue(status, out loanReturnDescription))
                {
                    return loanReturnDescription;
                }
                return status.ToString();

            case LoanExtensionStatus status:
                string loanExtensionDescription;
                if (LoanExtensionDescriptions.TryGetValue(status, out loanExtensionDescription))
                {
                    return loanExtensionDescription;
                }
                return status.ToString();

            default:
                return value.ToString();
        }
    }

    ```

1. Compile la solución para asegurarse de que no se hayan producido errores.

    Verá las mismas advertencias que ha visto al principio de este ejercicio, pero no debería haber ningún mensaje de error.

## Refactorización del código mediante chat en línea y la vista Chat en los modos Editar y Agente

LINQ es una característica eficaz de C# que permite consultar colecciones, bases de datos y documentos XML de manera uniforme. LINQ proporciona una manera más concisa y legible de consultar datos en comparación con los bucles foreach tradicionales.

En esta sección del ejercicio se incluyen las siguientes tareas:

- Refactorice la clase JsonData mediante chat en línea.
- Refactorice la clase JsonLoanRepository mediante la vista Chat en modo Editar.
- Refactorice la clase JsonPatronRepository mediante la vista Chat en modo Agente.

### Refactorización de la clase JsonData mediante chat en línea

La clase JsonData incluye los siguientes métodos de acceso a datos: GetPopulatedPatron, GetPopulatedLoan, GetPopulatedBookItem, GetPopulatedBook. Estos métodos usan bucles foreach para recorrer en iteración las colecciones y rellenar objetos. Puede refactorizar estos métodos para usar LINQ para mejorar la legibilidad y el mantenimiento del código.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. En la vista EXPLORADOR DE SOLUCIONES, expanda el proyecto **Library.Infrastructure** y después la carpeta **Data**.

1. Abra el archivo JsonData.cs.

1. Desplácese hacia abajo hasta el método **GetPopulatedPatron**.

    El método **GetPopulatedPatron** está diseñado para crear un objeto **Patron** de biblioteca completamente rellenado. Copia las propiedades básicas de **Patron** y rellena su colección **Loans** con objetos **Loan** detallados.

1. Selecciona el método **GetPopulatedPatron**.

    ```csharp

    public Patron GetPopulatedPatron(Patron p)
    {
        Patron populated = new Patron
        {
            Id = p.Id,
            Name = p.Name,
            ImageName = p.ImageName,
            MembershipStart = p.MembershipStart,
            MembershipEnd = p.MembershipEnd,
            Loans = new List<Loan>()
        };

        foreach (Loan loan in Loans!)
        {
            if (loan.PatronId == p.Id)
            {
                populated.Loans.Add(GetPopulatedLoan(loan));
            }
        }

        return populated;
    }

    ```

1. Abra un chat en línea y escriba un mensaje que refactorice el método mediante LINQ.

    ```plaintext
    #selection refactor selection to `return new Patron` using LINQ
    ```

1. Dedique un minuto a revisar la actualización sugerida.

    La actualización sugerida debe ser similar al código siguiente:

    ```csharp
    public Patron GetPopulatedPatron(Patron p)
    {
        return new Patron
        {
            Id = p.Id,
            Name = p.Name,
            ImageName = p.ImageName,
            MembershipStart = p.MembershipStart,
            MembershipEnd = p.MembershipEnd,
            Loans = Loans!
                .Where(loan => loan.PatronId == p.Id)
                .Select(GetPopulatedLoan)
                .ToList()
        };
    }
    ```

    Observe que se usa una consulta LINQ para reemplazar el bucle foreach.

    El código de LINQ usa el inicializador de objetos para asignar propiedades de objeto al nuevo objeto **Patron**. Esto alivia la necesidad de una instancia **rellenada** independiente del objeto **Patron**. En general, el código actualizado es más corto y legible.

    El código usa el usuario **p** para asignar algunas propiedades básicas al nuevo objeto **Patron**. Después, rellena la colección **Loans** con los préstamos asociados al parámetro de Patron **p** y transforma cada préstamo con el método **GetPopulatedLoan**.

    Puede desglosar la línea de código de LINQ que rellena la colección **Loans**:

    - **Loans!**: La expresión **Loans!** accede a la colección **Loans**. El operador **!** operator es un operador que admite valores null, lo que indica que el desarrollador tiene la seguridad de que **Loans** no es null. Debe asegurarse de que **Loans** se inicialice correctamente antes de llamar al método **GetPopulatedPatron**.

    - **.Where(loan => loan.PatronId == p.Id)**: este código filtra los préstamos para incluir solo los que pertenecen al usuario de entrada **p**.

    - **.Select(GetPopulatedLoan)**: este código transforma cada préstamo filtrado mediante el método **GetPopulatedLoan**.

    - **.ToList()**: convierte el resultado en un elemento **List\<Loan\>**.

1. Para aceptar la actualización sugerida, seleccione **Aceptar**.

    Usará este mismo enfoque para refactorizar otros tres métodos.

1. Refactoriza los métodos **GetPopulatedLoan**, **GetPopulatedBookItem**, y **GetPopulatedBook** con el mismo enfoque.

    Por ejemplo, use las siguientes indicaciones para refactorizar los tres métodos:

    Para el método **GetPopulatedLoan**:

    ```plaintext

    #selection refactor selection to `return new Loan` using LINQ. Use `GetPopulatedBookItem` for the `BookItem` property. Use `Single` for BookItem and Patron properties.

    ```

    Para el método **GetPopulatedBookItem**:

    ```plaintext

    #selection refactor selection to `return new BookItem` using LINQ. Use `GetPopulatedBook` and `Single` for the `BookItem` property.

    ```

    Para el método **GetPopulatedBook**:

    ```plaintext

    #selection refactor selection to `return new Book` using LINQ. Use `Where` and `Select` for `Author` property. Use `First` author.

    ```

1. Después de aceptar las actualizaciones sugeridas, dedique un minuto a revisar los cambios del código.

    El código actualizado debe tener un aspecto similar al siguiente:

    ```csharp
    public Loan GetPopulatedLoan(Loan l)
    {
        return new Loan
        {
            Id = l.Id,
            BookItemId = l.BookItemId,
            PatronId = l.PatronId,
            LoanDate = l.LoanDate,
            DueDate = l.DueDate,
            ReturnDate = l.ReturnDate,
            BookItem = GetPopulatedBookItem(BookItems!.Single(bi => bi.Id == l.BookItemId)),
            Patron = Patrons!.Single(p => p.Id == l.PatronId)
        };
    }

    public BookItem GetPopulatedBookItem(BookItem bi)
    {
        return new BookItem
        {
            Id = bi.Id,
            BookId = bi.BookId,
            AcquisitionDate = bi.AcquisitionDate,
            Condition = bi.Condition,
            Book = GetPopulatedBook(Books!.Single(b => b.Id == bi.BookId))
        };
    }

    public Book GetPopulatedBook(Book b)
    {
        return new Book
        {
            Id = b.Id,
            Title = b.Title,
            AuthorId = b.AuthorId,
            Genre = b.Genre,
            ISBN = b.ISBN,
            ImageName = b.ImageName,
            Author = Authors!.Where(a => a.Id == b.AuthorId).Select(a => new Author {
                Id = a.Id,
                Name = a.Name
            }).First()
        };
    }
    ```

1. Use la acción inteligente **Explicar** para ver una explicación de las consultas LINQ.

    Para abrir la acción inteligente **Explicar**, seleccione el código en el editor, haga clic con el botón derecho en el código seleccionado, seleccione Copilot y, después, **Explicar**. La acción inteligente **Explicar**proporciona una explicación detallada del código seleccionado. En este caso, las consultas de LINQ que se usan en el código.

    Por ejemplo, puede usar la acción inteligente **Explicar** en el método **GetPopulatedBook** para ver una explicación de la consulta LINQ que se usa para rellenar la propiedad **Author** del objeto **Book**.

    ```csharp
    Author = Authors!.Where(a => a.Id == b.AuthorId).Select(a => new Author {
        Id = a.Id,
        Name = a.Name
    }).First()
    ```

    La acción inteligente **Explicar** proporciona una explicación detallada de la consulta LINQ que se usa para rellenar la propiedad **Author** del objeto **Book**.

    Por ejemplo, la explicación podría tener este aspecto:

    ```plaintext

    The active selection is a C# code snippet that assigns a value to the Author property. This value is derived from a collection of Author objects named Authors. The code uses LINQ to filter and transform the data within this collection.
    
    First, the Authors! expression uses the null-forgiving operator (!) to indicate that Authors is not null, even if the compiler might think otherwise. This is a way to suppress nullable warnings. The Where method is then called on the Authors collection to filter the elements. The lambda expression a => a.Id == b.AuthorId is used to find all Author objects where the Id matches the AuthorId property of another object b.
    
    After filtering, the Select method is used to project each filtered Author object into a new Author object. This is done by creating a new instance of the Author class and copying the Id and Name properties from the original Author object.
    
    Finally, the First method is called to retrieve the first element from the resulting sequence. This means that the Author property will be assigned the first Author object that matches the filter criteria and has been projected into a new Author instance.
    
    This approach ensures that the Author property is set to a new Author object with the same Id and Name as the first matching Author in the Authors collection.

    ```

1. Compile la solución para asegurarse de que no hay errores.

### Refactorización de la clase JsonLoanRepository mediante la vista Chat en modo Editar

La clase JsonLoanRepository incluye los métodos de acceso a datos **GetLoan** y **UpdateLoan**. Refactorizará estos dos métodos, reemplazando los bucles foreach por LINQ para mejorar la legibilidad y el mantenimiento del código.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Abre el archivo **JsonLoanRepository.cs**.

1. Selecciona el método **GetLoan**.

    El método **GetLoan** está diseñado para recuperar un préstamo por su id.

    ```csharp
    public async Task<Loan?> GetLoan(int id)
    {
        await _jsonData.EnsureDataLoaded();

        foreach (Loan loan in _jsonData.Loans!)
        {
            if (loan.Id == id)
            {
                Loan populated = _jsonData.GetPopulatedLoan(loan);
                return populated;
            }
        }

        return null;
    }
    ```

1. Asegúrese de que la vista Chat esté abierta en modo **Editar**.

    Si la vista Chat no está abierta, seleccione **Alternar chat** y establezca el modo en **Editar**.

1. Escriba un mensaje que refactorice el método mediante LINQ.

    Por ejemplo, escriba el siguiente símbolo del sistema:

    ```plaintext
    refactor the foreach using LINQ. Use Where, Select, and GetPopulatedLoan return the first matching loan.
    ```

1. Dedique un minuto a revisar la actualización sugerida.

    La actualización sugerida debe ser similar al código siguiente:

    ```csharp
    public async Task<Loan?> GetLoan(int id)
    {
        await _jsonData.EnsureDataLoaded();

        return _jsonData.Loans!
            .Where(l => l.Id == id)
            .Select(l => _jsonData.GetPopulatedLoan(l))
            .FirstOrDefault();

    }
    ```

    El código actualizado usa LINQ para filtrar la colección de préstamos para incluir solo el préstamo con el identificador especificado. Observe que **loan** se debe declarar como que admite un valor NULL (**Loan? loan**). Después, transforma el préstamo con el método **GetPopulatedLoan** y devuelve el primer resultado. Si no se encuentra ningún préstamo coincidente, **FirstOrDefault** devuelve **null**. Después, el método devuelve este objeto de préstamo, que puede ser null si no existe ningún préstamo con el valor **id** especificado. Este enfoque garantiza que el préstamo devuelto se rellene completamente con todos los datos relacionados necesarios, lo que proporciona una visión completa del registro del préstamo.

    GitHub Copilot también podría sugerir el código siguiente, que es funcionalmente equivalente:

    ```csharp
    public async Task<Loan?> GetLoan(int id)
    {
        await _jsonData.EnsureDataLoaded();

        Loan? loan = _jsonData.Loans!
            .Where(l => l.Id == id)
            .Select(l => _jsonData.GetPopulatedLoan(l))
            .FirstOrDefault();

        return loan;
    }
    ```

1. Para aceptar el método GetLoan actualizado, seleccione **Mantener**.

1. Selecciona el método **UpdateLoan**.

    ```csharp
    public async Task UpdateLoan(Loan loan)
    {
        Loan? existingLoan = null;
        foreach (Loan l in _jsonData.Loans!)
        {
            if (l.Id == loan.Id)
            {
                existingLoan = l;
                break;
            }
        }

        if (existingLoan != null)
        {
            existingLoan.BookItemId = loan.BookItemId;
            existingLoan.PatronId = loan.PatronId;
            existingLoan.LoanDate = loan.LoanDate;
            existingLoan.DueDate = loan.DueDate;
            existingLoan.ReturnDate = loan.ReturnDate;

            await _jsonData.SaveLoans(_jsonData.Loans!);

            await _jsonData.LoadData();
        }
    }
    ```

1. Escriba un mensaje que refactorice el método mediante LINQ.

    Por ejemplo, escriba el siguiente símbolo del sistema:

    ```plaintext

    refactor selection using LINQ. find existing loan in `_jsonData.Loans!. replace existing loan.

    ```

1. Dedique un minuto a revisar la actualización sugerida.

    La actualización sugerida debe ser similar a uno de los ejemplos siguientes:

    ```csharp

    public async Task UpdateLoan(Loan loan)
    {
        var loans = _jsonData.Loans!;
        var index = loans.FindIndex(l => l.Id == loan.Id);

        if (index >= 0)
        {
            loans[index] = loan;
            await _jsonData.SaveLoans(loans);
            await _jsonData.LoadData();
        }
    }

    ```

    o

    ```csharp

    public async Task UpdateLoan(Loan loan)
    {
        Loan? existingLoan = _jsonData.Loans!.FirstOrDefault(l => l.Id == loan.Id);

        if (existingLoan != null)
        {
            existingLoan.BookItemId = loan.BookItemId;
            existingLoan.PatronId = loan.PatronId;
            existingLoan.LoanDate = loan.LoanDate;
            existingLoan.DueDate = loan.DueDate;
            existingLoan.ReturnDate = loan.ReturnDate;

            await _jsonData.SaveLoans(_jsonData.Loans!);

            await _jsonData.LoadData();
        }
    }

    ```

    El código actualizado usa LINQ para encontrar el préstamo existente en la colección de préstamos. A continuación, actualiza el préstamo existente con los nuevos datos del préstamo. A continuación, el método guarda la colección de préstamos actualizados y vuelve a cargar los datos. Este enfoque garantiza que los datos del préstamo se actualicen correctamente y que los cambios se conserven en el almacén de datos.

    También puede agregar el código para asegurarse de que los datos se cargan antes de ejecutar el método:

    ```csharp

    public async Task UpdateLoan(Loan loan)
    {
        await _jsonData.EnsureDataLoaded();

        Loan? existingLoan = _jsonData.Loans!.FirstOrDefault(l => l.Id == loan.Id);

        if (existingLoan != null)
        {
            existingLoan.BookItemId = loan.BookItemId;
            existingLoan.PatronId = loan.PatronId;
            existingLoan.LoanDate = loan.LoanDate;
            existingLoan.DueDate = loan.DueDate;
            existingLoan.ReturnDate = loan.ReturnDate;

            await _jsonData.SaveLoans(_jsonData.Loans!);

            await _jsonData.LoadData();
        }
    }

    ```

1. Para aceptar el método UpdateLoan actualizado, seleccione **Mantener**.

1. Compile la solución para asegurarse de que no se hayan producido errores.

    Verá advertencias. Puede ignorarlos por ahora.

### Refactorización de la clase JsonPatronRepository mediante la vista Chat en modo Agente

La clase **JsonPatronRepository** incluye los tres métodos siguientes:

- SearchPatrons: el método SearchPatrons está diseñado para buscar usuarios por nombre. Este método devuelve una lista ordenada de usuarios.
- GetPatron: el método GetPatron se usa para recuperar un usuario por identificador. Este método devuelve un objeto de usuario rellenado.
- UpdatePatron: el método UpdatePatron se usa para actualizar la información de un usuario. Este método actualiza el usuario existente con los nuevos datos y guarda la colección de usuarios actualizada.

En cada uno de los tres métodos se usa un bucle foreach para iterar los usuarios y buscar coincidencias en función de la entrada o el identificador de búsqueda.

Usará la vista Chat en modo Agente para refactorizar los métodos y reemplazar bucles foreach por consultas LINQ, como ha hecho para las clases **JsonData** y **JsonLoanRepository**.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Abre el archivo **JsonPatronRepository.cs**.

    La clase **JsonPatronRepository** está diseñada para administrar los clientes de la biblioteca.

1. Dedique un minuto a revisar tres métodos incluidos en la clase **JsonPatronRepository**.

    El método **SearchPatrons** está diseñado para buscar usuarios por nombre.

    ```csharp

    public async Task<List<Patron>> SearchPatrons(string searchInput)
    {
        await _jsonData.EnsureDataLoaded();

        List<Patron> searchResults = new List<Patron>();
        foreach (Patron patron in _jsonData.Patrons)
        {
            if (patron.Name.Contains(searchInput))
            {
                searchResults.Add(patron);
            }
        }
        searchResults.Sort((p1, p2) => String.Compare(p1.Name, p2.Name));

        searchResults = _jsonData.GetPopulatedPatrons(searchResults);

        return searchResults;
    }

    ```

    Observe que el método **SearchPatrons** usa un bucle foreach para iterar por los usuarios y buscar coincidencias basadas en la cadena **searchInput**. Después, el método ordena los resultados por nombre y devuelve una lista de usuarios rellenados.

    El método **GetPatron** está diseñado para devolver el usuario que coincide con el valor **id** especificado.

    ```csharp

    public async Task<Patron?> GetPatron(int id)
    {
        await _jsonData.EnsureDataLoaded();

        foreach (Patron patron in _jsonData.Patrons!)
        {
            if (patron.Id == id)
            {
                Patron populated = _jsonData.GetPopulatedPatron(patron);
                return populated;
            }
        }
        return null;
    }

    ```

    Observe que el **método GetPatron** usa un bucle foreach para iterar por los usuarios y buscar una coincidencia basada en el parámetro **id**. Después, el método devuelve el objeto de usuario rellenado.

    El método **UpdatePatron** está diseñado para actualizar el usuario con el valor **id** especificado.

    ```csharp

    public async Task UpdatePatron(Patron patron)
    {
        await _jsonData.EnsureDataLoaded();
        var patrons = _jsonData.Patrons!;
        Patron existingPatron = null;
        foreach (var p in patrons)
        {
            if (p.Id == patron.Id)
            {
                existingPatron = p;
                break;
            }
        }
        if (existingPatron != null)
        {
            existingPatron.Name = patron.Name;
            existingPatron.ImageName = patron.ImageName;
            existingPatron.MembershipStart = patron.MembershipStart;
            existingPatron.MembershipEnd = patron.MembershipEnd;
            existingPatron.Loans = patron.Loans;
            await _jsonData.SavePatrons(patrons);
            await _jsonData.LoadData();
        }
    }

    ```

    Observe que el método **UpdatePatron** usa un bucle foreach para iterar por los usuarios y buscar una coincidencia basada en el parámetro **id**. Después, el método actualiza el usuario existente con los nuevos datos y guarda la colección de usuarios actualizada.

1. En la vista Chat, cambie el modo a **Agente**

    El modo Agente está diseñado para ejecutar GitHub Copilot como agente. Puede usar lenguaje natural para especificar una tarea general. El agente evaluará la tarea asignada, planeará el trabajo necesario y aplicará los cambios en el código base.

    El modo Agente usa una combinación de la edición de código y la invocación de herramientas para realizar la tarea especificada. A medida que procesa la solicitud, supervisa el resultado de las ediciones y las herramientas, e itera para resolver los problemas que surjan. Si el agente no puede resolver un problema, le pedirá que intervenga. Por ejemplo, si el agente usa varias iteraciones que funcionan para resolver el mismo problema, pausará el proceso y le pedirá que proporcione contexto adicional para aclarar la solicitud o cancelar el proceso.

    > **IMPORTANTE**: Cuando se usa la vista Chat en modo Agente, GitHub Copilot puede realizar varias solicitudes premium para completar una sola tarea. Las solicitudes premium se pueden usar en mensajes iniciados por el usuario y acciones de seguimiento que Copilot realiza en su nombre. El número total de solicitudes premium usadas se basa en la complejidad de la tarea, el número de pasos implicados y el modelo seleccionado.

1. Dedique un minuto a tener en cuenta la tarea que necesita asignar al agente.

    La tarea consiste en refactorizar la clase **JsonPatronRepository**. El objetivo es reemplazar los bucles foreach por consultas LINQ que producen el mismo resultado que el código foreach original.

    Puede usar su experiencia con las clases **JsonData** y **JsonLoanRepository** a fin de escribir la tarea para el agente. Las consultas LINQ deben usar **Where**, **Select** y **FirstOrDefault** para buscar usuarios coincidentes. Las consultas LINQ también deben usar **OrderBy** para conservar la ordenación en el código foreach original.

1. Para asignar la tarea del agente, escriba el mensaje siguiente:

    ```plaintext

    Review the LINQ code used in the JsonData and JsonLoanRepository classes. Notice how Where, Select, and FirstOrDefault are used. Refactor the methods in the JsonPatronRepository class, replacing foreach loops with LINQ queries that produce the same result as the original foreach code. Use OrderBy to preserve sorting in original foreach code. Use ! to suppress nullability warnings when accessing collections.

    ```

    Este mensaje indica al agente que refactorice la clase **JsonPatronRepository**. Especifica que los bucles foreach se deben reemplazar por consultas LINQ que producen el mismo resultado que el código foreach original. También especifica que se debe usar **OrderBy** para conservar la ordenación en el código foreach original y que **!** se debe usar para suprimir las advertencias de nulabilidad al acceder a las colecciones.

1. Supervise el progreso del agente a medida que refactoriza el código.

    Observe que el agente completa la tarea en varias iteraciones. Cada paso de edición de código va seguido de un paso de revisión que comprueba si hay problemas. Si el agente encuentra un problema, refactorizará el código para resolverlo. Si el agente no puede resolver un problema, le pedirá que intervenga.

1. Una vez que finalice el agente, dedique un minuto a revisar las actualizaciones sugeridas.

    La actualización sugerida debe ser similar al código siguiente:

    ```csharp

    public async Task<List<Patron>> SearchPatrons(string searchInput)
    {
        await _jsonData.EnsureDataLoaded();

        var searchResults = _jsonData.Patrons!
            .Where(patron => patron.Name.Contains(searchInput))
            .OrderBy(patron => patron.Name)
            .ToList();

        return _jsonData.GetPopulatedPatrons(searchResults);
    }

    public async Task<Patron?> GetPatron(int id)
    {
        await _jsonData.EnsureDataLoaded();

        return _jsonData.Patrons!
            .Where(patron => patron.Id == id)
            .Select(patron => _jsonData.GetPopulatedPatron(patron))
            .FirstOrDefault();
    }

    public async Task UpdatePatron(Patron patron)
    {
        await _jsonData.EnsureDataLoaded();

        var existingPatron = _jsonData.Patrons!.FirstOrDefault(p => p.Id == patron.Id);
        if (existingPatron != null)
        {
            existingPatron.Name = patron.Name;
            existingPatron.ImageName = patron.ImageName;
            existingPatron.MembershipStart = patron.MembershipStart;
            existingPatron.MembershipEnd = patron.MembershipEnd;
            existingPatron.Loans = patron.Loans;

            if (_jsonData.Patrons != null)
            {
                await _jsonData.SavePatrons(_jsonData.Patrons);
                await _jsonData.LoadData();
            }
        }
    }

    ```

1. Para aceptar todas las actualizaciones, seleccione **Mantener**.

### Compilación y ejecución de la aplicación

Ahora que ha refactorizado el código, es el momento de compilar y ejecutar la aplicación para asegurarse de que todo funciona correctamente. También probará la aplicación para asegurarse de que el código refactorizado funciona según lo previsto.

1. Para limpiar la solución, haz clic con el botón derecho en **AccelerateAppDevGitHubCopilot** y después selecciona **Limpiar**.

    Esta acción quita los artefactos de compilación de la compilación anterior. La limpieza de la solución restablecerá eficazmente los archivos de datos JSON a sus valores originales (en el directorio de salida).

1. Asegúrese de que la solución se compila correctamente.

    Por ejemplo, en la vista EXPLORADOR DE SOLUCIONES, haga clic con el botón derecho en **AccelerateDevGHCopilot**y, después, seleccione **Compilar**.

    Verá varias Advertencias, pero no debería haber ningún Errores.

1. Para ejecutar la aplicación, haga clic con el botón derecho en **Library.Console**, seleccione **Depurar**y, a continuación, seleccione **Iniciar nueva instancia**.

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

En este ejercicio, ha aprendido a refactorizar código mediante GitHub Copilot. Ha usado la vista Chat en el modo Editar para refactorizar la clase **EnumHelper** y reemplazar la reflexión por diccionarios estáticos. También ha usado el chat en línea y el modo Editar para refactorizar las clases **JsonData** y **JsonLoanRepository**, y reemplazar los bucles foreach por consultas LINQ. Por último, ha usado el modo Agente para refactorizar la clase **JsonPatronRepository** y reemplazar los bucles foreach por consultas LINQ.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Si ha realizado algún cambio, reviértalos ahora.
