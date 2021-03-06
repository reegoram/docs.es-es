---
title: Usar Azure Key Vault para proteger secretos en tiempo de producción
description: Arquitectura de microservicios de .NET para aplicaciones .NET en contenedor | Usar Azure Key Vault para proteger secretos en tiempo de producción
author: mjrousos
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: 5738b81c90c886aff48451742881807dc09a9ff9
ms.sourcegitcommit: a885cc8c3e444ca6471348893d5373c6e9e49a47
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43863992"
---
# <a name="using-azure-key-vault-to-protect-secrets-at-production-time"></a>Usar Azure Key Vault para proteger secretos en tiempo de producción

Los secretos almacenados como variables de entorno o almacenados por la herramienta Administrador de secretos todavía se almacenan localmente y se descifran en el equipo. Una opción más segura para almacenar secretos es [Azure Key Vault](https://azure.microsoft.com/services/key-vault/), que proporciona una ubicación central y segura para almacenar claves y secretos.

El paquete Microsoft.Extensions.Configuration.AzureKeyVault permite que una aplicación de ASP.NET Core lea información de configuración de Azure Key Vault. Siga estos pasos para empezar a usar secretos de Azure Key Vault:

En primer lugar, registre la aplicación como una aplicación de Azure AD (el acceso a los almacenes de claves se administra mediante Azure AD). Puede hacerlo a través del portal de administración de Azure.

Como alternativa, si quiere que la aplicación se autentique mediante un certificado en lugar de hacerlo con una contraseña o un secreto de cliente, puede usar el cmdlet de PowerShell [New-AzureRmADApplication](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermadapplication). El certificado que registre en Azure Key Vault solo necesita su clave pública (la aplicación usará la clave privada).

En segundo lugar, conceda a la aplicación registrada acceso al almacén de claves creando una entidad de servicio. Puede hacerlo usando los siguientes comandos de PowerShell:

```powershell
$sp = New-AzureRmADServicePrincipal -ApplicationId "<Application ID guid>"
Set-AzureRmKeyVaultAccessPolicy -VaultName "<VaultName>" -ServicePrincipalName $sp.ServicePrincipalNames[0] -PermissionsToSecrets all -ResourceGroupName "<KeyVault Resource Group>"
```

En tercer lugar, incluya el almacén de claves como origen de configuración en la aplicación llamando al método de extensión IConfigurationBuilder.AddAzureKeyVault cuando cree una instancia de IConfigurationRoot. Tenga en cuenta que, al llamar a AddAzureKeyVault, necesitará el Id. de la aplicación registrada y a la que se concedió acceso al almacén de claves en los pasos anteriores.

  Actualmente, .NET Standard y .NET Core admiten la obtención de información de configuración de Azure Key Vault mediante un identificador de cliente y un secreto de cliente. Las aplicaciones de .NET Framework pueden usar una sobrecarga de IConfigurationBuilder.AddAzureKeyVault que toma un certificado en lugar del secreto de cliente. En el momento en el que se redactó este documento, [se estaba trabajando](https://github.com/aspnet/Configuration/issues/605) para que esa sobrecarga estuviera disponible en .NET Standard y .NET Core. Mientras la sobrecarga de AddAzureKeyVault que acepta un certificado no está disponible, las aplicaciones de ASP.NET Core pueden obtener acceso a un Azure Key Vault con una autenticación basada en certificados creando de manera explícita un objeto KeyVaultClient, como se muestra en el ejemplo siguiente:

```csharp
// Configure Key Vault client
var kvClient = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(async
    (authority, resource, scope) =>
    {
        var cert = // Get certificate from local store/file/key vault etc. as needed
        // From the Microsoft.IdentityModel.Clients.ActiveDirectory pacakge
        var authContext = new AuthenticationContext(authority,
            TokenCache.DefaultShared);
        var result = await authContext.AcquireTokenAsync(resource,
            // From the Microsoft.Rest.ClientRuntime.Azure.Authentication pacakge
            new ClientAssertionCertificate("{Application ID}", cert));
        return result.AccessToken;
    }));

    // Get configuration values from Key Vault
    var builder = new ConfigurationBuilder()
        .SetBasePath(env.ContentRootPath)
        // Other configuration providers go here.
        .AddAzureKeyVault("{KeyValueUri}", kvClient,
        new DefaultKeyVaultSecretManager());
```

En este ejemplo, la llamada a AddAzureKeyVault se incluye al final del registro del proveedor de configuración. Como procedimiento recomendado puede registrar Azure Key Vault como el último proveedor de configuración para que pueda reemplazar los valores de configuración de los proveedores anteriores, de modo que ningún valor de configuración de otros orígenes reemplace los del almacén de claves.

## <a name="additional-resources"></a>Recursos adicionales

-   **Using Azure Key Vault to protect application secrets (Usar Azure Key Vault para proteger secretos de aplicaciones)**
    [*https://docs.microsoft.com/azure/guidance/guidance-multitenant-identity-keyvault*](https://docs.microsoft.com/azure/guidance/guidance-multitenant-identity-keyvault)

-   **Safe storage of app secrets during development (Almacenamiento seguro de secretos de aplicación durante el desarrollo)**
    [*https://docs.microsoft.com/aspnet/core/security/app-secrets*](https://docs.microsoft.com/aspnet/core/security/app-secrets)

-   **Configuring data protection (Configuración de la protección de datos)**
    [*https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/overview*](https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/overview)

-   **Key management and lifetime**
    [*https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/default-settings\#data-protection-default-settings*](https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/default-settings#data-protection-default-settings) (Administración y duración de las claves)

-   Repositorio de GitHub **Microsoft.Extensions.Configuration.KeyPerFile**.
    [*https://github.com/aspnet/Configuration/tree/master/src/Config.KeyPerFile*](https://github.com/aspnet/Configuration/tree/master/src/Config.KeyPerFile)

>[!div class="step-by-step"]
[Anterior](developer-app-secrets-storage.md)
[Siguiente](../key-takeaways.md)
