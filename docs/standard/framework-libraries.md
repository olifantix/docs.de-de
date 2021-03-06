---
title: Frameworkbibliotheken
description: "Erfahren Sie, wie diese Bibliotheken Implementierungen für viele allgemeine und App-spezifische Typen, Algorithmen und Hilfsprogrammfunktionen bereitstellen."
keywords: .NET, .NET Core
author: richlander
ms.author: ronpet
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 7b77b6c1-8367-4602-bff3-91e4c05ac643
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 9e792eefa551dacda7c01bb03a6035647de04a35
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="framework-libraries"></a>Frameworkbibliotheken

.NET verfügt über einen umfangreichen Standardsatz an Klassenbibliotheken, die entweder als Basisklassenbibliotheken (Kernsatz) oder Frameworkklassenbibliotheken (vollständiger Satz) bezeichnet werden. Diese Bibliotheken bieten Implementierungen für viele allgemeine und App-spezifische Typen, Algorithmen und Hilfsprogrammfunktionen. Sowohl kommerzielle als auch communitybasierte Bibliotheken bauen auf den Frameworkklassenbibliotheken auf und bieten einfache, sofort einsatzbereite Bibliotheken für eine Vielzahl von Computingaufgaben.

Eine Teilmenge dieser Bibliotheken wird mit jeder .NET-Implementierung bereitgestellt. BCL-APIs (Base Class Library, Basisklassenbibliothek) werden in jeder .NET-Implementierung vorausgesetzt, weil sie von Entwicklern gewünscht und von beliebten Bibliotheken für die Ausführung benötigt werden. Über die BCL hinausgehende App-spezifische Bibliotheken – wie z.B. ASP.NET – sind nicht in allen .NET-Implementierungen verfügbar.

## <a name="base-class-libraries"></a>Basisklassenbibliotheken

Basisklassenbibliotheken stellen die meisten grundlegenden Typen und Hilfsprogrammfunktionen bereit und bilden die Grundlage für alle anderen .NET-Klassenbibliotheken. Sie sind darauf ausgerichtet, sehr allgemeine Implementierungen anzubieten, ohne einer bestimmten Arbeitsauslastung den Vorzug zu geben. Leistung ist immer ein wichtiger Gesichtspunkt, da je nach App unterschiedliche Richtlinien ein höheres Gewicht haben – z.B. niedrige Latenz gegenüber hohem Durchsatz oder geringer Arbeitsspeicherverbrauch gegenüber geringer CPU-Auslastung. Diese Bibliotheken sind generell auf hohe Leistung ausgelegt und versuchen, angesichts all der verschiedenen Leistungsanforderungen einen Mittelweg zu finden. Für die meisten Apps funktioniert diese Herangehensweise ziemlich gut.

## <a name="primitive-types"></a>Primitive Typen

.NET umfasst eine Reihe primitiver Typen, die (in unterschiedlichem Maß) in allen Programmen verwendet werden. Diese Typen enthalten Daten, beispielsweise Zahlen, Zeichenfolgen, Bytes und beliebige Objekte. Die Sprache C# enthält Schlüsselwörter für diese Typen. Unten finden Sie einen Beispielsatz dieser Typen, zusammen mit den entsprechenden C#-Schlüsselwörtern.

* <xref:System.Object?displayProperty=nameWithType> ([object](../csharp/language-reference/keywords/object.md)): Die ultimative Basisklasse im CLR-Typsystem. Sie bildet den Stamm der Typhierarchie.
* <xref:System.Int16?displayProperty=nameWithType> ([short](../csharp/language-reference/keywords/short.md)): Ein ganzzahliger 16-Bit-Typ mit Vorzeichen. Es gibt auch einen <xref:System.UInt16>-Typ ohne Vorzeichen.
* <xref:System.Int32?displayProperty=nameWithType> ([int](../csharp/language-reference/keywords/int.md)): Ein 32-Bit-Ganzzahltyp mit Vorzeichen Es gibt auch einen [UInt32](../csharp/language-reference/keywords/uint.md)-Typ ohne Vorzeichen.
* <xref:System.Single?displayProperty=nameWithType> ([float](../csharp/language-reference/keywords/float.md)): Ein 32-Bit-Gleitkommatyp
* <xref:System.Decimal?displayProperty=nameWithType> ([decimal](../csharp/language-reference/keywords/decimal.md)): Ein 128-Bit-Dezimaltyp
* <xref:System.Byte?displayProperty=nameWithType> ([byte](../csharp/language-reference/keywords/byte.md)): Ein 8-Bit-Ganzzahltyp ohne Vorzeichen, der ein Byte des Arbeitsspeichers darstellt
* <xref:System.Boolean?displayProperty=nameWithType> ([bool](../csharp/language-reference/keywords/bool.md)): Ein boolescher Typ, der `true` oder `false` darstellt
* <xref:System.Char?displayProperty=nameWithType> ([char](../csharp/language-reference/keywords/char.md)): Ein numerischer 16-Bit-Typ, der ein Unicodezeichen darstellt
* <xref:System.String?displayProperty=nameWithType> ([string](../csharp/language-reference/keywords/string.md)): Stellt eine Reihe von Zeichen dar. Unterscheidet sich von `char[]`, ermöglicht aber die Indizierung für jedes einzelne `char` in der `string`.

## <a name="data-structures"></a>Datenstrukturen

.NET umfasst eine Reihe von Datenstrukturen, die die Arbeitsgrundlage für nahezu alle .NET-Apps darstellen. Die meisten sind Auflistungen, es gibt jedoch auch andere Typen.

*   <xref:System.Array>: Stellt ein Array aus stark typisierten Objekten dar, auf die über einen Index zugegriffen werden kann. Verfügt konstruktionsbedingt über eine festgelegte Größe.
*   <xref:System.Collections.Generic.List%601>: Stellt eine stark typisierte Liste von Objekten dar, auf die über einen Index zugegriffen werden kann. Die Größe wird nach Bedarf automatisch angepasst.
*   <xref:System.Collections.Generic.Dictionary%602>: Stellt eine Auflistung aus Werten dar, die durch einen Schlüssel indiziert werden. Auf die Werte kann über einen Schlüssel zugegriffen werden. Die Größe wird nach Bedarf automatisch angepasst.
*   <xref:System.Uri>: Stellt eine Objektdarstellung eines URIs (Uniform Resource Identifier) und einfachen Zugriff auf die Teile des URIs bereit.
*   <xref:System.DateTime>: Stellt einen Zeitpunkt dar, normalerweise durch Datum und Uhrzeit angegeben.

## <a name="utility-apis"></a>Hilfsprogramm-APIs

.NET umfasst eine Reihe von Hilfsprogramm-APIs, die Funktionen für viele wichtige Aufgaben bereitstellen.

*   <xref:System.Net.Http.HttpClient>: Eine API zum Senden von HTTP-Anforderungen und Empfangen von HTTP-Antworten aus einer Ressource, die durch einen URI identifiziert wird.
*   <xref:System.Xml.Linq.XDocument>: Eine API zum Laden und Abfragen von XML-Dokumenten mit LINQ.
*   <xref:System.IO.StreamReader>: Eine API zum Lesen von Dateien (<xref:System.IO.StringWriter>). Kann zum Schreiben von Dateien verwendet werden.

## <a name="app-model-apis"></a>App-Modell-APIs

Es gibt viele App-Modelle von unterschiedlichen Herstellern, die mit .NET verwendet werden können.

*   [ASP.NET](http://asp.net): Stellt ein Webframework zum Erstellen von Websites und -diensten bereit. Unterstützt unter Windows, Linux und macOS (je nach ASP.NET-Version).
