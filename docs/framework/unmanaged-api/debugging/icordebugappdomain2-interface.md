---
title: ICorDebugAppDomain2 Interfaz1
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugAppDomain2
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugAppDomain2
helpviewer_keywords: ICorDebugAppDomain2 interface [.NET Framework debugging]
ms.assetid: 314d29f3-feb0-4a92-9530-b569c280cc31
topic_type: apiref
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: ebd1e504cbf2f74ad82e7fea6b6c3f355a1bda34
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugappdomain2-interface1"></a><span data-ttu-id="427b8-102">ICorDebugAppDomain2 Interfaz1</span><span class="sxs-lookup"><span data-stu-id="427b8-102">ICorDebugAppDomain2 Interface1</span></span>
<span data-ttu-id="427b8-103">Proporciona métodos para trabajar con matrices, punteros, punteros a función y tipos de referencia.</span><span class="sxs-lookup"><span data-stu-id="427b8-103">Provides methods to work with arrays, pointers, function pointers, and reference types.</span></span> <span data-ttu-id="427b8-104">Esta interfaz es una extensión de ICorDebugAppDomain (interfaz).</span><span class="sxs-lookup"><span data-stu-id="427b8-104">This interface is an extension of the ICorDebugAppDomain interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="427b8-105">Métodos</span><span class="sxs-lookup"><span data-stu-id="427b8-105">Methods</span></span>  
  
|<span data-ttu-id="427b8-106">Método</span><span class="sxs-lookup"><span data-stu-id="427b8-106">Method</span></span>|<span data-ttu-id="427b8-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="427b8-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="427b8-108">GetArrayOrPointerType (método)</span><span class="sxs-lookup"><span data-stu-id="427b8-108">GetArrayOrPointerType Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain2-getarrayorpointertype-method.md)|<span data-ttu-id="427b8-109">Obtiene una matriz del tipo especificado, o un puntero o referencia al tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="427b8-109">Gets an array of the specified type, or a pointer or reference to the specified type.</span></span>|  
|[<span data-ttu-id="427b8-110">GetFunctionPointerType</span><span class="sxs-lookup"><span data-stu-id="427b8-110">GetFunctionPointerType</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain2-getfunctionpointertype-method.md)|<span data-ttu-id="427b8-111">Obtiene un puntero a una función que tiene una firma dada.</span><span class="sxs-lookup"><span data-stu-id="427b8-111">Gets a pointer to a function that has a given signature.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="427b8-112">Comentarios</span><span class="sxs-lookup"><span data-stu-id="427b8-112">Remarks</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="427b8-113">Esta interfaz no admite que se la llame de forma remota, ya sea entre procesos o entre equipos.</span><span class="sxs-lookup"><span data-stu-id="427b8-113">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="427b8-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="427b8-114">Requirements</span></span>  
 <span data-ttu-id="427b8-115">**Plataformas:** vea [requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="427b8-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="427b8-116">**Encabezado:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="427b8-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="427b8-117">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="427b8-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="427b8-118">**Versiones de .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="427b8-118">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="427b8-119">Vea también</span><span class="sxs-lookup"><span data-stu-id="427b8-119">See Also</span></span>  
 [<span data-ttu-id="427b8-120">Interfaces de depuración</span><span class="sxs-lookup"><span data-stu-id="427b8-120">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)