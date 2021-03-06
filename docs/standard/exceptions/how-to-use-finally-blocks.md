---
title: "Gewusst wie: Verwenden von Finally-Blöcken"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- exceptions, try/catch blocks
- exceptions, finally blocks
- try/catch blocks
- finally blocks
- ArgumentOutOfRangeException class
ms.assetid: 4b9c0137-04af-4468-91d1-b9014df8ddd2
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 325be4836d661369326fbe3ea1f8b252bf251f3c
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="how-to-use-finally-blocks"></a>Verwenden von finally-Blöcken

Wenn eine Ausnahme auftritt, wird die Ausführung beendet und die Steuerung an den entsprechenden Ausnahmehandler übergeben. Dies bedeutet häufig, dass Codezeilen umgangen werden, die eigentlich ausgeführt werden sollten. Daher muss auch nach Auslösen einer Ausnahme eine Ressourcenbereinigung durchgeführt werden, z.B. das Schließen einer Datei. Zu diesem Zweck können Sie einen `finally`-Block verwenden. Ein `finally`-Block wird immer ausgeführt, unabhängig davon, ob eine Ausnahme ausgelöst wird.

Das folgende Codebeispiel verwendet einen `try`/`catch`-Block, um eine <xref:System.ArgumentOutOfRangeException> abzufangen. Die `Main`-Methode erstellt zwei Arrays und versucht, das eine Array in das andere zu kopieren. Die Aktion generiert eine <xref:System.ArgumentOutOfRangeException>, und der Fehler wird an die Konsole geschrieben. Der `finally`-Block wird unabhängig vom Ergebnis des Kopiervorgangs ausgeführt.

[!code-cpp[CodeTryCatchFinallyExample#3](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeTryCatchFinallyExample/CPP/source2.cpp#3)]
[!code-csharp[CodeTryCatchFinallyExample#3](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeTryCatchFinallyExample/CS/source2.cs#3)]
[!code-vb[CodeTryCatchFinallyExample#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeTryCatchFinallyExample/VB/source2.vb#3)]  

## <a name="see-also"></a>Siehe auch  
[Ausnahmen](index.md)   
