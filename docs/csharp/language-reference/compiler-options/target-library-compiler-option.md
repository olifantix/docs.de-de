---
title: -target:library (C#-Compileroptionen)
ms.date: 07/20/2015
f1_keywords:
- /dll
helpviewer_keywords:
- -target compiler options [C#], /target:library
- target compiler options [C#], /target:library
- /target compiler options [C#], /target:library
ms.assetid: c5670e88-2126-47c1-8d1c-217923837d17
ms.openlocfilehash: 39f6ad5839f7ca12b023502a3fc1ccde52e70899
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="-targetlibrary-c-compiler-options"></a>-target:library (C#-Compileroptionen)
Die Option **-target:library** veranlasst den Compiler dazu, eine Dynamic Link Library (DLL) statt einer ausführbaren Datei (EXE) zu erstellen.  
  
## <a name="syntax"></a>Syntax  
  
```console  
-target:library  
```  
  
## <a name="remarks"></a>Hinweise  
 Die DLL wird mit der DLL-Dateiendung erstellt.  
  
 Sofern es nicht anders mit der Option [-out](../../../csharp/language-reference/compiler-options/out-compiler-option.md) angegeben wurde, erhält die Ausgabedatei den Namen der ersten Eingabedatei.  
  
 Wenn es in der Befehlszeile angegeben wurde, werden alle Dateien bis zur nächsten Option **-out** oder **-target:module** verwendet, um die DLL-Datei zu erstellen.  
  
 Beim Erstellen einer DLL-Datei ist eine [Main](../../../csharp/programming-guide/main-and-command-args/index.md)-Methode nicht erforderlich.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>So legen Sie diese Compileroption in der Visual Studio-Entwicklungsumgebung fest  
  
1.  Öffnen Sie die Seite **Eigenschaften** des Projekts.  
  
2.  Klicken Sie auf die Eigenschaftenseite **Anwendung**.  
  
3.  Ändern Sie die Eigenschaft **Ausgabetyp**.  
  
 Informationen zum programmgesteuerten Festlegen dieser Compileroption finden Sie unter <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## <a name="example"></a>Beispiel  
 Kompilieren Sie `in.cs`, und `in.dll` wird erstellt:  
  
```console  
csc -target:library in.cs  
```  
  
## <a name="see-also"></a>Siehe auch  
 [-target (C#-Compileroptionen)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)  
 [C#-Compileroptionen](../../../csharp/language-reference/compiler-options/index.md)
