---
title: Auswählen zwischen DateTime, DateTimeOffset, TimeSpan und TimeZoneInfo
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTimeOffset structure
- TimeZoneInfo class
- time zones [.NET Framework], common uses
- date and time classes [.NET Framework]
- time zones [.NET Framework], type options
- DateTime structure
ms.assetid: 07f17aad-3571-4014-9ef3-b695a86f3800
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 368884e7f61f4504c8ca714165c543b19b3a1171
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="choosing-between-datetime-datetimeoffset-timespan-and-timezoneinfo"></a>Auswählen zwischen "DateTime", "DateTimeOffset", "TimeSpan" und "TimeZoneInfo"

.NET-Anwendungen, die Datums- und Uhrzeitinformationen verwenden, sind sehr vielfältig und können diese Informationen auf verschiedene Weise verwenden. Die häufigeren Verwendungsarten von Datums- und Uhrzeitinformationen sind mindestens eine der folgenden:

* Darstellen eines reinen Datums, damit Zeitinformationen unberücksichtigt bleiben.

* Darstellen einer reinen Uhrzeit, damit Datumsinformationen unberücksichtigt bleiben.

* Darstellen eines abstrakten Datums mit Uhrzeit, die an keine bestimmte Zeit und keinen bestimmten Ort gebunden sind (z. B. öffnen die meisten Geschäfte einer internationalen Kette an Wochentagen um 9:00 Uhr).

* Zum Abrufen von Datums-und Uhrzeitinformationen aus Quellen außerhalb von .NET in der Regel, in denen Datums-und Uhrzeitinformationen in einem einfachen gespeichert ist Datentyp.

* Eindeutiges und unzweideutiges Identifizieren eines einzigen Zeitpunkts. Einige Anwendungen erfordern, dass ein Datum und eine Uhrzeit eindeutig sind, nur auf dem Hostsystem. Andere erfordern, dass sie über Systeme hinweg eindeutig sind (d. h. ein auf dem einen System serialisiertes Datum kann weltweit auf einem anderen System sinnvoll deserialisiert und verwendet werden).

* Erhalten mehrerer verwandter Zeiten (z. B. die lokale Zeit des Anforderers und die Empfangszeit des Servers für eine Webanforderung).

* Durchführen von Datums- und Uhrzeitberechnungen, möglicherweise mit einem Ergebnis, das einen einzigen Zeitpunkt eindeutig identifiziert.

.NET enthält die <xref:System.DateTime>, <xref:System.DateTimeOffset>, <xref:System.TimeSpan>, und <xref:System.TimeZoneInfo> Typen, die alle zum Erstellen von Anwendungen, die mit Datumsangaben und Uhrzeiten arbeiten verwendet werden können.

> [!NOTE]
> In diesem Thema wird kein vierter Typ, <xref:System.TimeZone>, behandelt, weil seine Funktionalität nahezu vollständig in der <xref:System.TimeZoneInfo> -Klasse enthalten ist. Nach Möglichkeit sollten Entwickler die <xref:System.TimeZoneInfo> -Klasse anstelle der <xref:System.TimeZone> -Klasse verwenden.

## <a name="the-datetime-structure"></a>Die DateTime-Struktur

Ein <xref:System.DateTime> -Wert definiert ein bestimmtes Datum und eine Uhrzeit. Er enthält eine <xref:System.DateTime.Kind%2A> -Eigenschaft, bietet eingeschränkte Informationen über die Zeitzone, zu der dieses Datum und die Uhrzeit gehören. Der <xref:System.DateTimeKind> Rückgabewert von der <xref:System.DateTime.Kind%2A> Eigenschaft gibt an, ob der <xref:System.DateTime> Wert die Ortszeit darstellt (<xref:System.DateTimeKind.Local?displayProperty=nameWithType>), koordinierte Weltzeit (UTC) (<xref:System.DateTimeKind.Utc?displayProperty=nameWithType>), oder eine unspezifische Uhrzeit (<xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>).

Die <xref:System.DateTime> -Struktur eignet sich für Anwendungen, die Folgendes können:

* Nur mit Daten arbeiten.

* Nur mit Uhrzeiten arbeiten.

* Mit abstrakten Datums- und Uhrzeitwerten arbeiten.

* Mit Datums- und Uhrzeitwerten arbeiten, für die Zeitzoneninformationen fehlen.

* Nur mit UTC-Datums- und Uhrzeitwerten arbeiten.

* Abrufen von Datums-und Uhrzeitinformationen aus Quellen außerhalb von .NET, z. B. SQL-Datenbanken. In der Regel speichern diese Quellen Datums- und Uhrzeitinformationen in einem einfachen Format, das mit der <xref:System.DateTime> -Struktur kompatibel ist.

* Arithmetische Operationen mit Datums- und Uhrzeitwerten durchführen, wobei aber allgemeine Ergebnisse von Belang sind. Beispielsweise ist es bei einer Additionsoperation, bei der einem bestimmten Datum und einer Uhrzeit sechs Monate hinzuaddiert werden, oft nicht wichtig, ob das Ergebnis hinsichtlich der Sommerzeit angepasst wird.

