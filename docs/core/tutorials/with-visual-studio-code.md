---
title: 'Introducción a C# y Visual Studio Code: Guía de C#'
description: Obtenga información sobre cómo crear y depurar su primera aplicación .NET Core en C# mediante Visual Studio Code.
author: kendrahavens
ms.author: mairaw
ms.date: 09/27/2017
ms.openlocfilehash: 321edcebdea141b7290fa57b47c8d9fc91d3521c
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2018
ms.locfileid: "45668228"
---
# <a name="get-started-with-c-and-visual-studio-code"></a>Introducción a C# y Visual Studio Code

.NET Core ofrece una plataforma modular y rápida para crear aplicaciones que se ejecutan en Windows, Linux y macOS. Use Visual Studio Code con la extensión de C# para disfrutar de una sólida experiencia de edición con compatibilidad total para C# IntelliSense (completado de código inteligente) y para depuración.

## <a name="prerequisites"></a>Requisitos previos

1. Instale [Visual Studio Code](https://code.visualstudio.com/).
2. Instale el [SDK de .NET Core](https://www.microsoft.com/net/download/core).
3. Instale la [extensión de C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) para Visual Studio Code. Para más información sobre cómo instalar extensiones en Visual Studio Code, vea el [Marketplace de extensiones de VS Code](https://code.visualstudio.com/docs/editor/extension-gallery).

## <a name="hello-world"></a>Hello World

Se va a empezar con un programa "Hola mundo" sencillo basado en .NET Core:

1. Abrir un proyecto:

    * Abra Visual Studio Code.
    * Haga clic en el icono del explorador en el menú de la izquierda y después haga clic en **Abrir carpeta**.
    * Seleccione **Archivo** > **Abrir carpeta** en el menú principal para abrir la carpeta en la que quiere que esté el proyecto de C# y haga clic en **Seleccionar carpeta**. En el ejemplo se va a crear una carpeta para el proyecto denominada *HelloWorld*.

      ![VSCodeOpenFolder](media/with-visual-studio-code/vscodeopenfolder.png)

2. Inicializar un proyecto de C#:
    * Abra el terminal integrado de Visual Studio Code al seleccionar **Ver** > **Terminal integrado** en el menú principal.
    * En la ventana de terminal, escriba `dotnet new console`.
    * Este comando crea un archivo `Program.cs` en la carpeta con un programa "Hello World" sencillo ya escrito, junto con un archivo de proyecto de C# denominado `HelloWorld.csproj`.

      ![El nuevo comando de dotnet](media/with-visual-studio-code/dotnetnew.png)

3. Resolver los recursos de compilación:

    * En **.NET Core 1.x**, escriba `dotnet restore`. Al ejecutar `dotnet restore`, se concede acceso a los paquetes de .NET Core necesarios para compilar el proyecto.

      ![El comando de restauración de dotnet](media/with-visual-studio-code/dotnetrestore.png)

      [!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

4. Ejecutar el programa "Hola mundo":

    * Escriba `dotnet run`.

      ![El comando de ejecución de dotnet](media/with-visual-studio-code/dotnetrun.png)

También puede ver un breve tutorial de vídeo para obtener ayuda del programa de instalación en [Windows](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core), [macOS](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core-on-MacOS) o [Linux](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu).

## <a name="debug"></a>Depuración

1. Haga clic en el archivo *Program.cs* para abrirlo. La primera vez que se abre un archivo de C# en Visual Studio Code, se carga [OmniSharp](http://www.omnisharp.net/) en el editor.

    ![Abrir el archivo Program.cs](media/with-visual-studio-code/opencs.png)

2. Visual Studio Code debe pedirle que agregue los recursos que faltan para compilar y depurar la aplicación. Seleccione **Sí**.

    ![Solicitud de los recursos que faltan](media/with-visual-studio-code/missing-assets.png)

3. Para abrir la vista Depurar, haga clic en el icono de depuración en el menú de la izquierda.

    ![Abrir la pestaña Depurar](media/with-visual-studio-code/opendebug.png)

4. Busque la flecha verde en la parte superior del panel. Asegúrese de que `.NET Core Launch (console)` está seleccionado en el menú desplegable que está junto a la flecha.

    ![Selección de .NET Core](media/with-visual-studio-code/selectcore.png)

5. Agregue un punto de interrupción al proyecto; para ello, haga clic en el **margen del editor**, que es el espacio a la izquierda de los números de línea del editor, junto a la línea 9 o mueva el cursor del texto de la línea 9 en el editor y presione <kbd>F9</kbd>.

    ![Establecer un punto de interrupción](media/with-visual-studio-code/setbreakpoint.png)

6. Para comenzar a depurar, seleccione <kbd>F5</kbd> o la flecha verde. El depurador detiene la ejecución del programa cuando alcanza el punto de interrupción establecido en el paso anterior.
    * Mientras depura, puede ver las variables locales en el panel superior izquierdo o usar la consola de depuración.

    ![Ejecutar y depurar](media/with-visual-studio-code/rundebug.png)

7. Seleccione la flecha verde en la parte superior para continuar la depuración o seleccione el cuadrado rojo que se encuentra arriba para detenerla.

> [!TIP]
> Para obtener más información y sugerencias sobre solución de problemas en relación con la depuración de .NET Core con OmniSharp en Visual Studio Code, vea [Instructions for setting up the .NET Core debugger](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md) (Instrucciones para configurar el depurador de .NET Core).

## <a name="faq"></a>Preguntas más frecuentes

### <a name="im-missing-required-assets-to-build-and-debug-c-in-visual-studio-code-my-debugger-says-no-configuration"></a>Me faltan los recursos necesarios para compilar y depurar C# en Visual Studio Code. Mi depurador dice "Sin configuración".

La extensión C# de Visual Studio Code puede generar recursos para compilar y depurar por usted. Visual Studio Code le pedirá que genere estos recursos al abrir un proyecto de C#. Aunque no genere los recursos, podrá seguir ejecutando este comando abriendo la paleta de comandos (**Vista > Paleta de comandos**) y escribiendo ">.NET: Generate Assets for Build and Debug". Al seleccionar esta opción se generan los archivos de configuración .vscode, launch.json y tasks.json que necesita.

## <a name="see-also"></a>Vea también

* [Setting up Visual Studio Code](https://code.visualstudio.com/docs/setup/setup-overview) (Configuración de Visual Studio Code)
* [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging) (Depuración en Visual Studio Code)
