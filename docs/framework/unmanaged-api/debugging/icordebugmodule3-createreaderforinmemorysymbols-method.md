---
title: ICorDebugModule3::CreateReaderForInMemorySymbols (Método)
ms.date: 03/30/2017
api_name:
- ICorDebugModule3.CreateReaderForInMemorySymbols
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule3::CreateReaderForInMemorySymbols
helpviewer_keywords:
- CreateReaderForInMemorySymbols method, ICorDebugModule3 interface [.NET Framework debugging]
- ICorDebugModule3::CreateReaderForInMemorySymbols method [.NET Framework debugging]
ms.assetid: af317171-d66d-4114-89eb-063554c74940
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 342739f6c71e9c576e557433dc6abd0adbf38c8c
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43528848"
---
# <a name="icordebugmodule3createreaderforinmemorysymbols-method"></a>ICorDebugModule3::CreateReaderForInMemorySymbols (Método)
Crea un lector de símbolos de depuración para un módulo dinámico.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT CreateReaderForInMemorySymbols (  
      [in] REFIID riid,  
      [out][iid_is(riid)] void **    ppObj  
```  
  
#### <a name="parameters"></a>Parámetros  
 riid  
 [in] IID de la interfaz COM para devolver. Normalmente, esto es un [interfaz ISymUnmanagedReader](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md).  
  
 ppObj  
 [out] Puntero a un puntero a la interfaz devuelta.  
  
## <a name="return-value"></a>Valor devuelto  
 S_OK  
 El lector se creó correctamente.  
  
 CORDBG_E_MODULE_LOADED_FROM_DISK  
 El módulo no es un módulo dinámico o en memoria.  
  
 CORDBG_E_SYMBOLS_NOT_AVAILABLE  
 Símbolos no se hayan especificado por la aplicación o todavía no están disponibles.  
  
 E_FAIL (u otros códigos devueltos de E_)  
 No se puede crear el lector.  
  
## <a name="remarks"></a>Comentarios  
 Este método también puede ser utilizado para crear un objeto de lector de símbolos para los módulos (no dinámicos) en memoria, pero solo después de que los símbolos primero están disponibles (indicado por el [UpdateModuleSymbols (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-updatemodulesymbols-method.md) devolución de llamada).  
  
 Este método devuelve una nueva instancia de lector cada vez que se llama (como [CComPtrBase:: CoCreateInstance](https://msdn.microsoft.com/library/c0965041-6cb6-40c5-b272-2b99f02668a6)). Por lo tanto, el depurador debe almacenar en caché el resultado y solicitar una nueva instancia solo cuando pueden haber cambiado los datos subyacentes (es decir, cuando un [LoadClass (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-loadclass-method.md) se recibe la devolución de llamada).  
  
 Módulos dinámicos no tiene ningún símbolo disponible hasta que se ha cargado el primer tipo (tal y como indica la [LoadClass (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-loadclass-method.md) devolución de llamada).  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Vea [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET framework:** 4.5, 4, 3.5 SP1  
  
## <a name="see-also"></a>Vea también  
 [ICorDebugRemoteTarget (interfaz)](../../../../docs/framework/unmanaged-api/debugging/icordebugremotetarget-interface.md)  
 [ICorDebug (interfaz)](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)  
    
 [Interfaces de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
