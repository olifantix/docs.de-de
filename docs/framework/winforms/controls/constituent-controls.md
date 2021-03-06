---
title: Konstituierende Steuerelemente
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [Windows Forms], constituent controls
- constituent controls [Windows Forms]
- user controls [Windows Forms], constituent controls
ms.assetid: 5565e720-198b-4bbd-a2bd-c447ba641798
ms.openlocfilehash: 6fb708b81089b4fcd3678b35d1bcf7da2244c6d1
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="constituent-controls"></a>Konstituierende Steuerelemente
Die Steuerelemente, aus denen ein Benutzersteuerelement gebildet wird, werden als *konstituierende Steuerelemente* bezeichnet. Sie verhalten sich beim Rendering benutzerdefinierter Grafiken relativ unflexibel. Alle Windows Forms-Steuerelementen behandeln, ihre eigenen Rendering über ihre eigenen <xref:System.Windows.Forms.Control.OnPaint%2A> Methode. Da diese Methode geschützt ist, kann der Entwickler nicht auf sie zugreifen. Daher kann nicht verhindert werden, dass die Methode ausgeführt wird, sobald ein Steuerelement gezeichnet wird. Das bedeutet jedoch nicht, dass kein Code hinzugefügt werden kann, um die Darstellung konstituierender Steuerelemente zu beeinflussen. Zusätzliches Rendering kann ermöglicht werden, indem ein Ereignishandler hinzugefügt wird. Nehmen wir beispielsweise an, die Sie erstellen eine <xref:System.Windows.Forms.UserControl> mit einer Schaltfläche mit dem Namen `MyButton`. Wenn Sie zusätzliche gerendert hinausgeht, was durch bereitgestellt wurde die <xref:System.Web.UI.WebControls.Button>, fügen Sie Code zum Benutzersteuerelement ähnlich der folgenden:  
  
```vb  
Public Sub MyPaint(ByVal sender as Object, e as PaintEventArgs) Handles _  
   MyButton.Paint  
   'Additional rendering code goes here  
End Sub  
```  
  
```csharp  
// Add the event handler to the button's Paint event.  
MyButton.Paint +=   
   new System.Windows.Forms.PaintEventHandler (this.MyPaint);  
// Create the custom painting method.  
protected void MyPaint (object sender,   
System.Windows.Forms.PaintEventArgs e)  
{  
   // Additional rendering code goes here.  
}  
```  
  
> [!NOTE]
>  Einige Windows Forms-Steuerelemente, z. B. <xref:System.Windows.Forms.TextBox>, direkt von Windows gezeichnet werden. In diesen Fällen die <xref:System.Windows.Forms.Control.OnPaint%2A> wird nie aufgerufen, und daher im obigen Beispiel wird nie aufgerufen werden.  
  
 Hierdurch wird eine Methode erstellt, die jedes Mal ausgeführt wird, sobald das `MyButton.Paint`-Ereignis ausgeführt wird. So wird dem Steuerelement eine zusätzliche grafische Darstellung hinzugefügt. Beachten Sie, dass dadurch nicht die Ausführung von `MyButton.OnPaint` verhindert wird. Daher werden zusätzlich zu den benutzerdefinierten Zeichenvorgängen alle Zeichenvorgänge ausgeführt, die in der Regel über eine Schaltfläche erfolgen. Einzelheiten zu GDI+-Technologie und benutzerdefiniertem Rendering finden Sie unter [Erstellen von Grafiken mit GDI+](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md). Der beste Weg zum Erreichen einer einheitlichen Darstellung des Steuerelements besteht darin, ein geerbtes Steuerelement zu erstellen und Code zum benutzerdefinierten Ausgeben dieses Steuerelements zu schreiben. Einzelheiten dazu finden Sie unter [Benutzerdefinierte Steuerelemente](../../../../docs/framework/winforms/controls/user-drawn-controls.md).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.UserControl>  
 <xref:System.Windows.Forms.Control.OnPaint%2A>  
 [Benutzerdefinierte Steuerelemente](../../../../docs/framework/winforms/controls/user-drawn-controls.md)  
 [Gewusst wie: Erstellen von Grafikobjekten zum Zeichnen](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)  
 [Varieties of Custom Controls (Vielfalt benutzerdefinierter Steuerelemente)](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)
