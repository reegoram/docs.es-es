---
title: Usar comandos de Windows PowerShell en un archivo DockerFile para configurar los contenedores de Windows (Docker estándar según)
description: Ciclo de vida de aplicaciones de Docker en contenedor con la plataforma y las herramientas de Microsoft
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/19/2017
ms.openlocfilehash: d68378a12a16dd4072b381f00241e781b40c3e16
ms.sourcegitcommit: 979597cd8055534b63d2c6ee8322938a27d0c87b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37105555"
---
# <a name="using-windows-powershell-commands-in-a-dockerfile-to-set-up-windows-containers-docker-standard-based"></a>Usar comandos de Windows PowerShell en un archivo DockerFile para configurar los contenedores de Windows (Docker estándar según)

Con [contenedores de Windows](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/about/about_overview), puede convertir las aplicaciones de Windows existentes para las imágenes de Docker e implementarlas con las mismas herramientas que el resto del ecosistema de Docker.

Para utilizar los contenedores de Windows, solo tiene que escribir comandos de Windows PowerShell en el DockerFile, como se muestra en el ejemplo siguiente:

```
FROM microsoft/windowsservercore
LABEL Description="IIS" Vendor="Microsoft" Version="10"
RUN powershell -Command Add-WindowsFeature Web-Server
CMD [ "ping", "localhost", "-t" ]
```

En este caso, vamos a usar Windows PowerShell para instalar una imagen base de Windows Server Core, así como IIS.

De forma similar, también puede usar comandos de Windows PowerShell para configurar componentes adicionales como ASP.NET tradicional 4.x y 4.6 de .NET o cualquier otro software de Windows, como se muestra aquí:

```
RUN powershell add-windowsfeature web-asp-net45
```

>[!div class="step-by-step"]
[Anterior](visual-studio-tools-for-docker.md)
[Siguiente](../docker-devops-workflow/index.md)