Wenn nicht ein bestimmter <xref:System.DateTime> -Wert UTC darstellt, ist dieser Datums- und Uhrzeitwert häufig mehrdeutig oder in seiner Portierbarkeit eingeschränkt. Wenn z. B. ein <xref:System.DateTime> -Wert die lokale Uhrzeit darstellt, ist er innerhalb dieser lokalen Zeitzone portierbar (d. h., wenn der Wert auf einem anderen System in derselben Zeitzone deserialisiert wird, identifiziert dieser Wert immer noch eindeutig einen einzigen Zeitpunkt). Außerhalb der lokalen Zeitzone kann dieser <xref:System.DateTime> -Wert über mehrere Interpretationen verfügen. Wenn die <xref:System.DateTime.Kind%2A>-Eigenschaft des Werts <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> ist, ist er sogar noch weniger portierbar: Er ist jetzt innerhalb derselben Zeitzone mehrdeutig und möglicherweise sogar auf dem selben System, auf dem er erstmalig serialisiert wurde. Nur wenn ein <xref:System.DateTime> -Wert eine UTC-Zeit darstellt, identifiziert dieser Wert eindeutig einen einzigen Zeitpunkt, unabhängig vom System oder der Zeitzone, in der der Wert verwendet wird.

> [!IMPORTANT]
> Beim Speichern oder Freigeben von <xref:System.DateTime>-Daten sollte UTC verwendet werden, und die <xref:System.DateTime>-<xref:System.DateTime.Kind%2A>-Eigenschaft des Werts sollte auf <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> festgelegt werden.

## <a name="the-datetimeoffset-structure"></a>Die DateTimeOffset-Struktur

Die <xref:System.DateTimeOffset> -Struktur stellt einen Datums- und Uhrzeitwert zusammen mit einem Offset dar, der angibt, um wie viel dieser Wert von UTC abweicht. Somit identifiziert der Wert immer eindeutig einen einzigen Zeitpunkt.

Der <xref:System.DateTimeOffset> -Typ bietet die gesamte Funktionalität des <xref:System.DateTime> -Typs plus Unterstützung von Zeitzonen. Dies ist das geeignet für Anwendungen, die wie folgt vorgehen:

* Eindeutiges und unzweideutiges Identifizieren eines einzigen Zeitpunkts. Der <xref:System.DateTimeOffset> -Typ kann zur eindeutigen Definition der Bedeutung von "jetzt" verwendet werden, um Transaktionszeiten zu protokollieren, die Zeiten von System- oder Anwendungsereignissen zu protokollieren und um die Zeiten der Erstellung und Änderung von Dateien aufzuzeichnen.

* Ausführen von allgemeinen Datums- und Uhrzeitberechnungen

* Erhalten mehrerer verwandter Uhrzeiten, solange diese Zeiten als zwei gesonderte Werte oder als zwei Member einer Struktur gespeichert werden.

> [!NOTE]
> Diese Verwendungsarten für <xref:System.DateTimeOffset> -Werte sind sehr viel häufiger als die für <xref:System.DateTime> -Werte. Demzufolge sollte <xref:System.DateTimeOffset> als Standardtyp für Datum und Uhrzeit für die Anwendungsentwicklung angesehen werden.

Ein <xref:System.DateTimeOffset> -Wert ist nicht an eine bestimmte Zeitzone gebunden, kann aber aus jeder der zahlreichen Zeitzonen stammen. Um dies zu veranschaulichen, listet das folgende Beispiel die Zeitzonen auf, zu denen eine Reihe von <xref:System.DateTimeOffset> -Werten (einschließlich eines Werts in lokaler Pacific Normalzeit) gehören können.

