---
title: Erstellen eines NuGet-Pakets mit plattformübergreifenden Tools
description: Erfahren Sie, wie Sie ein NuGet-Paket mit dem Befehl „dotnet pack“ erstellen.
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.technology: dotnet-cli
ms.openlocfilehash: 6be94c2e2cef443f69b2d6df7c2d490cb1fb629d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-create-a-nuget-package-with-cross-platform-tools"></a>So erstellen Sie ein NuGet-Paket mit plattformübergreifenden Tools

> [!NOTE]
> Nachfolgend einige Befehlszeilenbeispiele unter Unix.  Der hier gezeigte Befehl `dotnet pack` funktioniert wie unter Windows.

Bibliotheken sollten für .NET Core 1.0 als NuGet-Pakete verteilt werden.  So werden alle .NET Standardbibliotheken verteilt und genutzt.  Am einfachsten geht dies mit dem Befehl `dotnet pack`.

Stellen Sie sich vor, dass Sie eine fantastische neue Bibliothek geschrieben haben, die Sie über NuGet verteilen möchten.  Sie können hierfür ein NuGet-Paket mit plattformübergreifenden Tools erstellen.  Als Beispiel dient eine Bibliothek namens **SuperAwesomeLibrary** für `netstandard1.0`.

Wenn Sie transitive Abhängigkeiten haben, das heißt ein Projekt, das von einem anderen Projekt abhängig ist, müssen Sie sicherstellen, dass Pakete für die gesamte Projektmappe mit dem Befehl `dotnet restore` wiederhergestellt werden, bevor das NuGet-Paket erstellt wird.  Andernfalls wird der Befehl `dotnet pack` nicht ordnungsgemäß funktionieren.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]


Nachdem Sie sichergestellt haben, dass Pakete wiederhergestellt wurden, können Sie zu dem Verzeichnis navigieren, in dem sich eine Bibliothek befindet:

`$ cd src/SuperAwesomeLibrary`

Anschließend genügt ein einzelner Befehl von der Befehlszeile:
    
`$ dotnet pack`

Ihr Ordner `/bin/Debug` sieht nun wie folgt aus:

```
$ ls bin/Debug

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

Beachten Sie, dass dies ein Paket erzeugt, das debuggt werden kann.  Wenn Sie ein NuGet-Paket mit Release-Binärdateien erstellen möchten, müssen Sie lediglich den Schalter `-c`/`--configuration` und das Argument `release` verwenden.

`$ dotnet pack --configuration release`

Ihr Ordner `/bin` hat nun einen Unterordner `release` mit dem NuGet-Paket und den Release-Binärdateien:

```
$ ls bin/release

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

Jetzt haben Sie die erforderlichen Dateien zum Veröffentlichen eines NuGet-Pakets.

## <a name="dont-confuse-dotnet-pack-with-dotnet-publish"></a>Verwechseln Sie nicht `dotnet pack` mit `dotnet publish`

Es ist wichtig zu beachten, dass zu keinem Zeitpunkt der Befehl `dotnet publish` beteiligt ist.  Der Befehl `dotnet publish` dient der Bereitstellung von Clientanwendungen mit allen Abhängigkeiten im gleichen Paket – nicht für das Generieren eines NuGet-Pakets, das über NuGet verteilt und genutzt wird.
