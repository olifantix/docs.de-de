---
title: -bugreport
ms.date: 03/08/2018
helpviewer_keywords:
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
ms.openlocfilehash: 0383a5e369ee4a8146764c13b2f12f48ebe52190
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="-bugreport"></a>-bugreport
Erstellt eine Datei, die Sie verwenden können, wenn Sie einen Fehlerbericht einreichen.  
  
## <a name="syntax"></a>Syntax  
  
```  
-bugreport:file  
```  
  
## <a name="arguments"></a>Argumente  
  
|Begriff|Definition|  
|---|---|  
|`file`|Erforderlich. Der Name der Datei, die den Problembericht enthalten wird. Setzen Sie den Dateinamen in Anführungszeichen (""), wenn der Name ein Leerzeichen enthält.|  
  
## <a name="remarks"></a>Hinweise  
 Die folgende Informationen hinzugefügt `file`:  
  
-   Eine Kopie des alle Quellcodedateien in der Kompilierung.  
  
-   Eine Liste der Compileroptionen, die in der Kompilierung verwendet werden soll.  
  
-   Versionsinformationen zur Compiler, common Language Runtime und Betriebssystem.  
  
-   Compilerausgabe, falls vorhanden.  
  
-   Eine Beschreibung des Problems ist, für die Sie dazu aufgefordert werden.  
  
-   Eine Beschreibung, wie Sie das Problem vermuten sollten korrigiert werden, für die Sie dazu aufgefordert werden.  
  
 Da eine Kopie für alle Quellcodedateien in enthalten ist `file`, Sie möchten den (vermuteten) Codefehler in der kürzestmöglichen Programm zu reproduzieren.  
  
> [!IMPORTANT]
>  Die `-bugreport` Option erstellt eine Datei, die möglicherweise vertrauliche Informationen enthält. Dies schließt die aktuelle Uhrzeit, Compilerversion, [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] Version, Betriebssystemversion, Benutzername, die Befehlszeilenargumente, mit denen der Compiler ausgeführt wurde, werden alle Quellcode, und die binäre Form eines referenzierten Assemblys. Diese Option kann zugegriffen werden, durch Angabe von Befehlszeilenoptionen in der Datei "Web.config" für eine serverseitige Kompilierung einer [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] Anwendung. Um dies zu verhindern, ändern Sie die Datei "Machine.config", um Benutzer an der Kompilierung auf dem Server zu unterbinden.  
  
 Wenn diese Option verwendet wird, mit `-errorreport:prompt`, `-errorreport:queue`, oder `-errorreport:send`, und die Anwendung erkennt, die Informationen in einen interner Compilerfehler `file` wird gesendet, um Microsoft Corporation. Diese Informationen helfen Microsoft-Experten, die die Ursache des Fehlers zu identifizieren und die nächste Version von Visual Basic zu verbessern. Standardmäßig werden keine Informationen an Microsoft gesendet. Allerdings beim Kompilieren einer Anwendung mit `-errorreport:queue`, die standardmäßig aktiviert ist, sammelt die Anwendung ihre Fehlerberichte. Klicken Sie dann bei dem Computer anmeldet, zeigt Berichtssystems Fehler ein Popup-Fenster, das ermöglicht dem Administrator die Weiterleitung an Microsoft, die alle Fehler meldet, die seit der Anmeldung aufgetreten sind.  
  
> [!NOTE]
>  Die `/bugreport` Option ist nicht innerhalb der Visual Studio-Entwicklungsumgebung verfügbar, steht er nur, wenn Sie über die Befehlszeile kompilieren.  
  
## <a name="example"></a>Beispiel  
 Im folgende Beispiel kompiliert `T2.vb` und alle Fehlerberichte Informationen in der Datei `Problem.txt`.  
  
```  
vbc -bugreport:problem.txt t2.vb  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Visual Basic-Befehlszeilencompiler](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-Debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)  
 [-errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)  
 [Beispiele für Kompilierungsbefehlszeilen](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [TrustLevel Element für SecurityPolicy ((ASP.NET Settings Schema)](http://msdn.microsoft.com/library/729ab04c-03da-4ee5-86b1-be9d08a09369)
