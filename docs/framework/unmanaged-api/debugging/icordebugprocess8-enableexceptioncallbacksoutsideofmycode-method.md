---
title: Método de ICorDebugProcess8::EnableExceptionCallbacksOutsideOfMyCode
ms.date: 03/30/2017
dev_langs:
- cpp
ms.assetid: b3af44ec-7d41-425b-aed9-0c4379e5cbe9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5f08f24e16b34d911793b5c8d4a28168f7677b22
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33418973"
---
# <a name="icordebugprocess8enableexceptioncallbacksoutsideofmycode-method"></a>Método de ICorDebugProcess8::EnableExceptionCallbacksOutsideOfMyCode
[compatible con la versión [!INCLUDE[net_v46](../../../../includes/net-v46-md.md)] y posteriores]  
  
 Habilita o deshabilita ciertos tipos de [ICorDebugManagedCallback2](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-interface.md) las devoluciones de llamada de excepción.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
HRESULT EnableExceptionCallbacksOutsideOfMyCode(  
   [in] BOOL enableExceptionsOutsideOfJMC  
);  
```  
  
#### <a name="parameters"></a>Parámetros  
 `enableExceptionsOutsideOfJMC`  
 [in]  
  
## <a name="remarks"></a>Comentarios  
 Si el valor de `enableExceptionsOutsideOfJMC` es `false`:  
  
-   No se producirá una excepción DEBUG_EXCEPTION_FIRST_CHANCE una devolución de llamada al depurador.  
  
-   Una excepción DEBUG_EXCEPTION_CATCH_HANDLER_FOUND no generará una devolución de llamada al depurador si la excepción nunca se convierte en código de usuario (es decir, la ruta de acceso de origen a un controlador de excepciones no tiene métodos marcados como JustMyCode o JMC).  
  
 El valor predeterminado de `enableExceptionsOutsideOfJMC` es `true`.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** vea [requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET framework:** [!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [ICorDebugProcess8 (interfaz)](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess8-interface.md)  
 [Interfaces de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
