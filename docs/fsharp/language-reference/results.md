---
title: 'Resultados (F #)'
description: "Obtenga información acerca de cómo usar el tipo 'Provocar' de F # para ayudarle a escribir código tolerante a errores."
keywords: "visual f#, f#, programación funcional"
author: cartermp
ms.author: phcart
ms.date: 04/24/2017
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: a15b5cf1-9055-4481-918c-4c8a051b5829
ms.openlocfilehash: 26478ccfbf88d43c0b194e77d9aacc313515283f
ms.sourcegitcommit: 8d14e8c1b15009330c9880f8523686158924e1a4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2017
---
# <a name="results"></a><span data-ttu-id="a1af5-104">Resultados</span><span class="sxs-lookup"><span data-stu-id="a1af5-104">Results</span></span>

<span data-ttu-id="a1af5-105">A partir de F # 4.1, hay un `Result<'T,'TFailure>` tipo que puede utilizar para escribir código tolerante a errores que puede combinarse.</span><span class="sxs-lookup"><span data-stu-id="a1af5-105">Starting with F# 4.1, there is a `Result<'T,'TFailure>` type which you can use for writing error-tolerant code which can be composed.</span></span>

## <a name="syntax"></a><span data-ttu-id="a1af5-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="a1af5-106">Syntax</span></span>

```fsharp
// The definition of Result in FSharp.Core
[<StructuralEquality; StructuralComparison>]
[<CompiledName("FSharpResult`2")>]
[<Struct>]
type Result<'T,'TError> = 
    | Ok of ResultValue:'T 
    | Error of ErrorValue:'TError
```

## <a name="remarks"></a><span data-ttu-id="a1af5-107">Comentarios</span><span class="sxs-lookup"><span data-stu-id="a1af5-107">Remarks</span></span>

<span data-ttu-id="a1af5-108">Tenga en cuenta que el tipo de resultado es un [struct unión discriminada](discriminated-unions.md#struct-discriminated-unions), que es otra característica que se introdujo en F # 4.1.</span><span class="sxs-lookup"><span data-stu-id="a1af5-108">Note that the result type is a [struct discriminated union](discriminated-unions.md#struct-discriminated-unions), which is another feature introduced in F# 4.1.</span></span>  <span data-ttu-id="a1af5-109">Semántica de igualdad estructural se aplica aquí.</span><span class="sxs-lookup"><span data-stu-id="a1af5-109">Structural equality semantics apply here.</span></span>

<span data-ttu-id="a1af5-110">El `Result` tipo se utiliza habitualmente en monádico control de errores, que a menudo se conoce como [programación orientada a ferroviario](https://swlaschin.gitbooks.io/fsharpforfunandprofit/content/posts/recipe-part2.html) dentro de la Comunidad de F #.</span><span class="sxs-lookup"><span data-stu-id="a1af5-110">The `Result` type is typically used in monadic error-handling, which is often referred to as [Railway-oriented Programming](https://swlaschin.gitbooks.io/fsharpforfunandprofit/content/posts/recipe-part2.html) within the F# community.</span></span>  <span data-ttu-id="a1af5-111">El siguiente ejemplo trivial muestra este enfoque.</span><span class="sxs-lookup"><span data-stu-id="a1af5-111">The following trivial example demonstrates this approach.</span></span>

```fsharp
// Define a simple type which has fields that can be validated
type Request = 
    { Name: string
      Email: string }

// Define some logic for what defines a valid name.
//
// Generates a Result which is an Ok if the name validates;
// otherwise, it generates a Result which is an Error.
let validateName req =
    match req.Name with
    | null -> Error "No name found."
    | String.Empty -> Error "Name is empty."
    | "bananas" -> Error "Bananas is not a name."
    | _ -> Ok req

// Similarly, define some email validation logic.
let validateEmail req =
    match req.Email with
    | null -> Error "No email found."
    | String.Empty -> Error "Email is empty."
    | s when s.EndsWith("bananas.com") -> Error "No email from bananas.com is allowed."
    | _ -> OK req

let validateRequest reqResult =
    reqResult 
    |> Result.bind validateName
    |> Result.bind validateEmail

let test() = 
    // Now, create a Request and pattern match on the result.
    let req1 = { Name = "Phillip"; Email = "phillip@contoso.biz" }
    let res1 = validateRequest (OK req1)
    match res1 with
    | Ok req -> printfn "My request was valid! Name: %s Email %s" req1.Name req1.Email
    | Error e -> printfn "Error: %s" e
    // Prints " "My request was valid!  Name: Phillip Email: phillip@consoto.biz"

    let req2 = { Name = "Phillip"; Email = "phillip@bananas.com" }
    let res2 = validateRequest (OK req2)
    match res2 with
    | Ok req -> printfn "My request was valid! Name: %s Email %s" req1.Name req1.Email
    | Error e -> printfn "Error: %s" e
    // Prints: "Error: No email from bananas.com is allowed."

test()
```

<span data-ttu-id="a1af5-112">Como puede ver, es bastante fácil encadenar varias funciones de validación si se fuerza que todas ellas para devolver un `Result`.</span><span class="sxs-lookup"><span data-stu-id="a1af5-112">As you can see, it's quite easy to chain together various validation functions if you force them all to return a `Result`.</span></span>  <span data-ttu-id="a1af5-113">Esto permite dividir la funcionalidad similar al siguiente en pequeñas porciones que son como que admite composición según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a1af5-113">This lets you break up functionality like this into small pieces which are as composable as you need them to be.</span></span>  <span data-ttu-id="a1af5-114">Este enfoque también tiene el valor añadido de *exigir* el uso de [coincidencia de patrones](pattern-matching.md) al final de un ciclo de validación, lo exige un mayor grado de corrección del programa.</span><span class="sxs-lookup"><span data-stu-id="a1af5-114">This also has the added value of *enforcing* the use of [pattern matching](pattern-matching.md) at the end of a round of validation, which in turns enforces a higher degree of program correctness.</span></span>

## <a name="see-also"></a><span data-ttu-id="a1af5-115">Vea también</span><span class="sxs-lookup"><span data-stu-id="a1af5-115">See Also</span></span>

[<span data-ttu-id="a1af5-116">Uniones discriminadas</span><span class="sxs-lookup"><span data-stu-id="a1af5-116">Discriminated Unions</span></span>](discriminated-unions.md)

[<span data-ttu-id="a1af5-117">Coincidencia de patrones</span><span class="sxs-lookup"><span data-stu-id="a1af5-117">Pattern Matching</span></span>](pattern-matching.md)