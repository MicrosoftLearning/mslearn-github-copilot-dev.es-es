---
lab:
  title: "Ejercicio: Introducción a la codificación de ambiente mediante el agente GitHub\_Copilot"
  description: "Aprenda a crear una aplicación prototipo mediante un proceso de codificación de ambiente y el agente GitHub\_Copilot."
---

# Introducción a la codificación de ambiente mediante el agente GitHub Copilot

La codificación de ambiente es un enfoque de programación que usa herramientas de inteligencia artificial, como el agente GitHub Copilot, para generar software. En lugar de escribir código manualmente, un usuario proporciona una descripción del lenguaje natural de su aplicación prevista y la inteligencia artificial genera el código correspondiente. Esto cambia el rol del programador, que pasa de la codificación tradicional a guiar, probar y perfeccionar los resultados generados por la IA.

En este ejercicio, usará un proceso de codificación de ambiente y el agente GitHub Copilot para crear una versión prototipo de una aplicación de compras en línea. La aplicación prototipo incluye las siguientes páginas: productos, detalles del producto, carro de la compra y finalización de la compra. La aplicación incluye navegación básica entre páginas y un conjunto de datos limitado que ayuda a demostrar las características de la aplicación. El prototipo no incluye ninguna funcionalidad de back-end, como la autenticación de usuario, el procesamiento de pagos o la integración de bases de datos.

Este ejercicio debería tardar en completarse **30** minutos aproximadamente.

> **IMPORTANTE**: Para completar este ejercicio, debe proporcionar su propia cuenta de GitHub y suscripción de GitHub Copilot. Si no tiene una cuenta de GitHub, puede <a href="https://github.com/" target="_blank">registrarse</a> para obtener una cuenta individual gratuita y usar un plan gratuito de GitHub Copilot para completar el ejercicio. Si tiene acceso a una suscripción de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise desde el entorno de laboratorio, puede usar la suscripción de GitHub Copilot existente para completar este ejercicio.

## Antes de comenzar

El entorno de laboratorio debe incluir lo siguiente:

- Visual Studio Code.
- Una cuenta de GitHub con acciones de GitHub Copilot habilitadas.

Si usa un equipo local como entorno de laboratorio para este ejercicio:

- Puede descargar el archivo del instalador de Visual Studio Code desde la siguiente dirección URL: <a href="https://code.visualstudio.com/download" target="_blank">Descargar Visual Studio Code</a>.

- Para obtener ayuda sobre cómo habilitar la suscripción de GitHub Copilot en Visual Studio Code, abra el siguiente vínculo en un explorador: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

Si usa un entorno de laboratorio hospedado que admite este ejercicio:

- Para obtener ayuda con la habilitación de la suscripción de GitHub Copilot en Visual Studio Code, abra un explorador y pegue la siguiente dirección URL en la barra de navegación del sitio: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Habilitación de GitHub Copilot en Visual Studio Code</a>.

## Escenario del ejercicio

Eres un empresario que quiere usar un proceso de codificación de ambiente para crear una aplicación de compras prototipo. El prototipo inicial debe demostrar las funcionalidades básicas que un usuario espera de una aplicación de compras en línea y características específicas que ha previsto.

Identifique las siguientes especificaciones base para comenzar el proceso de desarrollo:

1. Use HTML, CSS y JavaScript para crear una aplicación web del lado cliente.
2. Incluya las siguientes páginas web: Productos, Detalles del producto, Carro de la compra y Finalización de la compra.
3. Habilite la navegación entre páginas.

Este ejercicio incluye las siguientes tareas:

1. **Definición de los requisitos de producto**: Use GitHub Copilot para ayudar a realizar la transición de las especificaciones base a requisitos de producto más detallados.

1. **Creación de una aplicación de prototipo inicial**: Use el agente GitHub Copilot y los requisitos del producto para crear una aplicación de prototipo inicial.

1. **Refinar la aplicación de prototipo**: Use el agente GitHub Copilot para completar una serie de actualizaciones iterativas que refinan la experiencia del usuario y garantizan que la aplicación cumple los requisitos previstos.

> **NOTA**: Una aplicación prototipo es un modelo interactivo temprano de una aplicación que muestra su diseño visual y la experiencia del usuario. En este ejercicio, la aplicación prototipo debe implementar características básicas y satisfacer un pequeño número de casos de uso de alto nivel.

