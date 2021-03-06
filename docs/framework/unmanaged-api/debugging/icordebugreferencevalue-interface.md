---
title: ICorDebugReferenceValue Schnittstelle1
ms.date: 03/30/2017
api_name:
- ICorDebugReferenceValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugReferenceValue
helpviewer_keywords:
- ICorDebugReferenceValue interface [.NET Framework debugging]
ms.assetid: 2040e2be-119a-4cfb-ae52-b0b6f052665c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b6cdfa9f3717e4025ff6f4fe6da3c1457cdebf7e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugreferencevalue-interface1"></a>ICorDebugReferenceValue Schnittstelle1
Enthält Methoden, die einen Wert zu verwalten, der einen Verweis auf ein Objekt ist. (D. h. diese Schnittstelle stellt Methoden bereit, die einen Zeiger zu verwalten.) Diese Schnittstelle implementiert "ICorDebugValue".  
  
## <a name="methods"></a>Methoden  
  
|Methode|Beschreibung|  
|------------|-----------------|  
|[Dereference-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugreferencevalue-dereference-method.md)|Ruft das Objekt ab, auf die verwiesen wird.|  
|[DereferenceStrong-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugreferencevalue-dereferencestrong-method.md)|Nicht implementiert. Rufen Sie diese Methode nicht.|  
|[GetValue-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugreferencevalue-getvalue-method.md)|Ruft die aktuelle Speicheradresse des referenzierten Objekts ab.|  
|[IsNull-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugreferencevalue-isnull-method.md)|Ruft einen Wert, der angibt, ob dies `ICorDebugReferenceValue` ein null-Wert in diesem Fall wird die `ICorDebugReferenceValue` verweist nicht auf ein Objekt.|  
|[SetValue-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugreferencevalue-setvalue-method.md)|Legt die aktuelle Speicheradresse. D. h. diese Methode legt für diesen `ICorDebugReferenceValue` auf ein Objekt verweisen.|  
  
## <a name="remarks"></a>Hinweise  
 Die common Language Runtime (CLR) möglicherweise eine Garbagecollection Objekte führen, wenn es sich bei ein debuggten Prozess fortgesetzt wird. Die Garbagecollection kann Objekte im Arbeitsspeicher verschieben. Ein `ICorDebugReferenceValue` werden entweder zusammen mit der Garbagecollection, damit die Informationen nach der Garbagecollection aktualisiert werden, oder er wird implizit vor der Garbagecollection ungültig gemacht.  
  
 Die `ICorDebugReferenceValue` Objekt möglicherweise implizit ungültig gemacht, nachdem der debuggten Prozess fortgesetzt wurde. Der abgeleitete "ICorDebugHandleValue" ist nicht für ungültig erklärt, bis er explizit freigegeben oder verfügbar gemacht wird.  
  
> [!NOTE]
>  Diese Schnittstelle kann weder computerübergreifend noch prozessübergreifend remote aufgerufen werden.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
    
    
 [Debuggen von Schnittstellen](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
