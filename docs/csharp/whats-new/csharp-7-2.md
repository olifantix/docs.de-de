---
title: Neues in C# 7.2
description: "Eine Übersicht der neuen Funktionen in C# 7.2"
keywords: C#-Sprachentwurf, 7.2, Visual Studio 2017,
author: billwagner
ms.author: wiwagn
ms.date: 08/16/2017
ms.topic: article
ms.prod: .net
ms.devlang: devlang-csharp
ms.openlocfilehash: cc861f186bea681bb32a2f8041a7155026679987
ms.sourcegitcommit: 401c4427a3ec0d1263543033b3084039278509dc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2017
---
# <a name="whats-new-in-c-72"></a><span data-ttu-id="02df0-104">Neues in C# 7.2</span><span class="sxs-lookup"><span data-stu-id="02df0-104">What's new in C# 7.2</span></span>

<span data-ttu-id="02df0-105">C# 7.2 ist ein weiteres Release einer Unterversion, das eine Reihe nützlicher Funktionen ergänzt.</span><span class="sxs-lookup"><span data-stu-id="02df0-105">C# 7.2 is another point release that adds a number of useful features.</span></span>
<span data-ttu-id="02df0-106">Ein Aspekt für diesen Release ist die effizientere Arbeit mit Werttypen durch Vermeiden unnötiger Kopien oder Zuweisungen.</span><span class="sxs-lookup"><span data-stu-id="02df0-106">One theme for this release is working more efficiently with value types by avoiding unnecessary copies or allocations.</span></span> 

<span data-ttu-id="02df0-107">Die restlichen Funktionen sind kleine Features, die den Komfort steigern.</span><span class="sxs-lookup"><span data-stu-id="02df0-107">The remaining features are small, nice-to-have features.</span></span>

<span data-ttu-id="02df0-108">C# 7.2 verwendet das Konfigurationselement [Sprachversionsauswahl](csharp-7-1.md#language-version-selection), um die Version der Compilersprache auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="02df0-108">C# 7.2 uses the [language version selection](csharp-7-1.md#language-version-selection) configuration element to select the compiler language version.</span></span>

<span data-ttu-id="02df0-109">Die neuen Sprachfeatures in diesem Release umfassen:</span><span class="sxs-lookup"><span data-stu-id="02df0-109">The new language features in this release are:</span></span>