## Definición de los requisitos de producto:

Para que un agente de IA desarrolle la aplicación prevista, debe comprender los requisitos del producto y la experiencia de usuario prevista. Puede comunicar sus intenciones al agente GitHub Copilot mediante cualquiera de los siguientes procesos:

- **Código primero e iteración para definir los requisitos**: Este enfoque comienza con especificaciones base mínimas y salta directamente a la codificación. A medida que avanza el desarrollo, la aplicación evoluciona orgánicamente a través de ciclos iterativos, dando forma gradual a las características y la experiencia del usuario del producto. Este enfoque corre el riesgo de desviarse de la visión original, para bien o para mal, a medida que explora las características implementadas por la inteligencia artificial. Un proceso dirigido por inteligencia artificial puede tardar mucho tiempo y puede no producir los resultados deseados, especialmente cuando las especificaciones iniciales son vagas o abiertas.

- **Explorar los requisitos antes de codificar**: Este enfoque enfatiza la claridad desde el principio. Colabore con la inteligencia artificial para redactar un documento de requisitos de producto (PRD) antes de escribir cualquier código. El PRD describe el propósito de la aplicación, los usuarios de destino, las características clave y las restricciones técnicas. Al establecer una visión clara por adelantado, proporciona a la inteligencia artificial una base sólida para generar código que se alinee con sus objetivos, lo que reduce la ambigüedad y mejora las posibilidades de crear la aplicación que realmente ha previsto.

En esta tarea, usará GitHub Copilot para evaluar las especificaciones base y desarrollar requisitos de producto para la aplicación prototipo.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. Abra Visual Studio Code.

1. En el menú Archivo, seleccione **Agregar carpeta al área de trabajo**.

1. En el cuadro de diálogo **Agregar carpeta al área de trabajo**, navegue hasta una ubicación de carpeta fácil de encontrar, cree una nueva carpeta con el nombre **VibeCoding-PrototypeApp** y, a continuación, seleccione **Agregar**.

    La ubicación de la carpeta debe estar fuera de cualquier repositorio de Git existente y debe ser fácil de encontrar. Por ejemplo, si usa un equipo Windows, puede crear una carpeta denominada **VibeCoding-PrototypeApp** en el **escritorio** o en el directorio **Documentos**.

    Después de completar este ejercicio de laboratorio, puede archivar o eliminar el proyecto de código.

1. Abra la vista Chat de GitHub Copilot.

    La vista Chat se puede abrir seleccionando el icono de GitHub Copilot situado cerca del centro superior de la ventana de Visual Studio Code, justo a la derecha del cuadro de texto de búsqueda.

1. Asegúrese de que el modo de chat esté establecido en **Preguntar** y que esté seleccionado el modelo **GPT-4.1**.

    Los menús desplegables *Establecer modo* y *Elegir modelo* se encuentran en la esquina inferior izquierda de la vista Chat.

    **Modos de GitHub Copilot**: Aunque sus funcionalidades se superponen, cada uno de los modos de chat (Preguntar, Editar y Agente) está optimizado para un propósito específico:

    - **Pregunta**: Use este modo para hacer preguntas de GitHub Copilot sobre el código base. Puede usar modo Pregunta para explicar código, sugerir revisiones o correcciones, o proporcionar información relacionada con el código base.
    - **Editar**: Use este modo para editar archivos de código específicos en el área de trabajo. Puede usar el modo Editar para refactorizar el código, agregar comentarios, implementar pruebas o agregar nuevas características a las aplicaciones.
    - **Agente**: Use este modo para ejecutar GitHub Copilot como agente. Puede usar el modo agente para realizar tareas de codificación de forma autónoma.

    **Modelos admitidos**: GitHub Copilot admite varios modelos, cada uno con diferentes puntos fuertes. Algunos modelos priorizan la velocidad y la rentabilidad, mientras que otros están optimizados para la precisión, el razonamiento o trabajo con entradas bidireccionales (como imágenes y código). El plan gratuito de GitHub Copilot admite actualmente GPT-4.1, GPT-4o, o3-mini, Claude Sonnet 3.5 y Gemini 2.0 Flash. El modelo GPT-4.1 es una buena opción para este ejercicio porque genera finalizaciones de código rápidas, precisas y explicaciones, admite la entrada visual y controla tareas complejas de forma eficaz.

    > **NOTA**: Elegir un modelo diferente afectará a las respuestas que recibe de GitHub Copilot. Se recomienda el modelo GPT-4.1 para este ejercicio, pero puede repetir el ejercicio con otros modelos si desea ver cómo responden a sus mensajes.

