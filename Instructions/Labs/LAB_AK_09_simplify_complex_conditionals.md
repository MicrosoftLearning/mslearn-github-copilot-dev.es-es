---
lab:
  title: "Ejercicio: Simplificación de condicionales complejos mediante GitHub\_Copilot"
  description: "Aprenda a refactorizar lógica condicional compleja en código base de C# mediante herramientas de GitHub\_Copilot."
---

# Simplificación de condicionales complejos mediante GitHub Copilot

La lógica condicional en las aplicaciones empresariales a menudo crece más compleja y profundamente anidada con el tiempo, lo que dificulta la lectura, el mantenimiento y la prueba del código. Desafortunadamente, la misma complejidad que dificulta el mantenimiento del código también puede dificultar la refactorización. La dificultad aumenta cuando el código está estrechamente unido a la lógica de negocios.

En este ejercicio, usará GitHub Copilot para analizar el código que contiene lógica condicional profundamente anidada, refactorizar la lógica de código y, a continuación, probar el código refactorizado para asegurarse de que funciona según lo previsto. Use GitHub Copilot en el modo Preguntar para comprender el código y explorar las opciones que simplifican la lógica. Puede usar GitHub Copilot en modo agente para refactorizar el código mediante la extracción de lógica condicional compleja en métodos auxiliares más pequeños y centrados y para reducir el anidamiento. Simplificar las condicionales complejas facilita la lectura, el mantenimiento y la prueba del código.

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

### Descarga de proyectos de código de ejemplo

Siga estos pasos para descargar los proyectos de ejemplo y abrirlos en Visual Studio Code:

1. Abra una ventana del explorador en el entorno de laboratorio.

1. Para descargar un archivo ZIP que contenga los proyectos de aplicación de ejemplo, abra la URL siguiente en el explorador: [Laboratorio de GitHub Copilot: desarrollo de características de código](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/GHCopilotEx9LabApps.zip)

    El archivo ZIP se denomina **GHCopilotEx9LabApps.zip**.

1. Extraiga los archivos del archivo **GHCopilotEx9LabApps.zip**.

    Por ejemplo:

    1. Vaya a la carpeta de descargas del entorno de laboratorio.

    1. Haga clic con el botón derecho en *GHCopilotEx9LabApps.zip* y, después seleccione **Extraer todo**.

    1. Seleccione **Mostrar los archivos extraídos al completar** y, a continuación, **Extraer**.

1. Copia la carpeta **GHCopilotEx9LabApps** en una ubicación que sea fácil de acceder, como la carpeta Escritorio de Windows.

1. Abra la carpeta **GHCopilotEx9LabApps** en Visual Studio Code.

    Por ejemplo:

    1. Abra Visual Studio Code en el entorno de laboratorio.

    1. En Visual Studio Code, en el menú **Archivo**, seleccione **Abrir archivo**.

    1. Vaya a la carpeta Escritorio de Windows, seleccione **GHCopilotEx9LabApps** y luego **Seleccionar carpeta**.

1. En la vista EXPLORADOR DE SOLUCIONES de Visual Studio Code, compruebe la siguiente estructura del proyecto:

    - GHCopilotEx9LabApps\
        - ECommercePricingEngine\
            - Dependencies\
            - ECommercePricingDemo.cs
            - Output-ECommercePricingEngine.txt
            - SecurityTest.cs
        - LoanApprovalWorkflow\
            - Dependencies\
            - LoanApprovalDemo.cs
            - Output-LoanApprovalWorkflow.txt
            - SecurityTest.cs

## Escenario del ejercicio

Es desarrollador de software y trabaja para una empresa de consultoría. Los clientes necesitan ayudar a refactorizar lógica condicional compleja para mejorar la legibilidad y el mantenimiento del código. Se le asigna a la aplicación siguiente:

- Motor de precios de comercio electrónico: La primera aplicación es un motor de precios de comercio electrónico que calcula los precios dinámicos en función de varias reglas de negocio. Los condicionales incluyen niveles de pertenencia, valores de pedido, códigos de cupón, categorías de productos y reglas de envío.
- Flujo de trabajo de aprobación de préstamos: La segunda aplicación es un flujo de trabajo de aprobación de préstamos que evalúa las solicitudes de préstamo en función de varios factores. Entre los condicionales se incluyen ingresos, estado laboral, ratios de deuda, garantías e historial de crédito.

Este ejercicio incluye las siguientes tareas:

1. Revise el código base del motor de precios de comercio electrónico.
1. Identifique las oportunidades de refactorización en el código de precios de comercio electrónico mediante GitHub Copilot.
1. Refactorice el código de precios de comercio electrónico mediante el agente de GitHub Copilot.
1. Pruebe el código de precios de comercio electrónico refactorizado.
1. (OPCIONAL) Simplifique los condicionales complejos en la aplicación de demostración LoanApprovalWorkflow.

### Revise el código base del motor de precios de comercio electrónico.

El primer paso de cualquier esfuerzo de refactorización es asegurarse de que comprende el código base existente.

En esta tarea, abrirá el proyecto del motor de precios de comercio electrónico y usará GitHub Copilot para ayudar a analizar la lógica condicional compleja.

Realice los pasos siguientes para completar esta tarea:

1. Asegúrese de que tiene abierta la carpeta GHCopilotEx9LabApps en Visual Studio Code.

    Consulte la sección **Antes de empezar** si no ha descargado los proyectos de código de ejemplo.

