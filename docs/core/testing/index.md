---
title: Unittests in .NET Core
description: Komponententests waren nie einfacher. Erfahren Sie, wie Komponententests in .NET Core- und .NET Standard-Projekten verwendet werden.
author: ardalis
ms.author: wiwagn
ms.date: 08/30/2017
ms.openlocfilehash: b3d8393cf285eae3493328b16c3dc038af208da6
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="unit-testing-in-net-core-and-net-standard"></a>Komponententests in .NET Core und .NET Standard

.NET Core wurde mit Prüfbarkeit als Hintergedanke entwickelt, sodass das Erstellen von Unittests für Ihre Anwendung einfacher als je zuvor ist. Dieser Artikel gibt eine kurze Einführung zu Unittests (und wie sich diese von anderen Arten von Tests unterscheiden). Verknüpfte Ressourcen zeigen, wie ein Testprojekt einer Lösung zugeordnet wird und anschließend Komponententests mithilfe der Befehlszeile oder Visual Studio ausgeführt werden.

.NET Core 2.0 unterstützt [.NET Standard 2.0](../../standard/net-standard.md). Die zur Demonstration der Komponententests in diesem Abschnitt verwendeten Bibliotheken basieren auf .NET Standard und funktionieren auch in anderen Projekttypen.

Ab .NET Core 2.0 sind Komponententest-Projektvorlagen sowohl für Visual Basic und F# als auch C# verfügbar.

## <a name="getting-started-with-testing"></a>Erste Schritte mit Tests

Eine Suite von automatisierten Tests ist eine der besten Möglichkeiten, um sicherzustellen, dass eine Softwareanwendung das tut, was von den Autoren verlangt wurde. Es gibt verschiedene Arten von Tests für Softwareanwendungen, einschließlich Integrationstests, Webtests, Auslastungstests und Sonstige. Komponententests, die einzelne Softwarekomponenten oder Methoden testen, sind Tests auf der untersten Ebene. Unittests sollen nur Code im Steuerelement des Entwicklers testen und nicht Infrastrukturprobleme wie z.B. Datenbanken, Dateisysteme oder Netzwerkressourcen. Unittests können mithilfe der [testgesteuerten Entwicklung](http://deviq.com/test-driven-development/) (Test Driven Development, TDD) geschrieben werden, oder sie können einem vorhandenen Code hinzugefügt werden, um dessen Richtigkeit zu bestätigen. In beiden Fällen sollten sie klein, gut benannt und schnell sein, da Sie im Idealfall hunderte davon ausführen möchten, bevor Sie Ihre Änderungen dem freigegebenen Coderepository des Projekts übergeben.

> [!NOTE]
> Entwickler haben oft Probleme bei der Benennung für ihre Testklassen und Methoden. Als Ausgangspunkt befolgt das ASP.NET-Produktteam [diesen Konventionen](https://github.com/aspnet/Home/wiki/Engineering-guidelines#unit-tests-and-functional-tests).

Wenn Sie Unittests schreiben, achten Sie darauf, dass Sie nicht versehentlich Abhängigkeiten der Infrastruktur einführen. Dies führt in der Regel dazu, dass Tests langsamer und anfälliger sind und sollten deshalb für Integrationstests reserviert werden. Sie können diese versteckten Abhängigkeiten in Ihrem Anwendungscode vermeiden, indem Sie das [Explicit Dependencies Principle (Explizites Abhängigkeitsprinzip)](http://deviq.com/explicit-dependencies-principle/) befolgen und [Dependency Injection (Abhängigkeitseinfügung)](/aspnet/core/fundamentals/dependency-injection) verwenden, um Ihre Abhängigkeiten vom Framework anzufordern. Sie können Ihre Unittests auch auf ein separates Projekt von Ihren Integrationstests beschränken, und sicherstellen, dass Ihr Unittestprojekt nicht über Referenzen für oder Abhängigkeiten auf den Infrastrukturpaketen verfügt.

Möchten Sie mehr über Unittests in .NET Core-Projekten erfahren?

Komponententestprojekte für .NET Core werden für [C#](../../csharp/index.md), [F#](../../fsharp/index.md) und [Visual Basic](../../visual-basic/index.md) unterstützt. Sie können außerdem zwischen [xUnit](http://xunit.github.io), [NUnit](http://nunit.org) und [MSTest](https://github.com/Microsoft/vstest-docs) wählen.

Sie können sich anhand dieser exemplarischen Vorgehensweisen über diese Kombinationen informieren:

* Erstellen von Komponententests mit [*XUnit* und *C#* mit der .NET Core-CLI](unit-testing-with-dotnet-test.md).
* Erstellen von Komponententests mit [*NUnit* und *C#* mit der .NET Core-CLI](unit-testing-with-nunit.md).
* Erstellen von Komponententests mit [*MSTest* und *C#* mit der .NET Core-CLI](unit-testing-with-mstest.md).
* Erstellen von Komponententests mit [*XUnit* und *F#* mit der .NET Core-CLI](unit-testing-fsharp-with-dotnet-test.md).
* Erstellen von Komponententests mit [*NUnit* und *F#* mit der .NET Core-CLI](unit-testing-fsharp-with-nunit.md).
* Erstellen von Komponententests mit [*MSTest* und *F#* mit der .NET Core-CLI](unit-testing-fsharp-with-mstest.md).
* Erstellen von Komponententests mit [*XUnit* und *Visual Basic* mit der .NET Core-CLI](unit-testing-visual-basic-with-dotnet-test.md).
* Erstellen von Komponententests mit [*NUnit* und *Visual Basic* mit der .NET Core-CLI](unit-testing-visual-basic-with-nunit.md).
* Erstellen von Komponententests mit [*MSTest* und *Visual Basic* mit der .NET Core-CLI](unit-testing-visual-basic-with-mstest.md).

Sie können verschiedene Sprachen für Ihre Klassenbibliotheken und Komponententestbibliotheken auswählen. Durch Mischen und Abstimmen der oben beschriebenen exemplarischen Vorgehensweisen können Sie Erfahrungen sammeln.

* Visual Studio Enterprise bietet nützliche Testtools für .NET Core. Weitere Informationen finden Sie in den Artikel zu [Live Unit Testing](/visualstudio/test/live-unit-testing) und [Codeabdeckung](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md#working-with-code-coverage).
* Weitere Informationen und Beispiele für die Verwendung der selektiven Komponententestfilterung finden Sie unter [Ausführen von selektiven Komponententests](selective-unit-tests.md) oder [Including and excluding test projects and test methods](/visualstudio/test/live-unit-testing#including-and-excluding-test-projects-and-test-methods) (Einbeziehen und Ausschließen von Testprojekten und Testmethoden).
* Das XUnit-Team hat ein Tutorial geschrieben, das zeigt, [how to use xUnit with .NET Core and Visual Studio (wie xUnit mit .NET Core und Visual Studio verwendet wird)](http://xunit.github.io/docs/getting-started-dotnet-core.html).
