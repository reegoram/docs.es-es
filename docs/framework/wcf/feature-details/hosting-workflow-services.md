---
title: Hospedar servicios de flujo de trabajo
ms.date: 03/30/2017
ms.assetid: 2d55217e-8697-4113-94ce-10b60863342e
ms.openlocfilehash: f75b8cc4cde0372b995c39a5da3ae4b71590743e
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43505551"
---
# <a name="hosting-workflow-services"></a>Hospedar servicios de flujo de trabajo
Debe hospedarse un servicio del flujo de trabajo para que responda a los mensajes entrantes. Los servicios del flujo de trabajo usan la infraestructura de mensajería de WCF y, por lo tanto, se hospedan de maneras similares. Como los servicios WCF, servicios de flujo de trabajo se pueden hospedar en cualquier aplicación administrada, en Internet Information Services (IIS) o en Windows Process Activation Services (WAS). Además, los servicios de flujo de trabajo pueden hospedarse en Windows Server App Fabric. Para obtener más información acerca de Windows Server App Fabric, consulte [documentación de Windows Server App Fabric](https://go.microsoft.com/fwlink/?LinkId=193037), [AppFabric Hosting Features](https://go.microsoft.com/fwlink/?LinkId=196494), y [conceptos de hospedaje de AppFabric](https://go.microsoft.com/fwlink/?LinkId=196495). Para obtener más información sobre las diversas maneras de hospedaje de WCF los servicios, consulte [servicios de hospedaje](../../../../docs/framework/wcf/hosting-services.md).

## <a name="hosting-in-a-managed-application"></a>Hospedar en una aplicación administrada
 Para hospedar un servicio de flujo de trabajo en una aplicación administrada, use la clase <xref:System.ServiceModel.Activities.WorkflowServiceHost>. El constructor <xref:System.ServiceModel.Activities.WorkflowServiceHost> le permite especificar una instancia de servicio del flujo de trabajo singleton, una definición del servicio de flujo de trabajo o una actividad que usa las actividades de mensajería de flujo de trabajo. Una llamada a <<!--zz xref:System.ServiceModel.Activities.WorkflowServiceHost.Open%2A--> `System.ServiceModel.Activities.WorkflowServiceHost.Open`> hace que el servicio empiece a escuchar los mensajes entrantes.

## <a name="hosting-under-iis-or-was"></a>Hospedar en IIS o WAS
 Hospedar un servicio de flujo de trabajo en IIS o FUE implica la creación de un directorio virtual y la colocación de archivos en el directorio virtual para definir el servicio y su comportamiento. Al hospedar un servicio de flujo de trabajo en IIS o WAS, existen varias posibilidades:

-   Coloque un archivo .xamlx que defina el servicio de flujo de trabajo en un directorio virtual de IIS/WAS junto con un archivo Web.config que especifique los comportamientos del servicio, los extremos y otros elementos de configuración.

-   Coloque en un directorio virtual de IIS/WAS un archivo .xamlx que defina el servicio del flujo de trabajo. El archivo .xamlx especifica los extremos que se van a exponer. Los extremos se especifican en un elemento `WorkflowService.Endpoints`, como se muestra en el siguiente ejemplo.

    ```xml
    <WorkflowService xmlns="http://schemas.microsoft.com/netfx/2009/xaml/servicemodel"  xmlns:p1="http://schemas.microsoft.com/netfx/2009/xaml/activities" xmlns:sad="clr-namespace:System.Activities.Debugger;assembly=System.Activities" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
      <WorkflowService.Endpoints>
        <Endpoint ServiceContractName="IWorkFlowEchoService" AddressUri="">
          <Endpoint.Binding>
            <BasicHttpBinding />
          </Endpoint.Binding>
        </Endpoint>
      </WorkflowService.Endpoints>
    <!-- ... -->
    </WorkflowService>
    ```

    > [!NOTE]
    > Los comportamientos no se pueden especificar en un archivo .xamlx, de modo que debe usar un archivo Web.config si necesita especificar la configuración del comportamiento.

-   Coloque en un directorio virtual de IIS/WAS un archivo .xamlx que defina el servicio del flujo de trabajo. Además, coloque un archivo .svc en el directorio virtual. El archivo .svc le permite especificar un generador de host de servicio Web personalizado, aplicar el comportamiento personalizado o cargar la configuración desde una ubicación personalizada.

-   Coloque en el directorio virtual de IIS/WAS un ensamblado que contenga una actividad que use las actividades de mensajería de WF.

 Un archivo .xamlx que define un servicio de flujo de trabajo debe contener un <`Service`> elemento raíz o un elemento raíz que contiene cualquier tipo derivado de <xref:System.Workflow.ComponentModel.Activity>. Cuando se usa la plantilla de actividad de Visual Studio, se crea un archivo .xamlx. Cuando se usa la plantilla de servicio de flujo de trabajo de WCF, se crea un archivo .xamlx.

## <a name="hosting-workflow-services-under-windows-server-app-fabric"></a>Hospedar servicios de flujo de trabajo en Windows Server App Fabric
 El hospedaje de un servicio de flujo de trabajo en Windows Server App Fabric se realiza del mismo modo que el hospedaje en IIS/WAS. La única diferencia es el hecho de que Windows Server App Fabric se instala. Windows Server App Fabric proporciona herramientas que se agregan al Administrador de Internet Information Services, además de los commandlets de PowerShell. Estas herramientas simplifican la implementación, la administración y el seguimiento de los servicios de flujo de trabajo y los servicios WCF.

## <a name="referencing-custom-activities"></a>Hacer referencia a actividades personalizadas
 Las referencias a las actividades personalizadas deben agregarse a la <`Assemblies`> en la sección <`System.Web.Compilation`> para que se carguen en el dominio de aplicación y el deserializador XAML puedo buscar los tipos. Esta configuración se puede realizar en el nivel de la aplicación o en el archivo Web.config de la raíz si la configuración se debe aplicar a todas las aplicaciones del equipo.

## <a name="deployment"></a>Implementación
 La herramienta de implementación web se ha creado para facilitar el trabajo de implementación. La herramienta le permite migrar las aplicaciones entre IIS 6.0 e IIS 7.0, sincronizar las granjas de servidores y empaquetar, archivar e implementar las aplicaciones web. Para obtener más información, consulte [herramienta de implementación de MS](https://go.microsoft.com/fwlink/?LinkId=178690).

## <a name="see-also"></a>Vea también

- [Información interna de extensiones del host de servicio de flujo de trabajo](../../../../docs/framework/wcf/feature-details/workflow-service-host-internals.md)
- [Configuración de WorkflowServiceHost](../../../../docs/framework/wcf/feature-details/configuring-workflowservicehost.md)