1. Compruebe que el proyecto de código **ECommercePricingEngine** se compila correctamente.

    Por ejemplo, en la vista EXPLORADOR DE SOLUCIONES, haga clic con el botón derecho en **ECommercePricingEngine**y, a continuación, seleccione **Compilar**.

    Verá advertencias "No se puede convertir el literal NULL en un tipo de referencia que no acepta valores NULL". al compilar el proyecto, pero no debería haber ningún error. Puede omitir las advertencias para los fines de este ejercicio.

1. Abra la vista GitHub Copilot Chat.

    Si la Vista de chat aún no está abierta, puede abrirla seleccionando el icono **Chat** situado en la parte superior de la ventana de Visual Studio Code, justo a la derecha del cuadro de texto Buscar.

1. En la vista Chat, asegúrese de que el modo de chat está establecido en **Preguntar** y el modelo está establecido en **GPT-4.1**.

    Estos valores están disponibles en la esquina inferior izquierda de la vista Chat. El modo **Preguntar**de GitHub Copilot se usa para formular preguntas generales de programación y para generar explicaciones relacionadas con el código. El **modelo GPT-4.1** , que se incluye con el plan gratis de GitHub Copilot, es una buena opción para el análisis de código, las explicaciones y las instrucciones relacionadas con la refactorización de código.

    Usará el modo **Agente** de GitHub Copilot más adelante en este ejercicio, pero por ahora usará el modo **Preguntar** para el análisis y las explicaciones del código.

    > [!NOTE]
    > Algunos modelos son más adecuados para tareas específicas que otras. El modelo que seleccione puede afectar a las respuestas generadas por GitHub Copilot. Después de completar este ejercicio de laboratorio con la configuración recomendada, es posible que desee repetir el ejercicio con diferentes modelos y comparar los resultados.

1. En Visual Studio Code, abra el archivo **ECommercePricingDemo.cs**.

    Este archivo incluye las siguientes clases:

    - Usuario: Representa a un cliente, con propiedades para el nivel de pertenencia, el historial de compras y los estados especiales (estudiante, empleado, corporativo, etc.). Se usa para determinar la idoneidad de varios descuentos y beneficios.
    - Cupón: Representa un cupón de descuento o envío, con propiedades para código, validez, tipo (porcentaje o envío) y valor. Se usa en los cálculos de precios para aplicar descuentos adicionales o envío gratuito.
    - Artículo: Representa un producto en un pedido, con el nombre, la categoría y el precio. Se usa para crear pedidos y calcular subtotales y descuentos específicos de la categoría.
    - Pedido: Representa el pedido de un cliente, que contiene una lista de artículos, región de envío, cupón, evento, método de pago y otras marcas específicas del pedido. Proporciona métodos para calcular subtotales, comprobar la presencia de categorías y determinar las características de orden (por ejemplo, valor alto, categorías mixtas).
    - PricingEngine: Contiene la lógica principal para calcular el precio final de un pedido. Aplica descuentos basados en el estado del usuario, los detalles del pedido, los cupones y las reglas específicas de la categoría. Controla las comprobaciones de seguridad y garantiza que los descuentos y los precios permanezcan dentro de los límites seguros.
    - Program: El punto de entrada. Crea usuarios de prueba, cupones y pedidos y, a continuación, ejecuta una serie de escenarios de precios complejos mediante las clases anteriores. Muestra cómo el motor de precios aplica su lógica en diferentes situaciones.

    Cada clase modela una entidad o proceso real en un sistema de precios de comercio electrónico e interactúan en la clase Program para simular y probar los cálculos de precios. Por ejemplo, las instancias de Usuario, Pedido y Cupón se pasan a PricingEngine.CalculateFinalPrice para calcular y mostrar el precio final con todos los descuentos aplicables.

1. Busque la clase **PricingEngine** y, a continuación, seleccione todo el método **CalculateFinalPrice**.

    El método CalculateFinalPrice contiene lógica condicional compleja y profundamente anidada que evalúa los niveles de pertenencia, los eventos estacionales, las cuentas corporativas, los servicios de suscripción y varios escenarios de descuento.

1. Dedique un minuto a desplazarse por la lógica condicional en el método de **CalculateFinalPrice**.

    El método es complejo y difícil de leer, con varios condicionales anidados que controlan diferentes escenarios de descuento. La complejidad surge de las distintas reglas de negocio que deben aplicarse en función del estado del usuario, los detalles del pedido y los códigos de cupón.

1. Haga clic con el botón derecho en el código seleccionado y seleccione **Copilot** > **Explicar**.

    GitHub Copilot analizará el método CalculateFinalPrice y proporcionará una explicación detallada de lo que hace el código.

1. Dedique unos minutos a revisar la explicación de GitHub Copilot.

    La explicación debe resaltar las principales categorías de descuento, como la pertenencia jerárquica, las aplicaciones de cupones, los incentivos de compra masiva y las reglas específicas de la categoría.

    Por ejemplo:

    ```md
    The CalculateFinalPrice method is a comprehensive pricing engine for an e-commerce scenario. It starts by validating its inputs, ensuring that both the user and order objects are not null and that the order data is valid. This prevents null reference exceptions and guards against invalid or malicious input. The method then calculates the base total of the order and checks that it falls within a reasonable range, aborting the calculation if the total is suspiciously low or high.
    
    Next, the method initializes variables for the discount percentage, shipping cost, and a list to track all applied discounts. The core of the function is a series of nested conditional blocks that determine which discounts the user is eligible for. These are based on membership level (Premium, Gold, Silver), user attributes (such as being a student, employee, or first-time buyer), order characteristics (like high value, bulk purchase, or mixed categories), and special events (such as Black Friday or Back to School). Each eligible discount is added using the SafeAddDiscount helper, which ensures the total discount does not exceed a maximum cap and records a description of the discount.
    
    The method also handles coupon codes, applying either a percentage discount or free shipping, with additional enhancements for certain membership levels or order types. For example, Premium members may receive a boosted coupon value, and further stacking is possible during special events or for corporate accounts.
    
    After all discounts are considered, the method applies additional bulk purchase incentives if the order contains a large number of items. It then enforces a final cap on the total discount to prevent excessive reductions. The final price is calculated using ApplyCategorySpecificDiscounts, which applies category-based discount caps (e.g., electronics discounts are limited to 15%). The shipping cost is added, and the final price is ensured to be above a minimum threshold.
    
    Finally, the method outputs a summary of the calculation, including the base total, all applied discounts, the total discount percentage (with a note about category caps), the shipping cost, and the final price. This approach ensures transparency and traceability in how the final price is determined, while also enforcing business rules and security best practices.
    ```

    Dedicar tiempo a comprender el código existente le ayudará a reconocer y seleccionar opciones de refactorización más adelante en este ejercicio.