* [<span data-ttu-id="02df0-110">Verweissemantik mit Werttypen</span><span class="sxs-lookup"><span data-stu-id="02df0-110">Reference semantics with value types</span></span>](#reference-semantics-with-value-types)
  - <span data-ttu-id="02df0-111">Eine Kombination aus Verbesserungen der Syntax, die das Arbeiten mit Werttypen mithilfe von Verweissemantik ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="02df0-111">A combination of syntax improvements that enable working with value types using reference semantics.</span></span>
* [<span data-ttu-id="02df0-112">Nicht schließende benannte Argumente</span><span class="sxs-lookup"><span data-stu-id="02df0-112">Non-trailing named arguments</span></span>](#non-trailing-named-arguments)
  - <span data-ttu-id="02df0-113">Positionelle Argumente können auf benannte Argumente folgen.</span><span class="sxs-lookup"><span data-stu-id="02df0-113">Named arguments can be followed by positional arguments.</span></span>
* [<span data-ttu-id="02df0-114">Führende Unterstriche in numerischen Literalen</span><span class="sxs-lookup"><span data-stu-id="02df0-114">Leading underscores in numeric literals</span></span>](#leading-underscores-in-numeric-literals)
  - <span data-ttu-id="02df0-115">Numerische Literale dürfen jetzt führende Unterstriche vor aufgeführten Stellen aufweisen.</span><span class="sxs-lookup"><span data-stu-id="02df0-115">Numeric literals can now have leading underscores before any printed digits.</span></span>
* [<span data-ttu-id="02df0-116">`private protected`-Zugriffsmodifizierer</span><span class="sxs-lookup"><span data-stu-id="02df0-116">`private protected` access modifier</span></span>](#private-protected)
  - <span data-ttu-id="02df0-117">Der `private protected`-Zugriffsmodifizierer ermöglicht den Zugriff für abgeleitete Klassen innerhalb der gleichen Assembly.</span><span class="sxs-lookup"><span data-stu-id="02df0-117">The `private protected` access modifier enables access for derived classes in the same assembly.</span></span>

## <a name="reference-semantics-with-value-types"></a><span data-ttu-id="02df0-118">Verweissemantik mit Werttypen</span><span class="sxs-lookup"><span data-stu-id="02df0-118">Reference semantics with value types</span></span>

<span data-ttu-id="02df0-119">In 7.2 eingeführte Sprachfeatures ermöglichen das Arbeiten mit Werttypen bei Verwendung der Verweissemantik.</span><span class="sxs-lookup"><span data-stu-id="02df0-119">Language features introduced in 7.2 let you work with value types while using reference semantics.</span></span> <span data-ttu-id="02df0-120">Sie dienen dazu, die Leistung durch Minimieren des Kopierens von Werttypen zu steigern, ohne die Speicherzuweisungen nach sich zu ziehen, die eine Verwendung von Verweistypen mit sich bringen würde.</span><span class="sxs-lookup"><span data-stu-id="02df0-120">They are designed to increase performance by minimizing copying value types without incurring the memory allocations associated with using reference types.</span></span> <span data-ttu-id="02df0-121">Das Feature beinhaltet:</span><span class="sxs-lookup"><span data-stu-id="02df0-121">The features include:</span></span>

 - <span data-ttu-id="02df0-122">Den `in`-Modifizierer für Parameter zur Angabe, dass ein Argument durch Verweis übergeben, von der aufgerufenen Methode aber nicht verändert wird.</span><span class="sxs-lookup"><span data-stu-id="02df0-122">The `in` modifier on parameters, to specify that an argument is passed by reference but not modified by the called method.</span></span>
 - <span data-ttu-id="02df0-123">Der `ref readonly`-Modifizierer für die Methodenrückgabe, um anzugeben, dass eine Methode ihren Wert als Verweis zurückgibt und keinen Schreibzugriff auf dieses Objekt zulässt.</span><span class="sxs-lookup"><span data-stu-id="02df0-123">The `ref readonly` modifier on method returns, to indicate that a method returns its value by reference but doesn't allow writes to that object.</span></span>
 - <span data-ttu-id="02df0-124">Die `readonly struct`-Deklaration, um anzugeben, dass eine Struktur unveränderlich ist und ihren Membermethoden als `in`-Parameter übergeben werden sollte.</span><span class="sxs-lookup"><span data-stu-id="02df0-124">The `readonly struct` declaration, to indicate that a struct is immutable and should be passed as an `in` parameter to its member methods.</span></span>
 - <span data-ttu-id="02df0-125">Die `ref struct`-Deklaration, um anzugeben, dass ein Strukturtyp direkt auf verwalteten Arbeitsspeicher zugreift und immer per Stapel zugeordnet werden muss.</span><span class="sxs-lookup"><span data-stu-id="02df0-125">The `ref struct` declaration, to indicate that a struct type accesses managed memory directly and must always be stack allocated.</span></span>

<span data-ttu-id="02df0-126">Weitere Informationen zu allen diesen Änderungen finden Sie unter [Verwenden von Werttypen mit Verweissemantik](../reference-semantics-with-value-types.md).</span><span class="sxs-lookup"><span data-stu-id="02df0-126">You can read more about all these changes in [Using value types with reference semantics](../reference-semantics-with-value-types.md).</span></span>

## <a name="non-trailing-named-arguments"></a><span data-ttu-id="02df0-127">Nicht schließende benannte Argumente</span><span class="sxs-lookup"><span data-stu-id="02df0-127">Non-trailing named arguments</span></span>

<span data-ttu-id="02df0-128">Methodenaufrufe dürfen jetzt benannte Argumente verwenden, die positionellen Argumenten vorstehen, wenn diese benannten Argumente in der richtigen Position verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="02df0-128">Method calls may now use named arguments that precede positional arguments when those named arguments are in the correct positions.</span></span> <span data-ttu-id="02df0-129">Weitere Informationen finden Sie unter [Benannte und optionale Argumente](../programming-guide/classes-and-structs/named-and-optional-arguments.md).</span><span class="sxs-lookup"><span data-stu-id="02df0-129">For more information see [Named and optional arguments](../programming-guide/classes-and-structs/named-and-optional-arguments.md).</span></span>

## <a name="leading-underscores-in-numeric-literals"></a><span data-ttu-id="02df0-130">Führende Unterstriche in numerischen Literalen</span><span class="sxs-lookup"><span data-stu-id="02df0-130">Leading underscores in numeric literals</span></span>

<span data-ttu-id="02df0-131">Die Implementierung der Unterstützung für Stellentrennzeichen in C# 7.0 ließ den Unterstrich `_` nicht als erstes Zeichen von Literalwerten zu.</span><span class="sxs-lookup"><span data-stu-id="02df0-131">The implementation of support for digit separators in C# 7.0 didn't allow the `_` to be the first character of the literal value.</span></span> <span data-ttu-id="02df0-132">Hexadezimale und binäre numerische Literale dürfen jetzt mit einem `_` beginnen.</span><span class="sxs-lookup"><span data-stu-id="02df0-132">Hex and binary numeric literals may now begin with an `_`.</span></span> 

<span data-ttu-id="02df0-133">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="02df0-133">For example:</span></span>

```csharp
int binaryValue = 0b_0101_0101;
```

## `private protected`

<span data-ttu-id="02df0-134">Schließlich zeigt der neue, zusammengesetzte Zugriffsmodifizierer `private protected` an, dass auf ein Element durch eine es enthaltende Klasse oder durch innerhalb der gleichen Assembly deklarierte abgeleitete Klassen zugegriffen werden darf.</span><span class="sxs-lookup"><span data-stu-id="02df0-134">Finally, a new compound access modifier: `private protected` indicates that a member may be accessed by containing class or derived classes that are declared in the same assembly.</span></span> <span data-ttu-id="02df0-135">Während `protected internal` den Zugriff durch abgeleitete Klassen oder Klassen, die sich in der gleichen Assembly befinden, erlaubt, schränkt `private protected` den Zugriff auf innerhalb der gleichen Assembly deklarierte abgeleitete Typen ein.</span><span class="sxs-lookup"><span data-stu-id="02df0-135">While `protected internal` allows access by derived classes or classes that are in the same assembly, `private protected` limits access to derived types declared in the same assembly.</span></span>

<span data-ttu-id="02df0-136">Weitere Informationen finden Sie unter [Zugriffsmodifizierer](../language-reference/keywords/access-modifiers.md) in der Sprachreferenz.</span><span class="sxs-lookup"><span data-stu-id="02df0-136">For more information see [access modifiers](../language-reference/keywords/access-modifiers.md) in the language reference.</span></span>