---
title: 'Cómo: detener la carga de una página'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pages [WPF], stopping from loading
- methods [WPF], Stoploading
- events [WPF], NavigationStopped
- NavigationStopped properties [WPF]
- stopping pages from loading [WPF]
- loading [WPF], stopping
ms.assetid: e2b695b0-517e-462c-8ccf-90cc8d6ba864
ms.openlocfilehash: e5cd7d1b881b816636c3acdd4d33565304ca9b63
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33545550"
---
# <a name="how-to-stop-a-page-from-loading"></a>Cómo: detener la carga de una página
Este ejemplo muestra cómo llamar a la <xref:System.Windows.Navigation.NavigationWindow.StopLoading%2A> método para detener la navegación al contenido antes de haya terminado de descarga.  
  
## <a name="example"></a>Ejemplo  
 <xref:System.Windows.Navigation.NavigationWindow.StopLoading%2A> detiene la descarga del contenido solicitado y hace que el <xref:System.Windows.Navigation.NavigationWindow.NavigationStopped> evento.  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateStopLoadingCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/MainWindow.xaml.cs#navigatestoploadingcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateStopLoadingCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/mainwindow.xaml.vb#navigatestoploadingcode)]
