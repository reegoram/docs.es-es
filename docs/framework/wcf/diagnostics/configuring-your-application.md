---
title: Configuración de su aplicación
ms.date: 03/30/2017
ms.assetid: a2f995b0-669d-4721-b00f-4561ec7eb6a4
ms.openlocfilehash: e06c428526c5383c6908521075cd2eca977ce89f
ms.sourcegitcommit: efff8f331fd9467f093f8ab8d23a203d6ecb5b60
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2018
ms.locfileid: "43481241"
---
# <a name="configuring-your-application"></a>Configuración de su aplicación
Windows Communication Foundation (WCF) utiliza el sistema de configuración de .NET y le permite configurar los servicios en el ámbito de equipo y aplicación.  
  
 Opciones de configuración definidas por WCF se encuentran en el `<system.serviceModel>` grupo de sección. Para obtener más información acerca de cómo configurar un servicio WCF, vea los temas siguientes:  
  
-   [Configuración de servicios](../../../../docs/framework/wcf/configuring-services.md)  
  
-   [\<system.serviceModel>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)  
  
 Los valores de configuración definidos por la aplicación se definen en el grupo de la sección `<appSettings>`. Para obtener más información acerca de la configuración de la aplicación en los archivos de configuración. NET, consulte [ \<appSettings >](https://go.microsoft.com/fwlink/?LinkId=95159).  
  
## <a name="using-the-configuration-editor"></a>Utilización del editor de configuración  
 WCF[Configuration Editor Tool (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) permite a los administradores y programadores crear y modificar valores de configuración para los servicios WCF mediante una interfaz gráfica de usuario. Con esta herramienta, puede administrar la configuración de enlaces, comportamientos, servicios y diagnósticos de WCF sin editar directamente los archivos de configuración XML.  
  
## <a name="editing-configuration-files-in-visual-studio"></a>Edición de los archivos de configuración en Visual Studio  
 Para editar el archivo de configuración de un proyecto de servicio WCF en Visual Studio, haga clic en **el Explorador de soluciones** y elija el **Editar configuración de WCF** elemento de menú contextual. Esto inicia el [Configuration Editor Tool (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md).  
  
> [!NOTE]
>  Si edita el archivo de configuración de un proyecto de servicio Web de WCF en Visual Studio con el botón secundario en **el Explorador de soluciones**, tenga en cuenta que el **Editar configuración de WCF** falta el elemento de menú contextual. Para solucionar este problema, haga clic en el **herramientas** menú y elija **Editor de configuración del servicio de WCF**. Después de eso, puede haga clic en un archivo de configuración y usar el **Editar configuración de WCF** elemento de menú contextual.  
  
## <a name="see-also"></a>Vea también  
 [Herramienta del editor de configuración (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)  
 [Configuración de servicios](../../../../docs/framework/wcf/configuring-services.md)  
 [\<system.serviceModel>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)
