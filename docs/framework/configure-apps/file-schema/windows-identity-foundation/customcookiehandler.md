---
title: '&lt;customCookieHandler&gt;'
ms.date: 03/30/2017
ms.assetid: a03b153d-5ec6-4915-9031-6f0c3fd348be
author: BrucePerlerMS
ms.openlocfilehash: 51ca91de5c77727f5f5506118461d19354f12c14
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48029091"
---
# <a name="ltcustomcookiehandlergt"></a>&lt;customCookieHandler&gt;
Establece el tipo de controlador de cookies personalizado. Este elemento solo puede estar presente si el `mode` atributo de la `<cookieHandler>` elemento es "Custom". El tipo personalizado debe derivarse de la <xref:System.IdentityModel.Services.CookieHandler> clase.  
  
 \<system.identityModel.services >  
\<federationConfiguration >  
\<cookieHandler >  
\<customCookieHandler >  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler mode="Custom">  
      <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" >  
      </customCookieHandler>  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|type|Especifica un tipo personalizado que deriva la <xref:System.IdentityModel.Services.CookieHandler> clase. Para obtener más información sobre cómo especificar el `type` atributo, vea [referencias de tipos personalizado](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md).|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguna  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<cookieHandler >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md)|Configura el <xref:System.IdentityModel.Services.CookieHandler> que el <xref:System.IdentityModel.Services.SessionAuthenticationModule> usa para leer y escribir cookies.|  
  
## <a name="remarks"></a>Comentarios  
 Al especificar un controlador de cookies personalizado estableciendo la `mode` atributo de la `<cookieHandler>` elemento en "Custom", debe especificar el tipo del controlador de cookies personalizado mediante la inclusión de un `<customCookieHandler>` elemento secundario que hace referencia al tipo de controlador de cookie. Este elemento no puede ser que se especificó cuando la `mode` atributo está establecido en "Chunked" o "Default". Controladores de cookies personalizado deben derivarse de la <xref:System.IdentityModel.Services.CookieHandler> clase.  
  
 El `<customCookieHandler>` elemento representado por la <xref:System.IdentityModel.Configuration.CustomTypeElement> clase.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente configura el SAM para usar un controlador de cookies personalizado del tipo `MyNamespace.MyCustomCookieHandler`.  
  
```xml  
<cookieHandler mode="Custom">  
    <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" />  
</cookieHandler>  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:System.IdentityModel.Services.CookieHandler>