1. En la Vista de chat, para obtener un análisis más profundo del proceso de cálculo, escriba el mensaje siguiente:

    ```plaintext
    @workspace Explain the business logic flow in the CalculateFinalPrice method. What are the different discount paths and how do they interact with each other? What are the key business rules that govern pricing calculations?
    ```

    Este análisis debe ayudarle a comprender cómo interactúan las diferentes categorías de descuento y qué reglas de negocio se aplican en cada paso del cálculo de precios.

1. Dedique un minuto a revisar la explicación proporcionada por GitHub Copilot.

    La respuesta debe identificar las rutas de acceso de descuento principales y cómo interactúan entre sí. Por ejemplo:

    ```md
    The `CalculateFinalPrice` method in `ECommercePricing.PricingEngine` implements a layered, rule-driven approach to pricing calculation for an e-commerce order. Here’s how the business logic flows and how the discount paths interact:
    
    ### 1. **Input Validation**
    - The method first validates that both `user` and `order` are not null and that the order data is valid (e.g., no negative prices, all required fields present).
    - It checks that the order subtotal is within allowed bounds (greater than zero and less than $1,000,000).
    
    ### 2. **Base Discount Initialization**
    - The method initializes the discount percentage (`discountPercent`) to 0 and calculates the base shipping cost.
    
    ### 3. **Membership-Based Discount Paths**
    - The first major decision point is the user's membership level:
      - **Premium:** Starts with a 15% discount, then applies additional discounts for high-value orders, seasonal events, corporate accounts, subscriptions, loyalty (years as member), lifetime spending, and express shipping. Each condition is nested, so deeper benefits require all previous conditions to be met.
      - **Gold:** Starts with a 12% discount, then adds bonuses for seasonal events, bulk purchases, category diversity, employee status, pre-orders, and alternative payment methods. These are also nested, but less deeply than Premium.
      - **Silver:** Starts with 8%, with further bonuses for students, back-to-school events, bulk purchases, electronics focus, gift wrap, and express shipping. These are nested within the student path.
      - **First-Time Buyer:** If the user is a first-time buyer (and not a member), a 10% discount is applied, with further bonuses for seasonal events, order size, payment method, high-value orders, premium shipping regions, and express shipping.
    
    ### 4. **Coupon Application**
    - If a coupon is present:
      - **Valid Percent Coupon:** The coupon value is capped at 50%. Premium and Gold members get a multiplier (Premium: 1.3x up to 50%, Gold: 1.2x up to 40%). Additional stacking occurs for Premium members on Black Friday, corporate accounts, and bulk orders, with each step further capping the discount.
      - **Valid Shipping Coupon:** Shipping is set to zero for domestic orders or Premium members.
      - **Expired Coupon:** No discount is applied, and a message is logged.
    
    ### 5. **Bulk Purchase Incentives**
    - Additional discounts are applied for orders with 10+ items (5%) or 20+ items (8%).
    
    ### 6. **Discount Capping**
    - The total discount percentage is capped at 95% to prevent excessive reductions.
    
    ### 7. **Category-Specific Discount Rules**
    - The final discount is applied with category-specific caps:
      - **Electronics:** Discount capped at 15%.
      - **Clothing:** Discount capped at 20% (25% during Back-to-School).
      - **Accessories/Other:** Full discount applies.
    
    ### 8. **Final Price Calculation**
    - The final price is the sum of all discounted category subtotals plus shipping, with a minimum enforced price of $0.01.
    
    ### 9. **Result Output**
    - The method prints the base total, all applied discounts, the total discount percentage (with a note about the electronics cap), shipping cost, and the final price.
    
    ---
    
    ## **Discount Path Interactions**
    - **Nesting:** Many discounts are nested, meaning deeper discounts require all previous conditions to be true (e.g., Premium members with high-value orders, during Black Friday, who are also corporate accounts, etc.).
    - **Stacking:** Discounts from different sources (membership, coupons, bulk, etc.) are added together, but always subject to the overall cap.
    - **Category Caps:** Even if the total discount is high, certain categories (like electronics) have stricter caps, so the effective discount for those items may be lower than the overall discount.
    
    ---
    
    ## **Key Business Rules**
    - **Validation:** Orders and users must be valid; otherwise, pricing is aborted.
    - **Membership Drives Discounts:** Higher membership levels unlock deeper and more complex discount paths.
    - **Coupons Are Enhanced by Membership:** Premium and Gold members get more value from percent-off coupons.
    - **Bulk and Seasonal Bonuses:** Large orders and seasonal events can trigger additional discounts.
    - **Category Protection:** Electronics and clothing have maximum discount caps to protect margins.
    - **Shipping Can Be Discounted:** Shipping can be free with certain coupons or for Premium members.
    - **Discount Caps:** No combination of discounts can exceed 95% off the order.
    - **Transparency:** All applied discounts are tracked and displayed for auditability.
    
    For more details, see the full implementation in ECommercePricingDemo.cs, especially the `ECommercePricing.PricingEngine.CalculateFinalPrice` method.
    ```

