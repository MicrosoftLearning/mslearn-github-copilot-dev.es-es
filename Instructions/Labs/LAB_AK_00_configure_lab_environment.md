---
lab:
  title: "Preparación: configuración del entorno de laboratorio para ejercicios de GitHub\_Copilot."
  description: "Revise los requisitos del laboratorio y configure los recursos antes de iniciar los ejercicios de GitHub\_Copilot."
---

# Configuración del entorno de laboratorio para ejercicios de GitHub Copilot

El entorno de laboratorio debe configurarse para el desarrollo de C# mediante Visual Studio Code y GitHub Copilot. Se requiere acceso a una cuenta de GitHub con GitHub Copilot habilitado.

Complete los pasos siguientes para comprobar que el entorno de laboratorio está configurado correctamente:

1. Compruebe que la versión 2.48 o posterior de Git esté instalada en el entorno de laboratorio.

    Ejecute el siguiente comando en una ventana de terminal para comprobar la versión instalada de Git:

    ```bash
    git --version
    ```

    Si ejecuta Windows y desea actualizar Git, puede usar el siguiente comando:

    ```bash
    git update-git-for-windows
    ```

    Si es necesario, puede descargar Git mediante la siguiente dirección URL: <a href="https://git-scm.com/downloads" target="_blank">Descargar Git</a>.

1. Compruebe que la versión más reciente de LTS o STS del SDK de .NET esté instalada en el entorno de laboratorio.

    Ejecute el comando siguiente en una ventana de terminal para comprobar la versión instalada del SDK de .NET:

    ```dotnetcli
    dotnet --version
    ```

    Si es necesario, puede descargar el SDK de .NET mediante la siguiente dirección URL: <a href="https://dotnet.microsoft.com/download/dotnet" target="_blank">Descargue el SDK de .NET</a>.

1. Compruebe que Visual Studio Code y la extensión del Kit de desarrollo de C# están instaladas en el entorno de laboratorio.

    Si es necesario, puede descargar Visual Studio Code mediante la siguiente dirección URL: <a href="https://code.visualstudio.com/download" target="_blank">Descarga de Visual Studio Code</a>

    Puede instalar la extensión del Kit de desarrollo de C# mediante la vista Extensiones de Visual Studio Code.

1. Compruebe que tiene acceso a una cuenta de GitHub y a una suscripción de GitHub Copilot.

    Puede iniciar sesión en su cuenta de GitHub con la siguiente dirección URL: <a href="https://github.com/login" target="_blank">Inicio de sesión en GitHub</a>.

    Si no tiene una cuenta de GitHub, puede crear una cuenta individual desde la página de inicio de sesión de GitHub. En la página de inicio de sesión, seleccione **Crear una cuenta**.

    Abra la página configuración/perfil de la cuenta de GitHub y compruebe que tiene acceso a una suscripción de GitHub Copilot. Si tiene una suscripción activa para GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise que puede usar para el entrenamiento, puede usar la suscripción de GitHub Copilot existente para completar los ejercicios de GitHub Copilot.

    Si tiene una cuenta de GitHub individual, pero no tiene una suscripción a GitHub Copilot, puede configurar un plan gratuito de GitHub Copilot desde Visual Studio Code durante un ejercicio de entrenamiento.

    > **IMPORTANTE**: El plan gratuito de GitHub Copilot es una versión limitada de GitHub Copilot, lo que permite hasta 2000 finalizaciones de código y 50 chats o solicitudes premium al mes. Si usa un plan gratuito de GitHub Copilot fuera de los ejercicios de entrenamiento, puede superar los límites de recursos del plan antes de completar el entrenamiento. El plan gratuito de GitHub Copilot no está disponible para las suscripciones de GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business o GitHub Copilot Enterprise.