1. En la vista Chat, escriba el siguiente símbolo del sistema:

    ```plaintext
    I want to create a product requirements document (PRD) for an app that I'll develop using a vibe coding process. I want the PRD to include information about the app's purpose, target audience, features, and technical requirements. I've defined the following high-level parameters for my app: 1 - Use HTML, CSS, and JavaScript to create a client-side web app. 2 - Include the following web pages: Products, ProductDetails, ShoppingCart, and Checkout. 3 - Enable navigation between pages. I want the prototype app to implement basic features and satisfy a small number of high-level use cases. The prototype should implement the following: basic use case functionality, simple navigation, a sample dataset, and basic styling. I'll be adding the PRD to the chat context, then asking GitHub Copilot Agent to create the prototype app. What sections should I include in the PRD to enable GitHub Copilot Agent to create my envisioned prototype?
    ```

1. Revise la respuesta generada por GitHub Copilot.

    Por ejemplo, el recurso  podría simplificarse como el ejemplo siguiente:

    ```md
    To enable GitHub Copilot Agent to create your envisioned prototype app, your Product Requirements Document (PRD) should include the following sections:
    
    1. App Overview / Purpose  
       - Briefly describe what the app does and its main goal.
    
    2. Target Audience  
       - Define who will use the app (e.g., general consumers, online shoppers, etc.).
    
    3. Core Features  
       - List and describe the main features (e.g., view products, view product details, add to cart, checkout).
    
    4. Page Descriptions  
       - Detail each required page (Products, ProductDetails, ShoppingCart, Checkout) and what should be displayed or possible on each.
    
    5. Navigation  
       - Explain how users move between pages (e.g., navigation bar, links, buttons).
    
    6. Sample Data  
       - Describe the sample dataset (e.g., a few example products with name, price, description, image).
    
    7. Technical Requirements  
       - Specify technologies to use (HTML, CSS, JavaScript, client-side only, no backend).
       - Mention any libraries or frameworks (if any) or state "vanilla JS".
    
    8. Styling  
       - Indicate the level of styling (e.g., basic, clean, minimal, responsive).
    
    9. Use Cases / User Flows  
       - List a few high-level use cases (e.g., browse products, view details, add to cart, proceed to checkout).
    
    10. Out of Scope  
        - Clarify what is not required (e.g., user authentication, payment processing, backend integration).
    
    Including these sections will give clear, actionable guidance for building your prototype app.
    ```

    > **NOTA**: No se preocupe si la respuesta incluye títulos de sección diferentes o si las secciones aparecen en un orden diferente. Las respuestas que generan las herramientas de IA suelen ser ligeramente diferentes de una sesión de chat a otra. El modelo de IA seleccionado, el historial de chat y el contexto de la sesión de chat también pueden afectar a las respuestas.

1. Dedique unos minutos a tener en cuenta la información necesaria para completar cada sección del PRD.

    Un PRD bien definido ayuda a garantizar que el agente GitHub Copilot tenga una comprensión clara de su visión para la aplicación. El PRD debe proporcionar detalles suficientes para permitir que el agente cree una aplicación prototipo que cumpla sus requisitos y la experiencia de usuario prevista. El PRD debe basarse en las especificaciones base enumeradas anteriormente en el ejercicio.

    Si no está seguro de qué información incluir en una sección específica, puede pedir al agente GitHub Copilot que le ayude a generar el contenido de esa sección. Por ejemplo, puede pedir a GitHub Copilot ideas sobre qué incluir en las secciones "Características principales" o "Casos de uso".

    > **Sugerencia**: Puede proporcionar texto en lenguaje natural que describa los requisitos de la aplicación y que tenga el formato de GitHub Copilot como PRD. También puede usar GitHub Copilot para ayudarle a revisar y actualizar el PRD y asegurarse de que proporciona el nivel de detalle necesario para que el agente GitHub Copilot cree el prototipo.