1. Compare la explicación de GitHub Copilot con sus propias observaciones de la lógica condicional compleja en el método `CalculateFinalPrice`.

    Sus propias observaciones probablemente identificaron las fuentes de descuento principales: niveles de pertenencia, códigos de cupón e incentivos de compra masiva. La explicación de GitHub Copilot debe admitir sus observaciones y proporcionar información adicional sobre cómo interactúan estas rutas de descuento y las reglas empresariales clave que rigen los cálculos de precios.

    - Observe cómo los diferentes niveles de pertenencia (Premium, Gold, Silver) aplican descuentos y cómo se trata a los compradores por primera vez.
    - Observe cómo se evalúa y aplica la validación de cupones y cómo interactúan los descuentos de cupones con los descuentos de pertenencia.
    - Observe cómo se aplican los descuentos basados en el volumen en función de los recuentos de artículos.

    Las reglas de negocio se aplican a través de los condicionales anidados, lo que garantiza que los descuentos se aplican correctamente en función del estado del usuario, los detalles del pedido y los códigos de cupón. Estas reglas deben avanzar con el proceso de refactorización.

1. Ejecute el proyecto ECommercePricingEngine y revise el resultado.

    El resultado debe mostrar los precios base y con descuento para varias combinaciones de usuario, pedido y cupón. Al final de este ejercicio, el código refactorizado debe generar los mismos resultados que el código original.

    Es posible que haya observado que el resultado incluye pruebas de seguridad básicas para entradas no válidas e intentos malintencionados de manipular precios. Aunque estas pruebas no representan todos los vectores de ataque posibles o el nivel de prueba necesario en una aplicación de producción, sirven como recordatorio de que garantizar la calidad y la seguridad del código es un requisito. El archivo **SecurityTest.cs** forma parte del proyecto ECommercePricingEngine.

    > [!NOTE]
    > Se puede encontrar una copia del resultado en el archivo **Output-ECommercePricingEngine.txt** incluido en la carpeta ECommercePricingEngine. Puede crear su propio archivo de resultado si desea comparar resultados o si modifica los datos de ejemplo. Cuando llegue al final de este ejercicio, usará el archivo de resultado para asegurarse de que el código refactorizado genera los mismos resultados que el código original.

    Para ejecutar el proyecto: Si tiene el archivo ECommercePricingDemo.cs abierto en el editor de Visual Studio Code, puede ejecutar el proyecto seleccionando el botón Ejecutar (Ejecutar proyecto asociado a este archivo) que se encuentra encima de la esquina superior derecha del panel del editor. Para ejecutar el proyecto desde la vista EXPLORADOR DE SOLUCIONES, haga clic con el botón derecho en **ECommercePricingEngine**, seleccione **Depurar** y, a continuación, seleccione **Iniciar nueva instancia**.

### Identifique las oportunidades de refactorización en el código de precios de comercio electrónico mediante GitHub Copilot.

GitHub Copilot es una excelente herramienta para analizar código complejo e identificar oportunidades de refactorización de código.

En esta tarea, usará GitHub Copilot para identificar oportunidades de refactorización específicas y sugerir métodos auxiliares que simplifican las condiciones complejas. Usará observaciones de la tarea anterior para ayudar a construir las indicaciones que proporcione a GitHub Copilot.

Realice los pasos siguientes para completar esta tarea:

1. Asegúrese de que tiene abierta la vista Chat de GitHub Copilot con el modo **Preguntar** y el modelo **GPT-4.1** seleccionado.

1. Agregue el archivo **ECommercePricingDemo.cs** al contexto de chat mediante la operación de arrastrar y soltar.

    Aunque ECommercePricingDemo.cs ya está abierto en el editor de Visual Studio Code, agregarlo al contexto de chat anima a GitHub Copilot a analizar todo el archivo de código, lo que puede dar lugar a sugerencias más precisas. Agregar archivos relevantes al contexto de chat es un procedimiento recomendado al usar GitHub Copilot, incluso cuando se incluyen las etiquetas **@workspace** o **#codebase** en el mensaje.

1. Envíe un mensaje que pida a GitHub Copilot que identifique las oportunidades de refactorización que mejoran la modularidad de código relacionada con las principales rutas de descuento.

    Tenga en cuenta los siguientes elementos al construir el mensaje:

    - Indique a GitHub Copilot que se centre en el método **CalculateFinalPrice** y sus condicionales anidados.
    - Pida a GitHub Copilot que sugiera opciones que muevan lógica compleja a métodos auxiliares de responsabilidad única más fáciles de administrar.
    - Enumere las rutas de acceso de descuento principales que se deben tener en cuenta para la extracción en métodos auxiliares.
    - Resalte la importancia de mantener la lógica de negocios al tiempo que simplifica la estructura de código.

    A menudo resulta beneficioso que GitHub Copilot tenga en cuenta las interacciones del código al analizarlo. Puede usar la etiqueta **@workspace** o **#codebase** para indicar a GitHub Copilot que incluya todo su código base en su análisis.

    Por ejemplo:

    ```plaintext
    @workspace Analyze the CalculateFinalPrice method and suggest refactoring opportunities. Include options that move the nested conditional logic into more manageable, single-responsibility helper methods. Focus on the main discount paths: membership discounts, coupon discounts, and bulk discounts. Maintain the business logic while simplifying the code structure.
    ```

    GitHub Copilot analizará el método y sugerirá oportunidades específicas de refactorización, identificando patrones en las condiciones anidadas que pueden extraerse en métodos auxiliares.

