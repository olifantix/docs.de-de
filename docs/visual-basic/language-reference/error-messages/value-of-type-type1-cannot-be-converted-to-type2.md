---
title: Wert des Typs &#39;Typ1&#39; kann nicht konvertiert werden, um &#39;Typ2&#39;
ms.date: 07/20/2015
f1_keywords:
- vbc31194
- bc31194
helpviewer_keywords:
- BC31194
ms.assetid: 03d50c31-addd-4c90-9c53-725b84f9782e
ms.openlocfilehash: 9e59d3bc5e2bfca3628248d08ffc475334d4da79
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="value-of-type-39type139-cannot-be-converted-to-39type239"></a>Wert des Typs &#39;Typ1&#39; kann nicht konvertiert werden, um &#39;Typ2&#39;
Wert vom Typ "Typ1" kann nicht in "Typ2" konvertiert werden. Sie können die Eigenschaft "Value" den Zeichenfolgenwert des ersten Elements der abzurufenden "\<ParentElement >'.  
  
 Es wurde versucht, ein XML-Literal implizit in einen bestimmten Typ umzuwandeln. Das XML-Literal kann nicht implizit in den angegebenen Typ umgewandelt werden.  
  
 **Fehler-ID:** BC31194  
  
## <a name="to-correct-this-error"></a>So beheben Sie diesen Fehler  
  
-   Verwenden Sie die `Value` -Eigenschaft des XML-Literals, um auf dessen Wert als `String`zu verweisen. Verwenden Sie die `CType` -Funktion, eine weitere Typkonvertierungsfunktion, oder die <xref:System.Convert> -Klasse, um den Wert in den angegebenen Typ umzuwandeln.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Convert>  
 [Typkonvertierungsfunktionen](../../../visual-basic/language-reference/functions/type-conversion-functions.md)  
 [XML-Literale](../../../visual-basic/language-reference/xml-literals/index.md)  
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)
