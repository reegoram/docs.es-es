---
title: Limitaciones del componente Timer de formularios Windows Forms&#39;s propiedad del intervalo
ms.date: 03/30/2017
helpviewer_keywords:
- timers [Windows Forms], event intervals
- Interval property [Windows Forms], limitations
- timers [Windows Forms], Windows-based
- Timer component [Windows Forms], limitations of Interval property
ms.assetid: 7e5fb513-77e7-4046-a8e8-aab94e61ca0f
ms.openlocfilehash: e5b9e7e43369913f0cdc9c7f2111bd4fe58675e6
ms.sourcegitcommit: efff8f331fd9467f093f8ab8d23a203d6ecb5b60
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2018
ms.locfileid: "43465660"
---
# <a name="limitations-of-the-windows-forms-timer-component39s-interval-property"></a>Limitaciones del componente Timer de formularios Windows Forms&#39;s propiedad del intervalo
Los formularios de Windows <xref:System.Windows.Forms.Timer> componente tiene un <xref:System.Windows.Forms.Timer.Interval%2A> propiedad que especifica el número de milisegundos que transcurren entre un evento del temporizador y el siguiente. A menos que el componente está deshabilitado, un temporizador continúa recibiendo el <xref:System.Windows.Forms.Timer.Tick> eventos a intervalos de tiempo aproximadamente iguales.  
  
 Este componente está diseñado para un entorno de Windows Forms. Si necesita un temporizador que sea adecuado para un entorno de servidor, consulte [Introducción a los temporizadores basados en servidor](https://msdn.microsoft.com/library/adc0bc0a-a519-4812-bafc-fb9d1a5801fc).  
  
## <a name="the-interval-property"></a>La propiedad Interval  
 El <xref:System.Windows.Forms.Timer.Interval%2A> propiedad tiene algunas limitaciones a tener en cuenta al programar un <xref:System.Windows.Forms.Timer> componente:  
  
-   Si la aplicación u otra aplicación está realizando fuertes exigencias del sistema, como bucles largos, cálculos intensivos o unidad, red o acceso a los puertos, la aplicación no es posible que obtenga los eventos del temporizador con tanta frecuencia como los <xref:System.Windows.Forms.Timer.Interval%2A> especifica la propiedad.  
  
-   El intervalo no se garantiza que transcurran exactamente en el tiempo. Para garantizar la precisión, el temporizador debe comprobar el reloj del sistema según sea necesario, en lugar de intentar realizar un seguimiento del tiempo acumulado internamente.  
  
-   La precisión de la <xref:System.Windows.Forms.Timer.Interval%2A> propiedad está en milisegundos. Algunos equipos proporcionan un contador de alta resolución que tenga una resolución mayor que milisegundos. La disponibilidad de este tipo de contador depende del hardware del procesador del equipo. Para obtener más información, vea el artículo 172338, "Cómo a usar QueryPerformanceCounter al código de tiempo," de Microsoft Knowledge Base en http://support.microsoft.com.  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Windows.Forms.Timer>  
 [Timer (componente)](../../../../docs/framework/winforms/controls/timer-component-windows-forms.md)  
 [Información general sobre el componente Timer](../../../../docs/framework/winforms/controls/timer-component-overview-windows-forms.md)
