---
title: ICorDebugStepper::SetRangeIL-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.SetRangeIL
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::SetRangeIL
helpviewer_keywords:
- SetRangeIL method [.NET Framework debugging]
- ICorDebugStepper::SetRangeIL method [.NET Framework debugging]
ms.assetid: a20c95f0-6da7-4b41-b27f-584211cebb92
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cb3c24b3a96a03359dc6983bcaac4a800613ff5d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugsteppersetrangeil-method"></a>ICorDebugStepper::SetRangeIL-Methode
Legt einen Wert, der angibt, ob Aufrufe von [ICorDebugStepper:: StepRange](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-steprange-method.md) Argument Werte, die relativ zu den systemeigenen Code oder relativ zum Microsoft intermediate Language (MSIL)-Code der Methode, die schrittweise wird übergeben durch.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT SetRangeIL (  
    [in] BOOL    bIL  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `bIL`  
 [in] Legen Sie auf `true` um anzugeben, dass die Bereiche relativ zu der MSIL-Code haben. Legen Sie auf `false` um anzugeben, dass der Bereich relativ zu den systemeigenen Code liegt. Der Standardwert ist `true`.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