[!code-csharp[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual1.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual1.vb#1)]

Die Ausgabe zeigt, dass jeder Datums- und Uhrzeitwert in diesem Beispiel zu mindestens drei verschiedenen Zeitzonen gehören kann. Der <xref:System.DateTimeOffset> -Wert "6/10/2007" zeigt, dass, wenn ein Datums- und Uhrzeitwert eine Sommerzeit darstellt, sein Offset von UTC noch nicht einmal unbedingt dem UTC-Basisoffset der Ursprungszeitzone oder dem in seinem Anzeigenamen vorgefundenen Offset von UTC entsprechen muss. Dies bedeutet, dass, weil ein einzelner <xref:System.DateTimeOffset> -Wert nicht eng mit seiner Zeitzone verknüpft ist, er nicht den Übergang einer Zeitzone zur und aus der Sommerzeit wiedergeben kann. Dies kann besonders problematisch sein, wenn ein <xref:System.DateTimeOffset> -Wert mithilfe von Datums- und Uhrzeitberechnungen manipuliert wird. (Eine Erläuterung der Durchführung von Datums- und Uhrzeitberechnungen auf eine Weise, die die Anpassungsregeln einer Zeitzone berücksichtigt, finden Sie unter [Performing arithmetic operations with dates and times](../../../docs/standard/datetime/performing-arithmetic-operations.md).)

## <a name="the-timespan-structure"></a>Die TimeSpan-Struktur

Die <xref:System.TimeSpan> -Struktur stellt ein Zeitintervall dar. Sein zwei typischen Anwendungsmöglichkeiten sind:

* Darstellen des Zeitintervalls zwischen zwei Datums- und Uhrzeitwerten. Beispielsweise gibt die Subtraktion eines <xref:System.DateTime> -Werts von einem anderen einen <xref:System.TimeSpan> -Wert zurück.

* Messen der verstrichenen Zeit. Z. B. die <xref:System.Diagnostics.Stopwatch.Elapsed%2A?displayProperty=nameWithType> Eigenschaft gibt eine <xref:System.TimeSpan> -Wert, der das Zeitintervall angibt, die seit dem Aufrufen einer der vergangenen der <xref:System.Diagnostics.Stopwatch> Methoden, die verstrichene Zeit zu messen beginnen.

Ein <xref:System.TimeSpan> -Wert kann auch als Ersatz für einen <xref:System.DateTime> -Wert verwendet werden, wenn dieser Wert eine Uhrzeit ohne Verweis auf eine bestimmte Tageszeit widerspiegelt. Diese Verwendung ähnelt den <xref:System.DateTime.TimeOfDay%2A?displayProperty=nameWithType> und <xref:System.DateTimeOffset.TimeOfDay%2A?displayProperty=nameWithType> Eigenschaften, die Zurückgeben einer <xref:System.TimeSpan> -Wert, der die Uhrzeit ohne Verweis auf ein Datum darstellt. Beispielsweise kann die <xref:System.TimeSpan> -Struktur verwendet werden, um die täglichen Öffnungszeiten eines Geschäfts darzustellen oder um die Uhrzeit darzustellen, zu der alle regulären Ereignisse auftreten.

Das folgende Beispiel definiert eine `StoreInfo` -Struktur, die <xref:System.TimeSpan> -Objekte für Öffnungszeiten von Geschäften enthält sowie ein <xref:System.TimeZoneInfo> -Objekt, das die Zeitzone des Geschäfts darstellt. Die Struktur enthält außerdem zwei Methoden, `IsOpenNow` und `IsOpenAt`, die angeben, ob das Geschäft zu einem vom Benutzer angegebenen Zeitpunkt geöffnet ist, wobei angenommen wird, dass er sich in der lokalen Zeitzone aufhält.

[!code-csharp[Conceptual.ChoosingDates#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#1)]
[!code-vb[Conceptual.ChoosingDates#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#1)]

Die `StoreInfo` -Struktur kann dann von Clientcode wie folgt verwendet werden.

[!code-csharp[Conceptual.ChoosingDates#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#2)]
[!code-vb[Conceptual.ChoosingDates#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#2)]

## <a name="the-timezoneinfo-class"></a>Die TimeZoneInfo-Klasse

Die <xref:System.TimeZoneInfo> class represents any of the Earth's time zones, and enables the conversion of any date and time in one time zone to its equivalent in another time zone. Die <xref:System.TimeZoneInfo> -Klasse ermöglicht das Arbeiten mit Datums- und Zeitwerten, sodass jeder Datums- und Uhrzeitwert eindeutig einen einzigen Zeitpunkt identifiziert. Die <xref:System.TimeZoneInfo> -Klasse ist außerdem erweiterbar. Obwohl sie von den für Windows-Systeme bereitgestellten und in der Registrierung definierten Zeitzoneninformationen abhängt, unterstützt sie die Erstellung benutzerdefinierter Zeitzonen. Sie unterstützt außerdem die Serialisierung und Deserialisierung von Zeitzoneninformationen.

In einigen Fällen kann noch weitere Entwicklungsarbeit erforderlich sein, um die <xref:System.TimeZoneInfo> -Klasse optimal zu nutzen. Wenn die Datums-und Uhrzeitwerte nicht eng verknüpft sind mit den Zeitzonen, zu dem sie gehören, weiter arbeiten, ist erforderlich. Wenn Ihre Anwendung einen Mechanismus zum Verknüpfen von Datum und Uhrzeit mit der zugehörigen Zeitzone bietet, ist es einfach für ein bestimmtes Datum und die Time-Werten zu seiner Zeitzone aufgehoben werden. Eine Methode zum Verknüpfen dieser Informationen besteht darin, eine Klasse oder Struktur zu definieren, die sowohl den Datums- und Zeitwert als auch sein zugeordnetes Zeitzonenobjekt enthält.

Die Zeitzonenunterstützung in .NET kann nur genutzt werden, wenn die Zeitzone, zu der ein Datums- und Uhrzeitwert gehört, bekannt ist, wenn das Datums- und Uhrzeitobjekt instanziiert wird. Dies ist häufig nicht der Fall, insbesondere bei Web-oder Netzwerkanwendungen.

## <a name="see-also"></a>Siehe auch

[Datumsangaben, Uhrzeiten und Zeitzonen](../../../docs/standard/datetime/index.md)
