---
title: 'Gewusst wie: Registrieren eines benutzerdefinierten Protokolls mit WebRequest'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 98ddbdb9-66b1-4080-92ad-51f5c447fcf8
caps.latest.revision: "11"
author: mcleblanc
ms.author: markl
manager: markl
ms.workload: dotnet
ms.openlocfilehash: 7fefaf65fe0bf1c761e976359f3015389a557369
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-register-a-custom-protocol-using-webrequest"></a>Gewusst wie: Registrieren eines benutzerdefinierten Protokolls mit WebRequest
In diesem Beispiel wird gezeigt, wie Sie eine protokollspezifische Klasse registrieren, die an anderer Stelle definiert ist. In diesem Beispiel stellt `CustomWebRequestCreator` das vom Benutzer implementierte Objekt dar, das die **Create**-Methode implementiert, die wiederum das `CustomWebRequest`-Objekt zurückgibt. Im Codebeispiel wird vorausgesetzt, dass Sie den `CustomWebRequest`-Code geschrieben haben, der das benutzerdefinierte Protokoll implementiert.  
  
## <a name="example"></a>Beispiel  
  
```csharp  
WebRequest.RegisterPrefix("custom", new CustomWebRequestCreator());  
WebRequest req = WebRequest.Create("custom://customHost.contoso.com/");  
```  
  
```vb  
WebRequest.RegisterPrefix("custom", New CustomWebRequestCreator())  
Dim req As WebRequest = WebRequest.Create("custom://customHost.contoso.com/")  
```  
  
## <a name="compiling-the-code"></a>Kompilieren des Codes  
 Für dieses Beispiel benötigen Sie Folgendes:  
  
 Verweise auf den Namespace <xref:System.Net>  
  
## <a name="see-also"></a>Siehe auch  
 [Programmieren austauschbarer Protokolle](../../../docs/framework/network-programming/programming-pluggable-protocols.md)
