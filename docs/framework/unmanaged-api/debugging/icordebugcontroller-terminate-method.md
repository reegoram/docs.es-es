---
title: "ICorDebugController::Terminate (Método)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugController.Terminate
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugController::Terminate
helpviewer_keywords:
- Terminate method, ICorDebugController interface [.NET Framework debugging]
- ICorDebugController::Terminate method [.NET Framework debugging]
ms.assetid: 4275af0c-b5a7-4e4c-97c9-7e41f36b2dd8
topic_type: apiref
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: fb3831e2640de8ad34299695b571cb4071974bd6
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugcontrollerterminate-method"></a><span data-ttu-id="35b38-102">ICorDebugController::Terminate (Método)</span><span class="sxs-lookup"><span data-stu-id="35b38-102">ICorDebugController::Terminate Method</span></span>
<span data-ttu-id="35b38-103">Finaliza el proceso con el código de salida especificado.</span><span class="sxs-lookup"><span data-stu-id="35b38-103">Terminates the process with the specified exit code.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="35b38-104">Este método es un contenedor de Win32 `TerminateProcess` función.</span><span class="sxs-lookup"><span data-stu-id="35b38-104">This method is a wrapper for the Win32 `TerminateProcess` function.</span></span> <span data-ttu-id="35b38-105">Por lo tanto, `Terminate` utiliza el código de salida de la misma forma en que Win32 `TerminateProcess` función lo usa.</span><span class="sxs-lookup"><span data-stu-id="35b38-105">Thus, `Terminate` uses the exit code in the same way that the Win32 `TerminateProcess` function uses it.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="35b38-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="35b38-106">Syntax</span></span>  
  
```  
HRESULT Terminate (  
    [in] UINT exitCode  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="35b38-107">Parámetros</span><span class="sxs-lookup"><span data-stu-id="35b38-107">Parameters</span></span>  
 `exitCode`  
 <span data-ttu-id="35b38-108">[in] Un valor numérico que es el código de salida.</span><span class="sxs-lookup"><span data-stu-id="35b38-108">[in] A numeric value that is the exit code.</span></span> <span data-ttu-id="35b38-109">Los valores numéricos válidos se definen en Winbase.h.</span><span class="sxs-lookup"><span data-stu-id="35b38-109">The valid numeric values are defined in Winbase.h.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="35b38-110">Comentarios</span><span class="sxs-lookup"><span data-stu-id="35b38-110">Remarks</span></span>  
 <span data-ttu-id="35b38-111">Si el proceso se detiene cuando `Terminate` es llama, el proceso debe continuar usando el [ICorDebugController:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) método para que el depurador reciba confirmación de la finalización a través de la [ ICorDebugManagedCallback:: ExitProcess](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-exitprocess-method.md) o [ICorDebugManagedCallback:: ExitAppDomain](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-exitappdomain-method.md) devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="35b38-111">If the process is stopped when `Terminate` is called, the process should be continued by using the [ICorDebugController::Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) method so that the debugger receives confirmation of the termination through the [ICorDebugManagedCallback::ExitProcess](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-exitprocess-method.md) or [ICorDebugManagedCallback::ExitAppDomain](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-exitappdomain-method.md) callback.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="35b38-112">Este método no se implementa en un dominio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="35b38-112">This method is not implemented by an application domain.</span></span> <span data-ttu-id="35b38-113">Es decir, no se implementa en el <xref:System.AppDomain> nivel.</span><span class="sxs-lookup"><span data-stu-id="35b38-113">That is, it is not implemented at the <xref:System.AppDomain> level.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="35b38-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="35b38-114">Requirements</span></span>  
 <span data-ttu-id="35b38-115">**Plataformas:** vea [requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="35b38-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="35b38-116">**Encabezado:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="35b38-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="35b38-117">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="35b38-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="35b38-118">**Versiones de .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="35b38-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="35b38-119">Vea también</span><span class="sxs-lookup"><span data-stu-id="35b38-119">See Also</span></span>  
 