1. Tómese un par de minutos para revisar las sugerencias de GitHub Copilot.

    La respuesta debe identificar oportunidades que mejoran la capacidad de administración del código y la modularidad, como extraer las principales rutas de acceso de descuento en métodos auxiliares y uno o varios enfoques para reducir el anidamiento.

    Por ejemplo:

    ```md
    Collecting workspace informationThe `ECommercePricing.PricingEngine.CalculateFinalPrice` method is functionally rich but contains deeply nested conditional logic, especially for membership, coupon, and bulk discounts. This makes the code harder to read, maintain, and test. Here are refactoring opportunities and suggestions:
    
    ## **Refactoring Opportunities**
    
    ### 1. **Extract Membership Discount Logic**
    Move the entire membership-based discount logic into a helper method, e.g., `ApplyMembershipDiscounts`. This method would encapsulate all the nested membership, event, and user-attribute checks, returning the updated discount and applied discounts.
    
    ### 2. **Extract Coupon Discount Logic**
    Move coupon handling into a method like `ApplyCouponDiscounts`. This would handle coupon validation, membership-based coupon boosts, and shipping coupon logic.
    
    ### 3. **Extract Bulk Discount Logic**
    Move the bulk purchase logic into a method such as `ApplyBulkDiscounts`.
    
    ### 4. **Reduce Nesting**
    Within each helper, use early returns or guard clauses where possible to reduce nesting.
    
    ### 5. **Encapsulate Discount State**
    Consider using a small struct or class (e.g., `DiscountContext`) to pass and update the discount percent and applied discounts list, reducing parameter clutter.
    ```

1. Envíe un mensaje de seguimiento que pregunte a GitHub Copilot cómo simplificar la lógica condicional compleja y reducir los niveles de anidamiento en el método CalculateFinalPrice.

    Las indicaciones de seguimiento son una excelente manera de refinar el análisis y obtener sugerencias más específicas de GitHub Copilot. En este caso, desea información adicional sobre la reducción de los niveles de anidamiento, aún dentro del contexto de condicionales complejos en el método CalculateFinalPrice. También puede usar avisos de seguimiento para solicitar procedimientos recomendados o para comprender el impacto que podrían tener los cambios sugeridos en el código.

    Por ejemplo:

    ```plaintext
    How can I simplify the complex conditional logic and reduce nesting levels in the CalculateFinalPrice method? For example, the method has multiple nested conditionals that apply different membership discounts based on user status and order details. What are some best practices for reducing nesting levels and improving readability? Explain the benefit of each approach when applied to the CalculateFinalPrice method.
    ```

1. Dedique un minuto a revisar las sugerencias de GitHub Copilot para simplificar la lógica condicional y reducir los niveles de anidamiento.

    GitHub Copilot debe proporcionar una lista de sugerencias para simplificar la lógica condicional y reducir los niveles de anidamiento. Algunas de las sugerencias pueden ser repeticiones de sugerencias anteriores, lo cual es de esperar. Sin embargo, debería ver nuevas sugerencias relacionadas con la reducción de los niveles de anidamiento y la mejora de la legibilidad, tales como:

    - Use las cláusulas de devolución anticipada o protección para aplanar la lógica, reducir la sangría y aclarar el flujo.
    - Use funciones auxiliares locales para quitar la duplicación y aclarar la intención.
    - Use expresiones de cambio o coincidencias de patrones para hacer que la lógica de pertenencia sea explícita y fácil de mantener.
    - Use métodos más pequeños por pertenencia para modularizar la lógica y facilitar la prueba y actualización.
    - Use variables booleanas para las condiciones para mejorar la legibilidad de las comprobaciones complejas.

> [!NOTE]
> Usará los resultados del análisis para ayudar a construir la tarea asignada al agente GitHub Copilot en la sección siguiente del ejercicio.

### Refactorice el código de precios de comercio electrónico mediante el agente GitHub Copilot.

GitHub Copilot tiene tres modos: **Preguntar**, **Editar** y **Agente**. Cuando se ejecuta en modo agente, GitHub Copilot funciona como agente de IA autónomo.

En modo agente:

- El mensaje especifica la tarea asignada al agente GitHub Copilot.
- GitHub Copilot usa la información de tareas y el código base para identificar los archivos de código pertinentes y establecer el contexto de la tarea.
- GitHub Copilot formula un proceso que puede usar para realizar la tarea. El agente usa un enfoque iterativo y revisiones de código para ayudar a garantizar que la tarea se ha completado correctamente.
- GitHub Copilot usa la Vista de chat para mantenerle informado a medida que funciona en la tarea asignada. También puede proporcionar explicaciones o justificaciones para los cambios que se realizan.
- GitHub Copilot puede invocar herramientas para ayudarle a realizar la tarea o para comprobar que los cambios de código funcionan correctamente.
- GitHub Copilot puede pausar durante la tarea y pedirle ayuda o aclaración. Es importante supervisar el chat y responder cuando se le pida que ayude al agente autónomo.
- GitHub Copilot actualiza el archivo de código en el editor de Visual Studio Code. Una vez completada la tarea, debe revisar los cambios realizados por GitHub Copilot antes de aplicarlos al código base (individual o colectivamente).