1. En la vista Chat, escriba el siguiente símbolo del sistema:

    ```plaintext
    The PRD sections that you suggested look good. Here's some information that should help you construct the PRD:

    My prototype app targets online shoppers interested in ordering my products. The prototype should include the following:

    - A dynamic user interface that scales automatically to appear correctly on large or small screens (desktop and phone devices).
    - A simple dataset that defines 10 fruit products. The dataset should include: product name, description, price per unit (where unit could be the number of items, ounces, pounds, etc.). If possible, I want to include a simple image (an emoji) that represents the product.
    - A navigation menu on the left side of the screen that allows users to navigate between the Products, ProductDetails, ShoppingCart, and Checkout pages.
    - Basic styling that makes the user interface visually appealing, but it doesn't need to be fully responsive or polished.

    The prototype app won't include any backend functionality, such as user authentication, payment processing, or database integration. It will be a static prototype that demonstrates the basic concepts.

    Here's a description of the user interface:

    - The Products page should display a list of products with basic information such as product name, price per unit, and an image (an emoji). The Products page should also provide a way to select a desired quantity of a product and an option to add selected items to the shopping cart.
    - The ProductDetails page should display detailed information about a product when the product is selected from the Products page. The ProductDetails page should display the product name, a description of the product, the price per unit, and an image (an emoji) representing the product. The ProductDetails page should also provide a way to navigate back to the Products page.
    - The ShoppingCart page should display the list of products added to the cart. The list should include the product name, quantity, and total price for that product. The ShoppingCart page should also provide a way to update the quantity of each product that's in the cart, and an option to remove products from the cart.
    - The Checkout page should display a summary of the products being purchased, including product name, quantity, and price. The total price should be clearly displayed along with the option to "Process Order".
    - The left-side navigation menu should provide basic navigation between pages. The navigation bar should collapse down to display a one or two letter abbreviation when the display width drops below 300 pixels. The navigation bar should allow users to navigate between the app pages.
    ```

    GitHub Copilot debe generar una respuesta que incluya un PRD sugerido en función de la información proporcionada. La respuesta debe incluir las secciones que ha revisado anteriormente y debe incluir contenido para cada sección en función de la información proporcionada.

1. En la vista Chat, seleccione el modo **Agente**.

    El menú desplegable Establecer modo se encuentra en la esquina inferior izquierda de la vista Chat.

1. En la vista Chat, escriba el siguiente símbolo del sistema:

    ```md
    Create a markdown file named VibeCodingPRD.md using your suggested sections and the inputs that I've provided.
    ```

1. En la vista Chat, para guardar el archivo de VibeCodingPRD.md sugerido, seleccione **Mantener**.

1. Dedique unos minutos a revisar el archivo PRD.

    El archivo PRD sugerido debe ser suficiente para este ejercicio. Sin embargo, si ve lagunas o discrepancias, o si desea agregar más información, puede editar el archivo directamente en Visual Studio Code. También puede pedir a GitHub Copilot que le ayude a refinar el PRD mediante la generación de información adicional o la implementación de aclaraciones.

1. Abra la vista Explorer de Visual Studio Code.

