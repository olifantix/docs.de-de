---
title: public (C#-Referenz)
ms.date: 07/20/2015
f1_keywords:
- public
- public_CSharpKeyword
helpviewer_keywords:
- public keyword [C#]
ms.assetid: 0ae45d16-a551-4b74-9845-57208de1328e
ms.openlocfilehash: abf7219359c108108b1ce3a3fde3dc10f9a8732d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="public-c-reference"></a>public (C#-Referenz)
Das Schlüsselwort `public` ist ein Zugriffsmodifizierer für Typen und Typmember. Der öffentlicher Zugriff ist die eingeschränkteste Zugriffsebene. Es gibt keine Einschränkungen für den Zugriff auf öffentliche Member, wie im folgenden Beispiel veranschaulicht:  
  
```  
class SampleClass  
{  
    public int x; // No access restrictions.  
}  
```  
  
 Unter [Access Modifiers (Zugriffsmodifizierer)](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md) und [Accessibility Levels (Zugriffsebenen)](../../../csharp/language-reference/keywords/accessibility-levels.md) finden Sie weitere Informationen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden zwei Klassen deklariert, `PointTest` und `MainClass`. Auf die öffentlichen Member `x` und `y` von `PointTest` wird direkt von `MainClass` zugegriffen.  
  
 [!code-csharp[csrefKeywordsModifiers#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/public_1.cs)]  
  
 Wenn Sie die Zugriffsebene `public` auf [private](../../../csharp/language-reference/keywords/private.md) (privat) oder [protected](../../../csharp/language-reference/keywords/protected.md) (geschützt) festlegen, wird die folgende Fehlermeldung angezeigt:  
  
 'PointTest.y' is inaccessible due to its protection level (Der Zugriff auf ‚PointTest.y‘ ist aufgrund der Sicherheitsebene nicht möglich).  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Referenz](../../../csharp/language-reference/index.md)  
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)  
 [Zugriffsmodifizierer](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)  
 [C#-Schlüsselwörter](../../../csharp/language-reference/keywords/index.md)  
 [Zugriffsmodifizierer](../../../csharp/language-reference/keywords/access-modifiers.md)  
 [Zugriffsebenen](../../../csharp/language-reference/keywords/accessibility-levels.md)  
 [Modifizierer](../../../csharp/language-reference/keywords/modifiers.md)  
 [private](../../../csharp/language-reference/keywords/private.md)  
 [protected](../../../csharp/language-reference/keywords/protected.md)  
 [internal](../../../csharp/language-reference/keywords/internal.md)
