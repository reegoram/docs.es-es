---
title: "ICorProfilerInfo4::InitializeCurrentThread (Método)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo4::InitializeCurrentThread
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo4::InitializeCurrentThread
helpviewer_keywords:
- ICorProfilerInfo4::InitializeCurrentThread method [.NET Framework profiling]
- InitializeCurrentThread method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 18a3335c-8c75-476c-b6de-72c0bfedae5d
topic_type: apiref
caps.latest.revision: "8"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: bc19ae86c266c74097bd649aa96f532528df3d7c
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilerinfo4initializecurrentthread-method"></a><span data-ttu-id="f00dc-102">ICorProfilerInfo4::InitializeCurrentThread (Método)</span><span class="sxs-lookup"><span data-stu-id="f00dc-102">ICorProfilerInfo4::InitializeCurrentThread Method</span></span>
<span data-ttu-id="f00dc-103">Inicializa el subproceso actual antes de generador de perfiles posterior llamadas de API en el mismo subproceso, por lo que se puede evitar que un interbloqueo.</span><span class="sxs-lookup"><span data-stu-id="f00dc-103">Initializes the current thread in advance of subsequent profiler API calls on the same thread, so that deadlock can be avoided.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f00dc-104">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="f00dc-104">Syntax</span></span>  
  
```  
HRESULT InitializeCurrentThread ();  
```  
  
## <a name="remarks"></a><span data-ttu-id="f00dc-105">Comentarios</span><span class="sxs-lookup"><span data-stu-id="f00dc-105">Remarks</span></span>  
 <span data-ttu-id="f00dc-106">Se recomienda llamar a `InitializeCurrentThread` en cualquier subproceso que llama a un generador de perfiles API mientras haya suspendido subprocesos.</span><span class="sxs-lookup"><span data-stu-id="f00dc-106">We recommend that you call `InitializeCurrentThread` on any thread that will call a profiler API while there are suspended threads.</span></span> <span data-ttu-id="f00dc-107">Este método se utiliza normalmente los generadores de perfiles de muestreo que crear sus propios subprocesos para llamar a la [ICorProfilerInfo2:: DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) se explica el método para realizar la pila mientras se suspende el subproceso de destino.</span><span class="sxs-lookup"><span data-stu-id="f00dc-107">This method is typically used by sampling profilers that create their own thread to call the [ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) method to perform stack walks while the target thread is suspended.</span></span> <span data-ttu-id="f00dc-108">Mediante una llamada a `InitializeCurrentThread` una vez cuando el generador de perfiles crea primero el subproceso de muestreo, los generadores de perfiles pueden asegurarse de que la inicialización diferida por cada subproceso que CLR lo contrario se realizaría durante la primera llamada a `DoStackSnapshot` puede llevarse a cabo sin ningún riesgo cuando otros subprocesos no están suspendido.</span><span class="sxs-lookup"><span data-stu-id="f00dc-108">By calling `InitializeCurrentThread` once when the profiler first creates the sampling thread, profilers can ensure that lazy per-thread initialization that the CLR would otherwise perform during the first call to `DoStackSnapshot` can now occur safely when no other threads are suspended.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f00dc-109">`InitializeCurrentThread`realiza la inicialización de antemano para finalizar las tareas que adoptan bloqueos y pueden generar un interbloqueo.</span><span class="sxs-lookup"><span data-stu-id="f00dc-109">`InitializeCurrentThread` does the initialization in advance to finish tasks that take locks, and may deadlock.</span></span> <span data-ttu-id="f00dc-110">Llamar a `InitializeCurrentThread` cuando no haya ningún subproceso suspendido.</span><span class="sxs-lookup"><span data-stu-id="f00dc-110">Call `InitializeCurrentThread` only when there are no suspended threads.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f00dc-111">Requisitos</span><span class="sxs-lookup"><span data-stu-id="f00dc-111">Requirements</span></span>  
 <span data-ttu-id="f00dc-112">**Plataformas:** vea [requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f00dc-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f00dc-113">**Encabezado:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="f00dc-113">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="f00dc-114">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f00dc-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f00dc-115">**Versiones de .NET framework:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f00dc-115">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f00dc-116">Vea también</span><span class="sxs-lookup"><span data-stu-id="f00dc-116">See Also</span></span>  
 [<span data-ttu-id="f00dc-117">ICorProfilerInfo4 (interfaz)</span><span class="sxs-lookup"><span data-stu-id="f00dc-117">ICorProfilerInfo4 Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)  
 [<span data-ttu-id="f00dc-118">Interfaces de generación de perfiles</span><span class="sxs-lookup"><span data-stu-id="f00dc-118">Profiling Interfaces</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [<span data-ttu-id="f00dc-119">Generación de perfiles</span><span class="sxs-lookup"><span data-stu-id="f00dc-119">Profiling</span></span>](../../../../docs/framework/unmanaged-api/profiling/index.md)