1. En la vista Chat, escriba el siguiente símbolo del sistema:

    ```md
    Can you create low-fidelity wireframe diagrams (or text-based layouts) that represent the web pages and navigation bar (expanded and collapsed) for my prototype app? Use the PRD that I've provided as a reference.
    ```

    El agente GitHub Copilot debe generar diseños basados en texto de baja fidelidad que representan la interfaz de usuario de la aplicación prototipo. Estos "diagramas reticulares" deben ayudar a definir la interfaz de usuario y a cómo interactuarán los usuarios con la aplicación.

    Por ejemplo, la respuesta puede tener un aspecto similar al siguiente:

    ```md
    Certainly! Here are text-based, low-fidelity wireframe layouts for each main page of your prototype app, based on your PRD:

    ---

    ### 1. Products Page
    

    +------------------------------------------------------+
    | [Nav] Products | ProductDetails | Cart | Checkout    |
    +----------------+-------------------------------------+
    | 🍎 Apple         $1.00/each   [Qty: - 1 +] [Add]     |
    | 🍌 Banana        $0.50/each   [Qty: - 1 +] [Add]     |
    | 🍊 Orange        $0.80/each   [Qty: - 1 +] [Add]     |
    | ... (other fruits)                                  |
    +------------------------------------------------------+
    
    ---
    
    ### 2. ProductDetails Page
    
    +------------------------------------------------------+
    | [Nav] Products | ProductDetails | Cart | Checkout    |
    +----------------+-------------------------------------+
    | 🍎 Apple                                         |
    | Fresh, crisp apples                              |
    | Price: $1.00/each                               |
    | [Qty: - 1 +] [Add to Cart]                      |
    | [Back to Products]                              |
    +------------------------------------------------------+
    
    ---
    
    ### 3. ShoppingCart Page
    
    +------------------------------------------------------+
    | [Nav] Products | ProductDetails | Cart | Checkout    |
    +----------------+-------------------------------------+
    | Cart Items:                                       |
    | 🍎 Apple   Qty: [ - 2 + ]  $2.00   [Remove]        |
    | 🍌 Banana  Qty: [ - 1 + ]  $0.50   [Remove]        |
    | -------------------------------------------------- |
    | [Update Cart]                                     |
    | [Proceed to Checkout]                             |
    +------------------------------------------------------+
    
    ---
    
    ### 4. Checkout Page
    
    +------------------------------------------------------+
    | [Nav] Products | ProductDetails | Cart | Checkout    |
    +----------------+-------------------------------------+
    | Order Summary:                                     |
    | 🍎 Apple   x2   $2.00                              |
    | 🍌 Banana  x1   $0.50                              |
    | -------------------------------------------------- |
    | Total: $2.50                                      |
    | [Process Order]                                   |
    +------------------------------------------------------+
    
    ---
    
    ### 5. Navigation Bar (Left Side, Collapsible)
    
    +-------------------+      +-----+
    | Products          |      | P   |
    | ProductDetails    |      | D   |
    | Cart              |      | C   |
    | Checkout          |      | CO  |
    +-------------------+      +-----+
    (Full width)             (Collapsed <300px)
    
    ---
    
    These wireframes provide a clear, simple structure for each page and the navigation menu, matching your requirements. If you want these added to your PRD or as a separate markdown file, let me know!
    ```

    > **NOTA**: Hay muchas otras maneras de crear diagramas de tramas de alambre. Para obtener un enfoque basado en inteligencia artificial que se alinee con el proceso de codificación del ambiente, puede usar el Copilot M365 de Microsoft. Solo tiene que proporcionar a M365 Copilot una descripción de su aplicación (el contenido de su PRD) y pedir a la IA que cree imágenes de diagramas reticulares de baja fidelidad. Para crear diagramas reticulares de alta fidelidad manualmente, puede utilizar una herramienta de diseño de UI/UX como Figma.

1. En la vista Chat, escriba el siguiente símbolo del sistema:

    ```md
    Save the low-fidelity wireframe diagrams as text files, one file for each web page and one for navigation.
    ```

1. Supervise la vista Chat para asegurarse de que se guardan todos los archivos y, a continuación, seleccione **Mantener**.

1. Tómese un par de minutos para revisar los diagramas reticulares.

    Si ve algún problema obvio que desee corregir, puede editar los diagramas reticulares directamente en Visual Studio Code. También puede pedir a GitHub Copilot que le ayude a refinar los diagramas reticulares.

    En este ejercicio, los diagramas reticulares (diseños de texto) no necesitan ser exactos y las retículas sugeridas deben ser suficientes sin modificaciones. Sin embargo, si experimenta problemas más adelante en el ejercicio al que se atribuye a los diagramas reticulares, puede pedir al agente GitHub Copilot que le ayude a refinarlos.

    > **Sugerencia**: Si no está seguro de cómo interpretar un diagrama reticular o si cree que uno de los diagramas puede ser incorrecto, pida a GitHub Copilot que explique los diagramas. Por ejemplo, puede pedir al agente GitHub Copilot que "revise los diagramas reticulares y los use para explicar el diseño de la interfaz de usuario y cómo interactúa el usuario con la aplicación". Si la explicación de GitHub Copilot no coincide con sus expectativas, puede pedir al agente GitHub Copilot que le ayude a actualizar los diagramas reticulares para que coincidan mejor con su experiencia de usuario prevista.

## Creación de una aplicación de prototipo inicial:

El agente GitHub Copilot puede usar los requisitos del producto y los diagramas reticulares para desarrollar una aplicación prototipo. Proporcionar los requisitos de producto y diagramas reticulares suficientemente detallados ayuda al agente a comprender la experiencia del usuario, las características de la aplicación y los objetivos de diseño que pretende para la aplicación.

