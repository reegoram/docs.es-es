---
title: 'Cómo: Incrustar expresiones en literales XML (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- embedded expressions [Visual Basic]
- XML literals [Visual Basic], embedded expressions
ms.assetid: 75016fad-0141-42de-8564-5051be29487e
ms.openlocfilehash: 41dc6ef8d2ec2ffd6cd1cf793911f2e09f1a1e77
ms.sourcegitcommit: e614e0f3b031293e4107f37f752be43652f3f253
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2018
ms.locfileid: "42929521"
---
# <a name="how-to-embed-expressions-in-xml-literals-visual-basic"></a>Cómo: Incrustar expresiones en literales XML (Visual Basic)
Literales XML se pueden combinar con expresiones incrustadas para crear un documento XML, fragmento o elemento que contiene el contenido creado en tiempo de ejecución. Los ejemplos siguientes muestran cómo utilizar expresiones incrustadas para rellenar los nombres de elementos, atributos y contenido del elemento en tiempo de ejecución.  
  
 La sintaxis de una expresión incrustada es `<%=` `exp` `%>`, que es la misma sintaxis que [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] usa. Para obtener más información, consulte [expresiones incrustadas en XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
 También puede usar el [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] API para crear [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] objetos. Para obtener más información, consulta <xref:System.Xml.Linq.XElement>.  
  
## <a name="procedures"></a>Procedimientos  
  
#### <a name="to-insert-text-as-element-content"></a>Para insertar texto como contenido del elemento  
  
-   El ejemplo siguiente muestra cómo insertar el texto que se encuentra en la `contactName` variable entre los elementos de nombre de apertura y cierre.  
  
     [!code-vb[VbXMLSamples#39](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-embed-expressions-in-xml-literals_1.vb)]  
  
     Este ejemplo produce el siguiente resultado:  
  
    ```xml  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-as-an-attribute-value"></a>Para insertar texto como un valor de atributo  
  
-   El ejemplo siguiente muestra cómo insertar el texto que se encuentra en la `phoneType` variable como el valor de la `type` atributo.  
  
     [!code-vb[VbXMLSamples#40](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-embed-expressions-in-xml-literals_2.vb)]  
  
     Este ejemplo produce el siguiente resultado:  
  
    ```xml  
    <contact>  
      <phone type="home">206-555-0144</phone>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-for-an-element-name"></a>Para insertar texto para un nombre de elemento  
  
-   El ejemplo siguiente muestra cómo insertar el texto que se encuentra en la `elementName` variable como el nombre de un elemento.  
  
     Al crear elementos mediante esta técnica, debe cerrarlos con la \</ > etiqueta.  
  
     [!code-vb[VbXMLSamples#41](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-embed-expressions-in-xml-literals_3.vb)]  
  
     Este ejemplo produce el siguiente resultado:  
  
    ```xml  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Crear literales XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-create-xml-literals.md)  
 [Expresiones incrustadas en XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)  
 [Crear XML en Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
