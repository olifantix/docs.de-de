---
title: Grundlagen des verwalteten Threadings
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple threads
- threading [.NET Framework], multiple threads
- threading [.NET Framework], about threading
- managed threading
ms.assetid: b2944911-0e8f-427d-a8bb-077550618935
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 035834959aa5f9340727327b22cae93b3f21b056
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="managed-threading-basics"></a>Grundlagen des verwalteten Threadings
Die ersten fünf Themen in diesem Abschnitt sollen Ihnen helfen, zu bestimmen, wann Sie verwaltetes Threading verwenden sollten, und einige grundlegende Funktionen erläutern. Informationen zu den Klassen, die zusätzliche Funktionen bereitstellen, finden Sie unter [Threadingobjekte und -funktionen](../../../docs/standard/threading/threading-objects-and-features.md) und [Übersicht über Synchronisierungsprimitiven](../../../docs/standard/threading/overview-of-synchronization-primitives.md).  
  
 Bei den übrigen Themen in diesem Abschnitt handelt es sich um erweiterte Themen einschließlich der Interaktion verwalteten Threadings mit dem Windows-Betriebssystem.  
  
> [!NOTE]
>  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] stellen Task Parallel Library und PLINQ APIs für Aufgaben- und Datenparallelität in Multithreaded-Programmen bereit. Weitere Informationen finden Sie unter [Parallel Programming in the .NET Framework (Parallele Programmierung in .NET Framework)](../../../docs/standard/parallel-programming/index.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Threads and Threading (Threads und Threading)](../../../docs/standard/threading/threads-and-threading.md)  
 Erläutert die Vor- und Nachteile von mehreren Threads und beschreibt die Szenarien, in denen Sie Threads erstellen oder Threads aus Threadpools verwenden sollten.  
  
 [Ausnahmen in verwalteten Threads](../../../docs/standard/threading/exceptions-in-managed-threads.md)  
 Beschreibt das Verhalten der nicht behandelten Ausnahmen in Threads für verschiedene Versionen von .NET Framework, insbesondere die Situationen, in denen sie zum Beenden der Anwendung führen.  
  
 [Datensynchronisierung für Multithreading](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)  
 Beschreibt Strategien zum Synchronisieren von Daten in Klassen, die mit mehreren Threads verwendet werden.  
  
 [Zustände von verwalteten Threads](../../../docs/standard/threading/managed-thread-states.md)  
 Beschreibt die grundlegenden Threadzustände und erklärt, wie Sie ermitteln, ob ein Thread ausgeführt wird.  
  
 [Vordergrund- und Hintergrundthreads](../../../docs/standard/threading/foreground-and-background-threads.md)  
 Erläutert die Unterschiede zwischen Vordergrund-und Hintergrundthreads.  
  
 [Verwaltetes und nicht verwaltetes Threading in Windows](../../../docs/standard/threading/managed-and-unmanaged-threading-in-windows.md)  
 Beschreibt die Beziehung zwischen verwaltetem und nicht verwaltetem Threading, listet verwaltete Entsprechungen für Windows-Threading-APIs auf und erläutert die Interaktion von COM-Apartments und verwalteten Threads.  
  
 [Thread.Suspend, Garbage Collection und Sicherungspunkte](../../../docs/standard/threading/thread-suspend-garbage-collection-and-safe-points.md)  
 Beschreibt Anhalten von Threads und Garbage Collection.  
  
 [Threadlokaler Speicher: Threadbezogene statische Felder und Datenslots](../../../docs/standard/threading/thread-local-storage-thread-relative-static-fields-and-data-slots.md)  
 Beschreibt threadbezogene Speichermechanismen.  
  
 [Abbruch in verwalteten Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)  
 Beschreibt, wie asynchrone oder lang andauernde synchrone Vorgänge mit einem Abbruchtoken abgebrochen werden können.  
  
## <a name="reference"></a>Verweis  
 <xref:System.Threading.Thread>  
 Stellt die Referenzdokumentation für die **Thread**-Klasse bereit, die einen verwalteten Thread repräsentiert, und zwar unabhängig davon, ob er von nicht verwaltetem Code stammt oder in einer verwalteten Anwendung erstellt wurde.  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 Bietet eine sichere Möglichkeit zum Implementieren von Multithreading in Verbindung mit Benutzeroberflächenobjekten.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
 [Übersicht über Synchronisierungsprimitiven](../../../docs/standard/threading/overview-of-synchronization-primitives.md)  
 Beschreibt die verwalteten Klassen, die zum Synchronisieren mehrerer Threads verwendet werden.  
  
 [Empfohlene Vorgehensweise für das verwaltete Threading](../../../docs/standard/threading/managed-threading-best-practices.md)  
 Beschreibt allgemeine Probleme mit Multithreading und Strategien zur Vermeidung von Problemen.  
  
 [Parallele Programmierung](../../../docs/standard/parallel-programming/index.md)  
 Beschreibt Task Parallel Library und PLINQ, die das Erstellen von asynchronen und Multithreaded-.NET Framework-Anwendungen erheblich vereinfachen.
