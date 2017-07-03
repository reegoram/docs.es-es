---
title: "xml:lang Handling in XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XAML [XAML Services], xml:lang attribute"
  - "xml:lang attribute [XAML Services]"
  - "RFC 3066 standard [XAML Services]"
  - "standards [XAML Services], RFC 3066"
ms.assetid: 7aac0078-a1c5-41f8-b8b0-975510d9dca0
caps.latest.revision: 16
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 15
---
# xml:lang Handling in XAML
El atributo `xml:lang` es un atributo definido por [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)] que declara la información de idioma y referencia cultural para un elemento en XML. Este mismo significado del atributo persiste en XAML; sin embargo, se aplican algunas consideraciones adicionales.  
  
## Uso de atributos XAML  
  
```  
<object xml:lang="rfc3066lang" />  
```  
  
## Valores XAML  
  
|||  
|-|-|  
|*rfc3066lang*|Una cadena que se deriva del estándar [RFC 3066](http://go.microsoft.com/fwlink/?LinkId=132454) e identifica un idioma o un idioma\-región. En el caso de la segunda opción, el idioma y la región se separan con un solo guión. Para más información sobre los valores y el formato, vea <xref:System.Windows.Markup.XmlLanguage>.|  
  
## Comentarios  
 La definición del atributo `xml:lang` en [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] se deriva de `xml:lang` definido como un "atributo especial" por [!INCLUDE[TLA#tla_w3c](../../../includes/tlasharptla-w3c-md.md)] para [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)]. La información del idioma y de la referencia cultural se puede procesar de maneras diferentes, en función de sus implementaciones; sin embargo, no hay ningún procesamiento de [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] predeterminado del atributo `xml:lang`.  
  
 El valor predeterminado del atributo `xml:lang` es una cadena vacía en el nivel de atributo.  
  
 Los efectos del atributo `xml:lang` y el valor del atributo suelen perpetuarse para los elementos secundarios, cuando se interpretan por los sistemas que actúan en los valores `xml:lang`.  
  
 Cuando se interpreta por objetos de escritura XAML de los servicios XAML de .NET Framework, un valor `xml:lang` puede crear objetos <xref:System.Windows.Markup.XmlLanguage> o <xref:System.Globalization.CultureInfo> en la representación de objetos subyacente; sin embargo, ese comportamiento depende de si el valor especificado para `xml:lang` es una construcción válida para esas clases.  
  
 Los marcos de trabajo pueden crear asociaciones entre las propiedades definidas por el marco de trabajo y el significado de `xml:lang` en XML aplicando <xref:System.Windows.Markup.XmlLangPropertyAttribute> a la propiedad.  
  
## Nodos de uso de WPF  
 Para los elementos que son las clases derivadas de <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>, puede usar la propiedad de dependencia <xref:System.Windows.FrameworkElement.Language%2A> equivalente en lugar del atributo `xml:lang`. De forma predeterminada, la propiedad <xref:System.Windows.FrameworkElement.Language%2A> usa "en\-US" si no se establece de otra manera, a través de la propiedad o mediante el procesamiento del atributo `xml:lang`.  
  
## Vea también  
 [Globalización de WPF](../../../ocs/framework/wpf/advanced/globalization-for-wpf.md)