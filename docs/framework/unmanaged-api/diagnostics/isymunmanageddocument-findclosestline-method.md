---
title: "ISymUnmanagedDocument::FindClosestLine (Método)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ISymUnmanagedDocument.FindClosestLine
api_location: diasymreader.dll
api_type: COM
f1_keywords: ISymUnmanagedDocument::FindClosestLine
helpviewer_keywords:
- FindClosestLine method [.NET Framework debugging]
- ISymUnmanagedDocument::FindClosestLine method [.NET Framework debugging]
ms.assetid: 628f2a04-e529-407d-841e-3b3da219a9cb
topic_type: apiref
caps.latest.revision: "8"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 8a4fff5ce5cdcde35c8483136cf4c3cd75854f6c
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2017
---
# <a name="isymunmanageddocumentfindclosestline-method"></a><span data-ttu-id="fe073-102">ISymUnmanagedDocument::FindClosestLine (Método)</span><span class="sxs-lookup"><span data-stu-id="fe073-102">ISymUnmanagedDocument::FindClosestLine Method</span></span>
<span data-ttu-id="fe073-103">Devuelve la línea más próxima que sea un punto de secuencia, dada una línea en este documento que puede ser o no un punto de secuencia.</span><span class="sxs-lookup"><span data-stu-id="fe073-103">Returns the closest line that is a sequence point, given a line in this document that may or may not be a sequence point.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fe073-104">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="fe073-104">Syntax</span></span>  
  
```  
HRESULT FindClosestLine(  
    [in]  ULONG32  line,  
    [out, retval] ULONG32*  pRetVal);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="fe073-105">Parámetros</span><span class="sxs-lookup"><span data-stu-id="fe073-105">Parameters</span></span>  
 `line`  
 <span data-ttu-id="fe073-106">[in] Una línea en este documento.</span><span class="sxs-lookup"><span data-stu-id="fe073-106">[in] A line in this document.</span></span>  
  
 `pRetVal`  
 <span data-ttu-id="fe073-107">[out] Un puntero a una variable que recibe la línea.</span><span class="sxs-lookup"><span data-stu-id="fe073-107">[out] A pointer to a variable that receives the line.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="fe073-108">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="fe073-108">Return Value</span></span>  
 <span data-ttu-id="fe073-109">S_OK si el método tiene éxito; en caso contrario, un código de error.</span><span class="sxs-lookup"><span data-stu-id="fe073-109">S_OK if the method succeeds; otherwise, an error code.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fe073-110">Vea también</span><span class="sxs-lookup"><span data-stu-id="fe073-110">See Also</span></span>  
 [<span data-ttu-id="fe073-111">ISymUnmanagedDocument (interfaz)</span><span class="sxs-lookup"><span data-stu-id="fe073-111">ISymUnmanagedDocument Interface</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-interface.md)