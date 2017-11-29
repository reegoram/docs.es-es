---
title: ICLRDataEnumMemoryRegionsCallback (Interfaz)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICLRDataEnumMemoryRegionsCallback
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICLRDataEnumMemoryRegionsCallback
helpviewer_keywords: ICLRDataEnumMemoryRegionsCallback interface [.NET Framework debugging]
ms.assetid: 3f1af8b0-8478-48e0-a7ec-3e90e0b97649
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 40e51bfc176d8be6b008bc4274c0933253d7be3a
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2017
---
# <a name="iclrdataenummemoryregionscallback-interface"></a><span data-ttu-id="f7d01-102">ICLRDataEnumMemoryRegionsCallback (Interfaz)</span><span class="sxs-lookup"><span data-stu-id="f7d01-102">ICLRDataEnumMemoryRegionsCallback Interface</span></span>
<span data-ttu-id="f7d01-103">Proporciona un método de devolución de llamada para [ICLRDataEnumMemoryRegions:: EnumMemoryRegions](../../../../docs/framework/unmanaged-api/debugging/iclrdataenummemoryregions-enummemoryregions-method.md) para notificar al depurador el resultado de un intento de enumerar un área especificada de memoria.</span><span class="sxs-lookup"><span data-stu-id="f7d01-103">Provides a callback method for [ICLRDataEnumMemoryRegions::EnumMemoryRegions](../../../../docs/framework/unmanaged-api/debugging/iclrdataenummemoryregions-enummemoryregions-method.md) to report to the debugger the result of an attempt to enumerate a specified region of memory.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="f7d01-104">Métodos</span><span class="sxs-lookup"><span data-stu-id="f7d01-104">Methods</span></span>  
  
|<span data-ttu-id="f7d01-105">Método</span><span class="sxs-lookup"><span data-stu-id="f7d01-105">Method</span></span>|<span data-ttu-id="f7d01-106">Descripción</span><span class="sxs-lookup"><span data-stu-id="f7d01-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="f7d01-107">EnumMemoryRegion (método)</span><span class="sxs-lookup"><span data-stu-id="f7d01-107">EnumMemoryRegion Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/iclrdataenummemoryregionscallback-enummemoryregion-method.md)|<span data-ttu-id="f7d01-108">Llamado por el método `ICLRDataEnumMemoryRegions::EnumMemoryRegions` para notificar al depurador el resultado de un intento de enumerar un área especificada de memoria.</span><span class="sxs-lookup"><span data-stu-id="f7d01-108">Called by `ICLRDataEnumMemoryRegions::EnumMemoryRegions` to report to the debugger the result of an attempt to enumerate a specified region of memory.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="f7d01-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="f7d01-109">Requirements</span></span>  
 <span data-ttu-id="f7d01-110">**Plataformas:** vea [requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f7d01-110">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f7d01-111">**Encabezado:** ClrData.idl, ClrData.h</span><span class="sxs-lookup"><span data-stu-id="f7d01-111">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="f7d01-112">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f7d01-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f7d01-113">**Versiones de .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f7d01-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f7d01-114">Vea también</span><span class="sxs-lookup"><span data-stu-id="f7d01-114">See Also</span></span>  
 [<span data-ttu-id="f7d01-115">Interfaces de depuración</span><span class="sxs-lookup"><span data-stu-id="f7d01-115">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)