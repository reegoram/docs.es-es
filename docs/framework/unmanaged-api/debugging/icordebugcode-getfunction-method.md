---
title: "ICorDebugCode::GetFunction (Método)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugCode.GetFunction
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugCode::GetFunction
helpviewer_keywords:
- GetFunction method, ICorDebugCode interface [.NET Framework debugging]
- ICorDebugCode::GetFunction method [.NET Framework debugging]
ms.assetid: c568b737-fdb2-4816-accd-051f5ab760f1
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 0304eaadec5805b1ded9a4cbfe79959c3e18a344
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugcodegetfunction-method"></a><span data-ttu-id="1226e-102">ICorDebugCode::GetFunction (Método)</span><span class="sxs-lookup"><span data-stu-id="1226e-102">ICorDebugCode::GetFunction Method</span></span>
<span data-ttu-id="1226e-103">Obtiene la "ICorDebugFunction" asociado "ICorDebugCode".</span><span class="sxs-lookup"><span data-stu-id="1226e-103">Gets the "ICorDebugFunction" associated with this "ICorDebugCode".</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1226e-104">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="1226e-104">Syntax</span></span>  
  
```  
HRESULT GetFunction (  
    [out] ICorDebugFunction **ppFunction  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="1226e-105">Parámetros</span><span class="sxs-lookup"><span data-stu-id="1226e-105">Parameters</span></span>  
 `ppFunction`  
 <span data-ttu-id="1226e-106">[out] Un puntero a la dirección de la función.</span><span class="sxs-lookup"><span data-stu-id="1226e-106">[out] A pointer to the address of the function.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="1226e-107">Comentarios</span><span class="sxs-lookup"><span data-stu-id="1226e-107">Remarks</span></span>  
 <span data-ttu-id="1226e-108">`ICorDebugCode`y `ICorDebugFunction` mantienen una relación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="1226e-108">`ICorDebugCode` and `ICorDebugFunction` maintain a one-to-one relationship.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="1226e-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="1226e-109">Requirements</span></span>  
 <span data-ttu-id="1226e-110">**Plataformas:** vea [requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="1226e-110">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1226e-111">**Encabezado:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="1226e-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="1226e-112">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="1226e-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="1226e-113">**Versiones de .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1226e-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1226e-114">Vea también</span><span class="sxs-lookup"><span data-stu-id="1226e-114">See Also</span></span>  
 