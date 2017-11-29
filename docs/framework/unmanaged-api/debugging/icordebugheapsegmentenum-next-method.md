---
title: "ICorDebugHeapSegmentEnum::Next (Método)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: Next
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugHeapSegmentEnum::Next
helpviewer_keywords:
- ICorDebugHeapSegmentEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugHeapSegmentEnum interface [.NET Framework debugging]
ms.assetid: 51625fd0-7399-49c7-b22b-5dfb05451fe6
topic_type: apiref
caps.latest.revision: "6"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 655bc404003c4af3aa2ba934ee192b378caf2f2e
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugheapsegmentenumnext-method"></a><span data-ttu-id="40496-102">ICorDebugHeapSegmentEnum::Next (Método)</span><span class="sxs-lookup"><span data-stu-id="40496-102">ICorDebugHeapSegmentEnum::Next Method</span></span>
<span data-ttu-id="40496-103">Obtiene el número especificado de [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) instancias que contienen información acerca de las áreas de memoria del montón administrado.</span><span class="sxs-lookup"><span data-stu-id="40496-103">Gets the specified number of [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) instances that contain information about memory regions of the managed heap.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="40496-104">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="40496-104">Syntax</span></span>  
  
```  
HRESULT Next(  
    [in] ULONG celt,    [out, size_is(celt), length_is(*pceltFetched)] COR_SEGMENT segments[],   
    [out] ULONG *pceltFetched  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="40496-105">Parámetros</span><span class="sxs-lookup"><span data-stu-id="40496-105">Parameters</span></span>  
 <span data-ttu-id="40496-106">celt</span><span class="sxs-lookup"><span data-stu-id="40496-106">celt</span></span>  
 <span data-ttu-id="40496-107">[in] El número de segmentos que va a recuperar.</span><span class="sxs-lookup"><span data-stu-id="40496-107">[in] The number of segments to be retrieved.</span></span>  
  
 <span data-ttu-id="40496-108">segmentos</span><span class="sxs-lookup"><span data-stu-id="40496-108">segments</span></span>  
 <span data-ttu-id="40496-109">[out] Una matriz de punteros, cada uno de los cuales señala a un [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) objeto que proporciona información sobre una región de memoria en el montón administrado.</span><span class="sxs-lookup"><span data-stu-id="40496-109">[out] An array of pointers, each of which points to a [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) object that provides information about a region of memory in the managed heap.</span></span>  
  
 <span data-ttu-id="40496-110">pceltFetched</span><span class="sxs-lookup"><span data-stu-id="40496-110">pceltFetched</span></span>  
 <span data-ttu-id="40496-111">[out] Un puntero al número de [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) objetos realmente devueltos en `segments`.</span><span class="sxs-lookup"><span data-stu-id="40496-111">[out] A pointer to the number of [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) objects actually returned in `segments`.</span></span> <span data-ttu-id="40496-112">Este valor puede ser `null` si `celt` es 1.</span><span class="sxs-lookup"><span data-stu-id="40496-112">This value may be `null` if `celt` is 1.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="40496-113">Comentarios</span><span class="sxs-lookup"><span data-stu-id="40496-113">Remarks</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="40496-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="40496-114">Requirements</span></span>  
 <span data-ttu-id="40496-115">**Plataformas:** vea [requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="40496-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="40496-116">**Encabezado:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="40496-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="40496-117">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="40496-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="40496-118">**Versiones de .NET framework:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="40496-118">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="40496-119">Vea también</span><span class="sxs-lookup"><span data-stu-id="40496-119">See Also</span></span>  
 [<span data-ttu-id="40496-120">ICorDebugHeapSegmentEnum (interfaz)</span><span class="sxs-lookup"><span data-stu-id="40496-120">ICorDebugHeapSegmentEnum Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugheapsegmentenum-interface.md)  
 [<span data-ttu-id="40496-121">Interfaces de depuración</span><span class="sxs-lookup"><span data-stu-id="40496-121">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)