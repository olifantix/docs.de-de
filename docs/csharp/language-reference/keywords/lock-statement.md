---
title: lock-Anweisung (C#-Referenz)
ms.date: 07/20/2015
f1_keywords:
- lock_CSharpKeyword
- lock
helpviewer_keywords:
- lock keyword [C#]
ms.assetid: 656da1a4-707e-4ef6-9c6e-6d13b646af42
ms.openlocfilehash: 2ce870e8caa67d780ce603a6f1dbcc7cd303b842
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="lock-statement-c-reference"></a>lock-Anweisung (C#-Referenz)
Das Schlüsselwort `lock` kennzeichnet einen Anweisungsblock als kritischen Abschnitt, indem es die sich gegenseitig ausschließende Sperre für ein gegebenes Objekt abruft, eine Anweisung ausführt und anschließend die Sperre aufhebt. Das folgende Beispiel enthält eine `lock`-Anweisung.  
  
```csharp  
class Account  
{  
    decimal balance;  
    private Object thisLock = new Object();  
  
    public void Withdraw(decimal amount)  
    {  
        lock (thisLock)  
        {  
            if (amount > balance)  
            {  
                throw new Exception("Insufficient funds");  
            }  
            balance -= amount;  
        }  
    }  
}  
```  
  
 Weitere Informationen finden Sie unter [Threadsynchronisierung](../../programming-guide/concepts/threading/thread-synchronization.md).  
  
## <a name="remarks"></a>Hinweise  
 Das Schlüsselwort `lock` stellt sicher, dass ein Thread keinen kritischen Abschnitt eines Codes betritt, während ein anderer Thread in diesem Abschnitt ist. Wenn ein anderer Thread versucht, auf einen gesperrten Code zuzugreifen, wartet er, sperrt, bis das Objekt freigegeben wird.  
  
 Der Abschnitt [Threading](../../programming-guide/concepts/threading/index.md) wird das Threading behandeln.  
  
 Das `lock`-Schlüsselwort ruft am Anfang des Blocks <xref:System.Threading.Monitor.Enter%2A> und am Ende des Blocks <xref:System.Threading.Monitor.Exit%2A> auf. Ein <xref:System.Threading.ThreadInterruptedException> wird ausgelöst, wenn <xref:System.Threading.Thread.Interrupt%2A> einen Thread unterbricht, der darauf wartet eine `lock`-Anweisung einzugeben.  
  
 Vermeiden Sie generell das Sperren eines `public`-Typs oder von Instanzen außerhalb der Kontrolle Ihres Codes. Die gemeinsamen Konstrukte `lock (this)`, `lock (typeof (MyType))` und `lock ("myLock")` verstoßen gegen diese Richtlinie:  
  
-   `lock (this)` ist ein Problem, wenn auf die Instanz öffentlich zugegriffen werden kann.  
  
-   `lock (typeof (MyType))` ist problematisch, wenn auf `MyType` öffentlich zugegriffen werden.  
  
-   `lock("myLock")` ist problematisch, weil jeder andere Code in diesem Prozess, der die selbe Zeichenfolge verwendet, die gleiche Sperre teilt.  
  
 Eine bewährte Methode ist es, ein `private`-Objekt zum Sperren, oder eine `private static`-Objektvariable zu definieren, die Daten schützt, die in allen Instanzen häufig vorkommen.  
  
 Sie können das Schlüsselwort [await](../../../csharp/language-reference/keywords/await.md) nicht im Text einer `lock`-Anweisung verwenden.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine einfache Verwendung von Threads ohne das Sperren in C# gezeigt.  
  
 [!code-csharp[csrefKeywordsFixedLock#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/lock-statement_1.cs)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden Threads und `lock` verwendet. Solange die `lock`-Anweisung vorhanden ist, ist der Anweisungsblock ein kritischer Abschnitt, und `balance` wird nie eine negative Zahl werden.  
  
 [!code-csharp[csrefKeywordsFixedLock#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/lock-statement_2.cs)]  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Reflection.MethodImplAttributes>  
 <xref:System.Threading.Mutex>  
 [C#-Referenz](../../../csharp/language-reference/index.md)  
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)  
 [Threading](../../programming-guide/concepts/threading/index.md)  
 [C#-Schlüsselwörter](../../../csharp/language-reference/keywords/index.md)  
 [Anweisungsschlüsselwörter](../../../csharp/language-reference/keywords/statement-keywords.md)  
 <xref:System.Threading.Monitor>  
 [Interlocked-Vorgänge](../../../standard/threading/interlocked-operations.md)  
 [AutoResetEvent](../../../standard/threading/autoresetevent.md)  
 [Threadsynchronisierung](../../programming-guide/concepts/threading/thread-synchronization.md)
