---
title: -delaysign (Opciones del compilador de C#)
ms.date: 05/15/2018
f1_keywords:
- /delaysign
helpviewer_keywords:
- -delaysign compiler option [C#]
- delaysign compiler option [C#]
- /delaysign compiler option [C#]
ms.assetid: bcb058eb-2933-4e7f-b356-5c941db4de75
ms.openlocfilehash: 105f564d40799c1c006caf8b59d6199dbd8e9318
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43518335"
---
# <a name="-delaysign-c-compiler-options"></a>-delaysign (Opciones del compilador de C#)

Esta opción hace que el compilador reserve espacio en el archivo de salida de manera que se pueda agregar una firma digital más adelante.

## <a name="syntax"></a>Sintaxis

```console
-delaysign[ + | - ]
```

## <a name="arguments"></a>Argumentos

`+` &#124; `-`

Use **-delaysign-** para firmar completamente un ensamblado. Use **-delaysign+** si quiere incluir solo la clave pública en el ensamblado. El valor predeterminado es **-delaysign-**.

## <a name="remarks"></a>Comentarios

La opción **-delaysign** no tiene ningún efecto a menos que se use con [-keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md) o [-keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md).

Las opciones **-delaysign** y **-publicsign** son mutuamente excluyentes.

Cuando se solicita un ensamblado totalmente firmado, el compilador genera un valor hash para el archivo que contiene el manifiesto (metadatos del ensamblado) y firma dicho valor mediante la clave privada. Esta operación crea una firma digital que se almacena en el archivo que contiene el manifiesto. Cuando se retrasa la firma de un ensamblado, el compilador no calcula ni almacena la firma, sino que reserva espacio en el archivo para que la firma se pueda agregar más tarde.

Por ejemplo, si se usa **-delaysign+**, los evaluadores podrán colocar el ensamblado en la memoria caché global. Después de realizar las pruebas, coloque la clave privada en el ensamblado mediante la utilidad [Assembly Linker](../../../framework/tools/al-exe-assembly-linker.md) para firmar el ensamblado por completo.

Para obtener más información, vea [Crear y usar ensamblados con nombre seguro](../../../framework/app-domains/create-and-use-strong-named-assemblies.md) y [Delay Signing an Assembly](../../../framework/app-domains/delay-sign-assembly.md) (Retrasar la firma de un ensamblado).

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para establecer esta opción del compilador en el entorno de desarrollo de Visual Studio

1. Abra la página **Propiedades** del proyecto.
1. Modifique la propiedad **Solo retrasar firma**.

Para obtener información sobre cómo establecer esta opción del compilador mediante programación, vea <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>.

## <a name="see-also"></a>Vea también

- [Opción C# -publicsign](publicsign-compiler-option.md)  
- [Opciones del compilador de C#](index.md)  
- [Administrar propiedades de soluciones y proyectos](/visualstudio/ide/managing-project-and-solution-properties)