En esta sección del ejercicio, usará el agente GitHub Copilot para refactorizar la clase PricingEngine y simplificar la lógica condicional compleja en el método CalculateFinalPrice. La tarea que asigne al agente GitHub Copilot se basará en las sugerencias proporcionadas por GitHub Copilot durante el análisis de código (la tarea anterior).

Realice los pasos siguientes para completar esta tarea:

1. Asegúrese de que la vista Chat de GitHub Copilot está abierta en Visual Studio Code.

1. En la vista Chat, seleccione el modo **Agente**.

    El menú desplegable **Establecer modo** se encuentra en la esquina inferior izquierda de la vista Chat. Al seleccionar **Agente**, GitHub Copilot cambiará al modo Agente, lo que le permite trabajar de forma autónoma en tareas que asigne.

1. Dedique un minuto a identificar los requisitos de la tarea que asignará al agente GitHub Copilot.

    Debe escribir una tarea que explique su objetivo y describa los pasos que el agente GitHub Copilot puede usar para lograr ese objetivo.

    En este caso, el objetivo incluye los siguientes elementos:

    - Simplifique la lógica condicional compleja y reduzca los niveles de anidamiento.
    - Mejorar la legibilidad y el mantenimiento del código.
    - Conserve la funcionalidad existente y asegúrese de que el código refactorizado genera el mismo resultado que el código original.

    En la tarea anterior, ha pedido a GitHub Copilot que analice el código e identifique las oportunidades de refactorización. Ha generado dos conjuntos de sugerencias, uno para extraer lógica compleja en métodos auxiliares para mejorar la modularidad y otra para reducir los niveles de anidamiento y mejorar la legibilidad del código.

    Las oportunidades de refactorización identificadas en la tarea anterior pueden incluir:

    - Extraiga la lógica de descuento de nivel de pertenencia en un método auxiliar.
    - Extraiga la validación de cupones y la lógica de la aplicación en un método auxiliar.
    - Extraiga la lógica de descuento de nivel de pertenencia en un método auxiliar.
    - Use las cláusulas de devolución anticipada o protección para aplanar la lógica, reducir la sangría y aclarar el flujo.
    - Use funciones auxiliares locales para quitar la duplicación y aclarar la intención.
    - Use expresiones de cambio o coincidencias de patrones para hacer que la lógica de pertenencia sea explícita y fácil de mantener.
    - Use métodos más pequeños por pertenencia para modularizar la lógica y facilitar la prueba y actualización.
    - Use variables booleanas para las condiciones para mejorar la legibilidad de las comprobaciones complejas.

    La tarea que cree para el agente GitHub Copilot debe combinar la instrucción de objetivo y las oportunidades de refactorización que identificó.

    La tarea debe implementar la siguiente estructura organizativa:

    1. Instrucción objetivo: Explicar el objetivo general de la tarea.
    1. Actualizaciones de estructura de código/modularidad: Identifique las secciones de código grandes que se pueden extraer para mejorar la modularidad.
    1. Mejoras de código pequeñas o detalladas: Describir los enfoques específicos para reducir los niveles de anidamiento y mejorar la legibilidad.
    1. Resultado: Describir el resultado esperado del proceso de refactorización.

1. Construya una tarea que cumpla sus requisitos.

    La tarea debe incluir su objetivo y las oportunidades de refactorización sugeridas organizadas mediante la estructura organizativa sugerida.

    Por ejemplo:

    ```plaintext
    I need to simplify the complex conditional logic and reduce nesting levels in the CalculateFinalPrice method. The main areas of complexity are associated with membership discounts, coupon processing, and bulk discounts. Each of these areas could be moved into separate helper methods that are called from CalculateFinalPrice. There are several options to reduce nesting levels in the helper methods. Use early returns or guard clauses to flatten logic, reduce indentation, and clarify flow. Use local helper functions to remove duplication and clarify intent. Use switch expressions or pattern matching to make membership logic explicit and maintainable. Use smaller methods per membership to modularize logic and make it easier to test and update. Use Boolean variables for conditions to improve readability of complex checks. The goal is to improve code maintainability and readability while preserving the existing functionality and generated output.
    ```

    Esta tarea usa texto de lenguaje natural para describir el objetivo, las principales oportunidades de reestructuración y enfoques específicos para reducir los niveles de anidamiento y mejorar la legibilidad. La tarea también describe el resultado esperado del proceso de refactorización.

1. Use la Vista de chat para asignar la tarea al agente GitHub Copilot.

    El agente GitHub Copilot evaluará la tarea y el código base para desarrollar un enfoque para refactorizar CalculateFinalPrice y extraerá la lógica de descuento de pertenencia en un nuevo método auxiliar. El agente probará las actualizaciones de código en varias fases para asegurarse de que la refactorización es correcta y que la lógica de negocios permanece intacta.

    Después de enviar la tarea, el agente GitHub Copilot comenzará a trabajar en la tarea. Puede supervisar su progreso en la Vista de chat.

    > [!NOTE]
    > Si necesita realizar cambios en la tarea, puede editar el texto en la Vista de chat y volver a enviarlo. El agente GitHub Copilot volverá a evaluar la tarea y seguirá trabajando en ella.

1. Supervise la Vista de chat mientras el agente GitHub Copilot trabaja en la tarea.

    El agente proporcionará actualizaciones sobre su progreso, incluidos los desafíos que encuentre y cómo planea abordarlos. También puede solicitar aclaraciones o información adicional si es necesario. Si es necesario, proporcione ayuda respondiendo a las indicaciones del agente en la Vista de chat.