- El PRD proporciona información detallada sobre el propósito de la aplicación, la audiencia de destino, las características y los requisitos técnicos.
- Los diagramas reticulares muestran la interfaz de usuario prevista y ayudan a describir las interacciones del usuario.

En esta tarea, usará el agente GitHub Copilot para crear una aplicación de prototipo inicial basada en los diagramas PRD y reticulares que creó.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. En Visual Studio Code, cree una carpeta denominada **ShoppingApp** en la carpeta VibeCoding-PrototypeApp.

    El agente GitHub Copilot necesita una carpeta vacía para usarla como área de trabajo para los nuevos archivos de aplicación.

    Visual Studio Code cargará la nueva carpeta en la vista del explorador.

    ```plaintext
    UNTITLED (WORKSPACE)
    └── VibeCoding-PrototypeApp
        ├── ShoppingApp
        ├── VibeCodingPRD.md
        ├── wireframe-checkout.txt
        ├── wireframe-navigation.txt
        ├── wireframe-product-details.txt
        ├── wireframe-products.txt
            ```└── wireframe-shopping-cart.txt
    ```

1. Agregue los diagramas PRD y reticulares al contexto de chat.

    Al agregar estos archivos al contexto de chat, se indica al agente GitHub Copilot que haga referencia a los archivos al generar una respuesta.

    Puede agregar archivos al contexto de chat arrastrando y colocándolos desde la vista Explorer a la vista Chat o usando el botón **Agregar contexto** ubicado en el área inferior izquierda de la vista Chat.

1. En la vista Explorer, seleccione la carpeta **ShoppingApp** .

1. En la vista Chat, escriba el siguiente símbolo del sistema:

    ```md
    I want you to create a prototype shopping app using the information in my PRD and wireframe diagrams. Create the prototype app in the selected 'ShoppingApp' folder. The prototype should implement the following: basic use case functionality, simple navigation, a sample dataset, and basic styling. After creating the prototype app, add a '.github/copilot-instructions.md' file to the workspace. Add the contents of the PRD and wireframe files to the 'copilot-instructions.md' file.
    ```

    El agente GitHub Copilot usa este mensaje para generar una aplicación de prototipo inicial en función de los requisitos que haya definido.

    - El agente comprueba la carpeta **ShoppingApp** para asegurarse de que está vacía y lista para usarla como área de trabajo.
    - El agente usa los diagramas PRD y reticular para crear los archivos de la aplicación prototipo. Los archivos siguientes se crean en la carpeta **ShoppingApp**:

        - **app.js**: Contiene el código JavaScript que implementa la funcionalidad de la aplicación, como administrar el catálogo de productos, el carro de la compra y la navegación.
        - **index.html**: Actúa como punto de entrada para la aplicación web, configurando la estructura básica y vinculando los estilos y scripts.
        - **styles.css**: Proporciona el diseño visual y el diseño dinámico para la aplicación web prototipo.

    - El agente agrega un archivo **.github/copilot-instructions.md** al área de trabajo y, a continuación, agrega el contenido de los archivos PRD y reticular al archivo **copilot-instructions.md**.

    > **SUGERENCIA**: Puede almacenar instrucciones personalizadas en el área de trabajo o el repositorio en un archivo .github/copilot-instructions.md. Las instrucciones personalizadas le permiten describir directrices o reglas comunes para obtener respuestas que coincidan con sus prácticas de codificación específicas y la pila técnica. En lugar de incluir manualmente este contexto en cada consulta de chat, las instrucciones personalizadas incorporan automáticamente esta información con cada solicitud de chat. Estas instrucciones solo se aplican al área de trabajo donde se encuentra el archivo.

1. Supervise la vista Chat para realizar un seguimiento del progreso del agente a medida que funciona en la aplicación prototipo.

    > **NOTA**: Aunque el agente GitHub Copilot realiza tareas como agente autónomo, puede solicitar ayuda al realizar determinadas tareas. Para ayudar al agente, responda a las indicaciones que aparecen en la vista Chat. Por ejemplo, si el agente solicita permiso para ejecutar un comando en el terminal, seleccione **Ejecutar** para permitir que el agente ejecute el comando. Si el agente solicita una aclaración sobre sus requisitos, proporcione una respuesta que ayude al agente a comprender sus requisitos.

1. En la vista Chat, para guardar los archivos de la aplicación prototipo, seleccione **Mantener**.

1. Expanda la carpeta **ShoppingApp**.

    La carpeta debería contener los siguientes archivos:

    ```plaintext
    ShoppingApp
    ├── .github
    │   └── copilot-instructions.md
    ├── app.js
    ├── index.html
    ├── styles.css
    ```

1. Dedique un par de minutos a revisar cada uno de los archivos de código.

    - El archivo **index.html** actúa como punto de entrada para una aplicación web. Configura la estructura básica de la aplicación y vincula los estilos y los archivos de scripts.
    - El archivo **styles.css** proporciona el diseño visual y el diseño dinámico de la aplicación web prototipo.
    - El archivo **app.js** contiene el código JavaScript que administra el catálogo de productos, el carro de la compra, la navegación y la representación de la interfaz de usuario.

    Si el tiempo lo permite, considere la posibilidad de pedir a GitHub Copilot que genere una explicación detallada de cada archivo.

1. Abra el archivo **index.html** en el editor de Visual Studio Code.

1. En el menú **Ejecutar**, seleccione **Ejecutar sin depuración**

    Si se le solicita, seleccione su elección del explorador para ejecutar la aplicación.

1. Con la aplicación prototipo abierta en el explorador, pruebe los casos de uso que aparecen en el PRD y compruebe que la aplicación prototipo ofrece la funcionalidad esperada.

    Los casos de uso describen la funcionalidad básica que debe implementar la aplicación prototipo. Por ejemplo:

    - Como usuario, puedo examinar una lista de productos de frutas.
    - Como usuario, puedo ver información detallada sobre un producto seleccionado.
    - Como usuario, puedo agregar productos a mi carro de la compra y ajustar cantidades.
    - Como usuario, puedo revisar y actualizar mi carro antes de la compra.
    - Como usuario, puedo ver un resumen de mi pedido y "procesarlo" (sin transacción real).
    - Como usuario, puedo navegar entre las páginas Productos, Detalles del producto, Carro de la compra y Finalización de la compra.

1. Después de comprobar los casos de uso, pruebe el comportamiento dinámico de la aplicación mediante el cambio de tamaño de la ventana del explorador.

    La aplicación prototipo debe tener una interfaz de usuario dinámica que se adapte automáticamente para poder visualizarse tanto en ordenadores de sobremesa como en teléfonos móviles.

1. Intente probar la barra de navegación contraída.

    Ha especificado que la barra de navegación debe contraerse cuando el ancho de la página sea inferior a 300 píxeles. Cuando se contrae, la barra de navegación debe mostrar una o dos letras para representar cada una de las páginas web de la aplicación.

    > **NOTA**: La mayoría de los exploradores de escritorio (incluido Microsoft Edge) aplican un ancho de ventana mínimo mayor que 300 px (a menudo alrededor de 320–400 px). Esto significa que es posible que no pueda reducir manualmente el tamaño de la ventana del navegador lo suficiente como para provocar el colapso de la barra de navegación.

1. (Opcional) Realice pruebas adicionales para asegurarse de que la aplicación prototipo cumple con sus expectativas.

    Si lo desea, tome notas durante las pruebas. Puede usar las notas durante la siguiente tarea para ayudar a refinar la aplicación prototipo.

1. Cierre la ventana del explorador y detenga la aplicación presionando Mayús+F5 en Visual Studio Code.

## Refinar la aplicación de prototipo:

La aplicación de prototipo inicial ya debe proporcionar una implementación básica de los requisitos del producto. Sin embargo, es probable que se pueda refinar y mejorar, y es posible que no logre completamente la experiencia de usuario prevista.

En esta tarea, usará el agente GitHub Copilot para refinar las características y el comportamiento de la aplicación prototipo.

Completa los siguientes pasos para usar esta sección del ejercicio:

1. En la vista Chat, para ajustar el punto de interrupción de la barra de navegación contraída, escriba el símbolo del sistema siguiente:

    ```md
    #codebase Refactor the prototype app to use a higher breakpoint for the collapsed navigation bar. Change from 300 to 600px. Update the copilot-instructions.md file to explain the updated 600px requirement.
    ```

    Si el agente implementó una barra de navegación que cambia la orientación cuando la pantalla se estrecha (cambia de vertical a horizontal), use el siguiente comando para actualizar el comportamiento de la barra de navegación:

    ```md
    #codebase Refactor the code to ensure that the navigation bar stays on the left-side of the app for all devices types and sizes. The navigation bar should be responsive and maintain its position, in either an expanded or collapsed mode.
    ```

1. Dedique un minuto a revisar las actualizaciones de código que genera el agente GitHub Copilot en respuesta al mensaje.

1. En la vista Chat, seleccione **Mantener** para guardar los archivos de la aplicación prototipo actualizados.

1. Vuelva a ejecutar la aplicación y asegúrese de que la barra de navegación se contrae cuando el ancho sea inferior a 600 píxeles.

1. Cierre la ventana del explorador y detenga la aplicación presionando Mayús+F5 en Visual Studio Code.

1. En la vista Chat, escriba el siguiente símbolo del sistema y, a continuación, supervise el progreso del agente:

    ```md
    #codebase Update the prototype app to display an emoji in the nav bar for each of the web pages. Ensure that the emoji is centered horizontally in the nav bar when the nav bar is collapsed. Update the copilot-instructions.md file to include this product requirement.
    ```

1. Dedique un minuto a revisar las actualizaciones de código.

1. En la vista Chat, para guardar los archivos de la aplicación prototipo actualizados, seleccione **Mantener**.

1. Vuelva a ejecutar la aplicación y compruebe que los emojis se muestran correctamente en la barra de navegación.

    La barra de navegación debe mostrar un emoji que represente cada página web. El emoji debe centrarse horizontalmente en la barra de navegación cuando se contrae.

    Si ve algún problema adicional con la barra de navegación, puede pedir al agente GitHub Copilot que le ayude a refinar el comportamiento de la barra de navegación. Por ejemplo, puede pedir al agente que "#codebase Refactorice el código para asegurarse de que la barra de navegación siempre está visible y solo tenga dos fases, expandida o contraída".

1. Cierre la ventana del explorador y detenga la aplicación presionando Mayús+F5 en Visual Studio Code.

1. En la vista Chat, para identificar oportunidades adicionales de mejoras, escriba el siguiente mensaje:

    ```md
    #codebase Review the product requirements and wireframe diagrams in the copilot-instructions.md file. Are there any features or requirements that are missing from the implementation? Are there obvious opportunities to improve the user experience?
    ```

1. Revisa la respuesta de GitHub Copilot.

    Identifique tres o más mejoras sugeridas que le gustaría implementar.

1. Cree un mensaje que describa las mejoras que desea implementar.

    Use las sugerencias de GitHub Copilot y las notas de prueba que haya creado para implementar mejoras. Por ejemplo, puede pedir al agente GitHub Copilot que le ayude a implementar los siguientes cambios:

    ```md
    #codebase Implement the following improvements to the prototype app:

    - Replace alert() popups with in-app notification banners or toasts.
    - Add a confirmation/thank you message after processing an order.
    - Add a visual indicator (badge) for the number of items in the cart on the nav bar.

    Ensure that the copilot-instructions.md file is updated to reflect any changes to the product features, technical requirements, user experience, or other measurable characteristics.
    ```

    > **SUGERENCIA**: Puede copiar información de la respuesta de GitHub Copilot para ayudar a construir el nuevo mensaje. También puede consultar las secciones de la respuesta anterior en el mensaje.

1. Si el tiempo lo permite, continúe refinando la aplicación con las sugerencias de GitHub Copilot y sus propias ideas.

1. En el menú Archivo, seleccione **Guardar área de trabajo como...**.

1. Para guardar el archivo de configuración del área de trabajo (VibeCoding-PrototypeApp.code-workspace) en la carpeta **VibeCoding-PrototypeApp**, seleccione **Guardar**.

    Este archivo permite guardar y volver a abrir el área de trabajo con la misma estructura y configuración de carpetas.

## Resumen

En este ejercicio, usará un proceso de codificación de ambiente y el agente GitHub Copilot para crear un prototipo de aplicación de comercio electrónico. Ha definido los requisitos del producto, ha creado una aplicación de prototipo inicial y ha refinado la aplicación prototipo para satisfacer mejor la experiencia de usuario y la funcionalidad deseadas.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Si ha realizado algún cambio, reviértalos según sea necesario. Si usa un equipo local como entorno de laboratorio, puede archivar o eliminar la carpeta de la aplicación prototipo que creó para este ejercicio.
