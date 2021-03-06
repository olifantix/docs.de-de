---
title: ICorProfilerInfo-Schnittstelle
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo
helpviewer_keywords:
- ICorProfilerInfo interface [.NET Framework profiling]
ms.assetid: eb4e4ce0-06e7-4469-bbc4-edc2eb5da4b1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: da5a041e8a18420b4cf9962e4315683be8857711
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="icorprofilerinfo-interface"></a>ICorProfilerInfo-Schnittstelle
Stellt Methoden für die Verwendung durch Codeprofiler für Kommunikation mit der common Language Runtime (CLR), um die ereignisüberwachung zu steuern und Informationen anzufordern.  
  
> [!NOTE]
>  Jede Methode in der `ICorProfilerInfo` Schnittstelle gibt ein HRESULT, um Erfolg oder Fehler anzeigt. Eine Liste möglicher Rückgabecodes finden Sie unter "CorError.h".  
  
## <a name="methods"></a>Methoden  
  
|Methode|Beschreibung|  
|------------|-----------------|  
|[BeginInprocDebugging-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-begininprocdebugging-method.md)|Initialisiert in-Process-debugging-Unterstützung. Diese Methode ist veraltet in .NET Framework, Version 2.0.|  
|[EndInprocDebugging-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-endinprocdebugging-method.md)|Fährt eine Debugsitzung für in-Process. Diese Methode ist veraltet in .NET Framework, Version 2.0.|  
|[ForceGC-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-forcegc-method.md)|Erzwingt eine Garbagecollection innerhalb der Runtime auftreten.|  
|[GetAppDomainInfo-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getappdomaininfo-method.md)|Ruft Informationen über die angegebene Anwendungsdomäne ab.|  
|[GetAssemblyInfo-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getassemblyinfo-method.md)|Ruft Informationen über die angegebene Assembly ab.|  
|[GetClassFromObject-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromobject-method.md)|Ruft die `ClassID` des ein<br /><br /> -Objekt, dessen `ObjectID`.|  
|[GetClassFromToken-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromtoken-method.md)|Ruft die ID der Klasse, mit dem angegebenen Metadatentoken ab. Diese Methode ist veraltet in .NET Framework, Version 2.0. Verwenden der [ICorProfilerInfo2:: GetClassFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassfromtokenandtypeargs-method.md) Methode stattdessen.|  
|[GetClassIDInfo-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassidinfo-method.md)|Ruft das übergeordnete Modul und das Metadatentoken für die angegebene Klasse ab.|  
|[GetCodeInfo-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcodeinfo-method.md)|Ruft den Wertebereich des nativen Codes ab, der der angegebenen Funktions-ID zugeordnet ist. Diese Methode ist veraltet. Verwenden der [ICorProfilerInfo2:: Getcodeinfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcodeinfo2-method.md) Methode stattdessen.|  
|[GetCurrentThreadID-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcurrentthreadid-method.md)|Ruft die ID des aktuellen Threads ab, wenn es sich um einen verwalteten Thread ist.|  
|[GetEventMask-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-geteventmask-method.md)|Ruft die aktuellen Ereigniskategorien, die für die der Profiler ereignisbenachrichtigungen von der CLR empfangen möchte.|  
|[GetFunctionFromIP-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromip-method.md)|Ordnet einen verwalteten Code Anweisungszeiger einen `FunctionID`.|  
|[GetFunctionFromToken-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromtoken-method.md)|Ruft die ID einer Funktion ab. Diese Methode ist veraltet in .NET Framework, Version 2.0. Verwenden der [ICorProfilerInfo2:: GetFunctionFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md) Methode stattdessen.|  
|[GetFunctionInfo-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctioninfo-method.md)|Ruft die übergeordnete Klasse und die Metadaten für die angegebene Funktion.|  
|[GetHandleFromThread-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-gethandlefromthread-method.md)|Ordnet die ID eines Threads an ein Win32-Thread-Handle.|  
|[GetILFunctionBody-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbody-method.md)|Ruft einen Zeiger auf den Text einer Methode in Microsoft intermediate Language (MSIL)-Code, beginnend mit dem Header.|  
|[GetILFunctionBodyAllocator-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbodyallocator-method.md)|Ruft eine Schnittstelle, die eine Methode zum Reservieren von Speicher bietet für die Auslagerung des Texts einer Methode im MSIL-Code verwendet werden soll.|  
|[GetILToNativeMapping-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getiltonativemapping-method.md)|Ruft eine Zuordnung zwischen MSIL-Offsets und systemeigenen Offsets für den in der angegebenen Funktion enthaltenen Code ab.|  
|[GetInprocInspectionInterface-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getinprocinspectioninterface-method.md)|Ruft ein Objekt, das abgefragt werden kann für eine ICorDebugProcess-Schnittstelle. Diese Methode ist veraltet in .NET Framework, Version 2.0.|  
|[GetInprocInspectionIThisThread-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getinprocinspectionithisthread-method.md)|Ruft ein Objekt, das abgefragt werden kann, für die ICorDebugThread-Schnittstelle. Diese Methode ist veraltet in .NET Framework, Version 2.0.|  
|[GetModuleInfo-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmoduleinfo-method.md)|Gibt für die übergebene Modul-ID den Dateinamen des Moduls und die ID der übergeordneten Assembly des Moduls zurück.|  
|[GetModuleMetaData-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmodulemetadata-method.md)|Ruft eine Instanz der Metadaten-Schnittstelle, die das angegebene Modul zugeordnet.|  
|[GetObjectSize-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getobjectsize-method.md)|Ruft die Größe eines angegebenen Objekts ab.|  
|[GetThreadContext-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadcontext-method.md)|Ruft die Kontextidentität, die derzeit zugewiesen ist, mit dem angegebenen Thread ab.|  
|[GetThreadInfo-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadinfo-method.md)|Ruft die aktuelle Win32-Thread-Identität für den angegebenen Thread ab.|  
|[GetTokenAndMetadataFromFunction-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-gettokenandmetadatafromfunction-method.md)|Ruft das Metadatentoken und eine Instanz der Metadatenschnittstelle, die für die angegebene Funktion anhand des Tokens verwendet werden kann.|  
|[IsArrayClass-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-isarrayclass-method.md)|Bestimmt, ob die angegebene Klasse eine Array-Klasse.|  
|[SetEnterLeaveFunctionHooks-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setenterleavefunctionhooks-method.md)|Gibt Profiler implementierten Funktionen an, die für "eingeben", "Übernehmen" und "Tailcall" Hooks von verwalteten Funktionen aufgerufen werden.|  
|[SetEventMask-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)|Legt einen Wert, der die Ereignistypen angibt, für die der Profiler Benachrichtigungen von der CLR empfangen möchte.|  
|[SetFunctionIDMapper-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)|Gibt die vom Profiler implementierte Funktion an, die aufgerufen wird, um die `FunctionID`-Werte alternativen Werten zuzuordnen, die an die Funktionseinstiegs-/-exithooks des Profilers übergeben werden.|  
|[SetFunctionReJIT-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionrejit-method.md)|Nicht implementiert. Nicht verwenden.|  
|[SetILFunctionBody-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md)|Ersetzt den Text der angegebenen Funktion im angegebenen Modul.|  
|[SetILInstrumentedCodeMap-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md)|Gibt an, wie die neuen die Funktion Profiler geänderten MSIL-Offsets die Offsets der ursprünglichen MSIL einer angegebenen Funktion zugeordnet.|  
  
## <a name="remarks"></a>Hinweise  
 Ein Profiler Ruft eine Methode in der `ICorProfilerInfo` Schnittstelle für die Kommunikation mit der CLR, die ereignisüberwachung zu steuern und Informationen anzufordern.  
  
 Die Methoden der `ICorProfilerInfo` Schnittstelle werden von der CLR mithilfe des Freethread-Modells implementiert. Jede Methode gibt ein HRESULT zurück, um einen Erfolg oder einen Fehler anzugeben. Eine Liste möglicher Rückgabecodes finden Sie unter "CorError.h".  
  
 Die CLR übergibt über die Profiler-Implementierung von [ICorProfilerCallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md), einem `ICorProfilerInfo` -Schnittstelle an jeden Codeprofiler während der Initialisierung. Ein Codeprofiler kann dann Methoden von Aufrufen der `ICorProfilerInfo` Schnittstelle zum Abrufen von Informationen über verwalteten Code unter der Kontrolle der CLR ausgeführt wird.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorProf.idl, CorProf.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Profilerstellungsschnittstellen](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [ICorProfilerInfo2-Schnittstelle](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