1. Una vez completada la tarea de refactorización, revise las actualizaciones sugeridas en el editor de Visual Studio Code.

    Revise siempre las actualizaciones sugeridas de GitHub Copilot antes de aceptarlas. Compruebe que las actualizaciones se alinean con la lógica de negocios, la funcionalidad de la aplicación y los estándares de codificación previstos.

    El código refactorizado debe incluir un método **CalculateFinalPrice** muy simplificado que consta principalmente de llamadas a métodos para métodos auxiliares que administran descuentos de pertenencia, descuentos de cupones y descuentos masivos. La complejidad del método original debe reducirse significativamente, lo que facilita la lectura y el mantenimiento.

    El método auxiliar de descuentos para miembros también debe refactorizarse para gestionar la compleja lógica relacionada con los niveles de pertenencia, con un método auxiliar adicional para cada nivel (Premium, Gold, Silver y compradores por primera vez).

1. En la Vista de chat, para aceptar todas las actualizaciones, seleccione **Mantener**.

    Puede rechazar los cambios sugeridos si no cumplen sus expectativas o puede aceptar un subconjunto de los cambios y rechazar otros. Trabajar con GitHub Copilot para refactorizar el código suele ser un proceso iterativo que incluye refinar las indicaciones para lograr los resultados previstos.

    Si se aceptan las actualizaciones sugeridas por GitHub Copilot y posteriormente se detecta que las sugerencias han introducido problemas que pueden ser difíciles de resolver en el futuro, se pueden revertir los cambios seleccionando **Deshacer última solicitud** en la Vista de chat o utilizando la función de deshacer de Visual Studio Code.

1. Pida a GitHub Copilot que explique las actualizaciones de refactorización de código que implementó.

    Por ejemplo:

    ```plaintext
    Explain the refactoring updates that you implemented to simplify the complex conditional logic, reduce nesting levels, and improve code maintainability and readability.
    ```

    GitHub Copilot proporcionará una explicación de los cambios realizados, incluido cómo se ha simplificado la lógica condicional compleja y cómo se ha mejorado la estructura de código.

    Por ejemplo:

    ```md
    Here’s an explanation of the refactoring updates made to simplify the complex conditional logic, reduce nesting, and improve maintainability and readability in the `CalculateFinalPrice` method:
    
    ### 1. **Separation of Concerns with Helper Methods**
    - The main discount logic was split into three focused helper methods: `ApplyMembershipDiscounts`, `ApplyCouponDiscounts`, and `ApplyBulkDiscounts`.
    - Each helper method is responsible for a single aspect of the discount calculation, making the main method concise and easy to follow.
    
    ### 2. **Flattened Membership Discount Logic**
    - The deeply nested membership discount logic was moved into `ApplyMembershipDiscounts`, which uses a `switch` statement to dispatch to smaller, membership-specific methods (`ApplyPremiumDiscounts`, `ApplyGoldDiscounts`, `ApplySilverDiscounts`, `ApplyFirstTimeBuyerDiscounts`).
    - Each of these methods uses guard clauses (early returns) and Boolean variables to flatten the logic, reducing indentation and clarifying the flow.
    
    ### 3. **Guard Clauses and Early Returns**
    - Instead of multiple nested `if` statements, each helper method uses guard clauses to exit early when a condition is not met. This keeps the main logic path at the top level and reduces cognitive load.
    
    ### 4. **Switch Expressions and Pattern Matching**
    - The use of `switch` in `ApplyMembershipDiscounts` makes the membership logic explicit and easy to extend or modify.
    - This approach also makes it clear which logic applies to which membership type.
    
    ### 5. **Boolean Variables for Readability**
    - Boolean variables (e.g., `altPayment`, `premiumPayment`) are used to clarify complex conditions, making the code more self-documenting and easier to read.
    
    ### 6. **Local Helper Methods for Duplication and Intent**
    - Smaller, focused methods encapsulate repeated or complex logic, such as safe discount addition and category percentage calculation.
    - This reduces code duplication and clarifies the intent of each operation.
    
    ### 7. **Preserved Business Logic and Output**
    - All business rules, discount caps, and output formatting are preserved, ensuring that the refactoring does not change the program’s behavior.
    
    ## **Benefits**
    - **Readability:** The main method is now a clear sequence of high-level steps.
    - **Maintainability:** Each discount rule is isolated, making it easier to update or test.
    - **Extensibility:** Adding or modifying discount rules is straightforward.
    - **Testability:** Each helper method can be unit tested independently.
    
    This refactoring transforms a complex, deeply nested method into a modular, maintainable, and readable pricing engine, while preserving all business requirements and output.
    ```

1. Dedique un minuto a revisar el código refactorizado en la clase PricingEngine.

1. Envíe un mensaje de seguimiento que pida a GitHub Copilot que explique partes específicas del código refactorizado o para comparar las versiones originales y refactorizaciones.

    Por ejemplo:

    ```plaintext
    Compare the original PricingEngine class with the new refactored version of the PricingEngine class. Explain the relationship between methods in the two versions. Explain the implementation of business rules in the two versions.
    ```

### Pruebe el código de precios de comercio electrónico refactorizado.

Las pruebas son fundamentales para asegurarse de que la refactorización no cambia el comportamiento de la lógica de negocios. Ejecutará el código con varios escenarios para comprobar que los cálculos siguen siendo coherentes.

Realice los pasos siguientes para completar esta tarea:

1. Compile el proyecto para comprobar que no haya errores de compilación.

    Por ejemplo, en la vista EXPLORADOR DE SOLUCIONES, haga clic con el botón derecho en **ECommercePricingEngine**y, a continuación, seleccione **Compilar**.

    Si hay errores de compilación, revise el código refactorizado y corrija los problemas. GitHub Copilot puede ayudar a resolver errores de compilación si es necesario.

1. Ejecute la aplicación para probar la lógica de precios refactorizado.

    Si tiene el archivo ECommercePricingDemo.cs abierto en el editor de Visual Studio Code, puede ejecutar el proyecto seleccionando el botón Ejecutar (Ejecutar proyecto asociado a este archivo) que se encuentra encima de la esquina superior derecha del panel del editor. Para ejecutar el proyecto desde la vista EXPLORADOR DE SOLUCIONES, haga clic con el botón derecho en **ECommercePricingEngine**, seleccione **Depurar** y, a continuación, seleccione **Iniciar nueva instancia**.

    La aplicación debe ejecutarse sin errores y mostrar los cálculos de precios para varios escenarios de prueba.

    > [!IMPORTANT]
    > Si el código refactorizado encuentra un error en tiempo de ejecución, revise los cambios realizados por el agente GitHub Copilot y resuelva los problemas mediante GitHub Copilot. Si es necesario, puede usar la opción **Deshacer última solicitud** en la Vista de chat para revertir el último conjunto de cambios y, a continuación, actualizar la tarea asignada al agente GitHub Copilot. La iteración de las solicitudes o tareas para refinar los resultados es una práctica estándar al trabajar con herramientas habilitadas para IA.

1. Pida a GitHub Copilot que compare el resultado generado por el código refactorizado con el resultado original.

    El resultado original, **Output-ECommercePricingEngine.txt**, se incluye en la carpeta ECommercePricingEngine.

    Puede crear un segundo archivo de resultado y pedir a GitHub Copilot que identifique las diferencias entre los dos archivos.

    El resultado debe ser idéntico, lo que confirma que la lógica de negocios permanece sin cambios al tiempo que mejora la legibilidad y el mantenimiento del código.

### (OPCIONAL) Simplifique los condicionales complejos en la aplicación de demostración LoanApprovalWorkflow.

Si el tiempo lo permite, simplifique los condicionales complejos en la aplicación de demostración LoanApprovalWorkflow con el mismo proceso que usó para simplificar la lógica de precios en la aplicación de ejemplo Flujo de trabajo de aprobación de préstamos.

En esta tarea opcional, aplicará las mismas técnicas que usó en el motor de precios de comercio electrónico para refactorizar la lógica condicional compleja en la aplicación de demostración flujo de trabajo de aprobación de préstamos. Analizará el código de aprobación del préstamo, identificará las oportunidades de refactorización y, a continuación, usará el agente GitHub Copilot para extraer condicionales complejos en métodos auxiliares más pequeños y centrados.

> [!IMPORTANT]
> Las instrucciones de esta tarea incluyen los pasos de proceso de alto nivel, pero no incluyen indicaciones sugeridas ni explicaciones detalladas. Puede consultar las tareas anteriores de este ejercicio para ver ejemplos de cómo construir mensajes y usar GitHub Copilot de forma eficaz.

Realice los pasos siguientes para completar esta tarea:

1. Expanda la carpeta del proyecto **LoanApprovalWorkflow**, abra el **archivo LoanApprovalDemo.cs** y, a continuación, revise el código.

1. Use GitHub Copilot para explicar el código de **LoanApprovalDemo.cs**, incluida la lógica condicional compleja en el método Calcular de la clase LoanEvaluator.

1. Ejecute el proyecto LoanApprovalWorkflow para probar la lógica de aprobación inicial del préstamo y crear un registro de la salida.

1. Use GitHub Copilot para identificar oportunidades de refactorización de código que simplifican las condiciones complejas, reducen los niveles de anidamiento y mejoran la legibilidad y el mantenimiento en la clase LoanEvaluator.

1. Asigne una tarea al agente GitHub Copilot que simplifica la lógica condicional compleja, reduce los niveles de anidamiento y mejora la legibilidad y el mantenimiento en la clase LoanEvaluator (refactorizar el método Calcular).

    Por ejemplo, podría pedir al agente GitHub Copilot que cree métodos auxiliares para la evaluación de la puntuación de crédito, la verificación de ingresos y empleo, los cálculos de proporción financiera, la idoneidad del programa gubernamental y la determinación de los términos de préstamo.

1. Use el agente GitHub Copilot para simplificar la lógica condicional compleja y reducir los niveles de anidamiento en los métodos auxiliares.

1. Pruebe el código refactorizado y asegúrese de que la aplicación de demostración de aprobación del préstamo genera los mismos resultados que la implementación original.

## Resumen

En este ejercicio, ha aprendido a usar GitHub Copilot para simplificar la lógica condicional compleja en un código base. Ha explorado el motor de precios de comercio electrónico y las aplicaciones de demostración del flujo de trabajo de aprobación de préstamos, las oportunidades de refactorización identificadas y el agente GitHub Copilot para extraer condicionales complejos en métodos auxiliares más pequeños y centrados. También ha aprendido a reducir los niveles de anidamiento en el código para mejorar la legibilidad al tiempo que mantiene la misma lógica de negocios.

## Limpieza

Ahora que ha terminado el ejercicio, dedique un minuto a asegurarse de que no ha realizado cambios en la cuenta de GitHub ni en la suscripción de GitHub Copilot que no quiere conservar. Si ha realizado algún cambio, reviértalos según sea necesario. Si usa un equipo local como entorno de laboratorio, puede archivar o eliminar la carpeta de proyectos de ejemplo que ha creado para este ejercicio.
