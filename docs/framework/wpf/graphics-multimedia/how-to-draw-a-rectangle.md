---
title: 'Cómo: Dibujar un rectángulo'
ms.date: 03/30/2017
helpviewer_keywords:
- drawing [WPF], rectangles
- graphics [WPF], rectangles
- rectangles [WPF], drawing
ms.assetid: beeb57ef-fab5-4446-a38a-1588f97b4c2f
ms.openlocfilehash: 5f65bd11976817fe3f4d3e5d016f820a249769c3
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43506159"
---
# <a name="how-to-draw-a-rectangle"></a>Cómo: Dibujar un rectángulo
En este ejemplo se muestra cómo dibujar un rectángulo con el <xref:System.Windows.Shapes.Rectangle> elemento.  
  
 Para dibujar un rectángulo, cree un <xref:System.Windows.Shapes.Rectangle> elemento y especifique su <xref:System.Windows.FrameworkElement.Width%2A> y <xref:System.Windows.FrameworkElement.Height%2A>. Para pintar el interior del rectángulo, establezca su <xref:System.Windows.Shapes.Shape.Fill%2A>. Para dar un contorno de rectángulo, utilice su <xref:System.Windows.Shapes.Shape.Stroke%2A> y <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> propiedades.  
  
 Para dar el rectángulo esquinas redondeadas, especifique el valor opcional <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> y <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> propiedades. El <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> y <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> propiedades establecen los radios de ejes x y y de la elipse que se usa para redondear los vértices del rectángulo.  
  
 En el ejemplo siguiente, dos <xref:System.Windows.Shapes.Rectangle> se dibujan un <xref:System.Windows.Controls.Canvas>. El primer rectángulo tiene un <xref:System.Windows.Media.Brushes.Blue%2A> interior. El segundo rectángulo tiene una <xref:System.Windows.Media.Brushes.Blue%2A> interiores, un <xref:System.Windows.Media.Brushes.Black%2A> esquema y las esquinas redondeadas.  
  
## <a name="example"></a>Ejemplo  
 [!code-xaml[drawingwithshapeelements#Rectangle1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/rectangleexample.xaml#rectangle1)]  
  
 Aunque este ejemplo usa un <xref:System.Windows.Controls.Canvas> para contener los rectángulos, puede usar elementos de rectángulo (y todos los demás elementos de forma) con cualquier <xref:System.Windows.Controls.Panel> o <xref:System.Windows.Controls.Control> que admita contenido que no sean de texto. De hecho, los rectángulos son especialmente útiles para proporcionar fondos para partes de <xref:System.Windows.Controls.Grid> paneles. Para obtener un ejemplo, vea el [información general sobre tablas](../../../../docs/framework/wpf/advanced/table-overview.md).  
  
 Este ejemplo forma parte de un ejemplo más extenso; Para obtener un ejemplo completo, vea [Shape Elements Sample](https://go.microsoft.com/fwlink/?LinkID=160037).  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Windows.Shapes.Rectangle>  
 [Ejemplo de los elementos de forma](https://go.microsoft.com/fwlink/?LinkID=160037)  
 [Información general sobre formas y dibujo básico en WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)  
 [Información general sobre tablas](../../../../docs/framework/wpf/advanced/table-overview.md)
