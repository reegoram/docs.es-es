---
title: No se pudo obtener el nombre completo del sistema operativo debido a un error interno
ms.date: 07/20/2015
f1_keywords:
- vbrDiagnosticInfo_FullOSName
ms.assetid: f69da02b-eb9a-4284-bb9e-3025517ae6c1
ms.openlocfilehash: 192033348a779591a54860505d5d707a802c415a
ms.sourcegitcommit: 5bbfe34a9a14e4ccb22367e57b57585c208cf757
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2018
ms.locfileid: "45972733"
---
# <a name="could-not-obtain-full-operation-system-name-due-to-internal-error"></a>No se pudo obtener el nombre completo del sistema operativo debido a un error interno
No se pudo obtener el nombre completo del sistema operativo debido a un error interno. La causa podría ser que WMI no exista en la máquina actual.  
  
 Error al llamar a la propiedad `My.Computer.Info.OSFullName` . Una posible causa de este error es que Instrumental de administración de Windows (WMI) no esté instalado en el equipo actual.  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
1.  Agregue un bloque `Try...Catch` alrededor de la llamada a la propiedad `My.Computer.Info.OSFullName` .  
  
2.  Para obtener más información acerca de WMI y cómo instalarlo, vaya a y busque "Windows Management Instrumentation Core".  
  
## <a name="see-also"></a>Vea también  
 [My.Computer.Info.OSFullName](xref:Microsoft.VisualBasic.Devices.ComputerInfo.OSFullName)  
 [Excepciones y control de errores en Visual Basic](https://msdn.microsoft.com/library/3e351e73-cf23-40ab-8b60-05794160529e)  
 [Try...Catch...Finally (instrucción)](../../visual-basic/language-reference/statements/try-catch-finally-statement.md)
