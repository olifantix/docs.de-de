---
title: CLRDataCreateInstance-Funktion
ms.date: 03/30/2017
api_name:
- CLRDataCreateInstance
api_location:
- mscordbi.dll
- mscordacwks.dll
api_type:
- COM
f1_keywords:
- CLRDataCreateInstance
helpviewer_keywords:
- CLRDataCreateInstance function [.NET Framework debugging]
ms.assetid: 440bad90-5a88-45e7-9157-4596801d8d19
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d9d4965751db1a70871270317a644b0acb1302f7
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="clrdatacreateinstance-function"></a>CLRDataCreateInstance-Funktion
Erstellt ein Schnittstellenobjekt für das angegebene Ziel-Element.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT CLRDataCreateInstance (  
    [in]  REFIID           iid,   
    [in]  ICLRDataTarget  *target,   
    [out] void           **iface  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `iid`  
 [in] Der Bezeichner der Schnittstelle instanziiert werden.  
  
 `target`  
 [in] Ein Zeiger auf eine vom Benutzer implementierte [ICLRDataTarget](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget-interface.md) Objekt, das des Zielelements für die zum Erstellen des Schnittstellenobjekts darstellt.  
  
 `iface`  
 [out] Ein Zeiger auf die Adresse des Objekts zurückgegebene Schnittstelle.  
  
## <a name="remarks"></a>Hinweise  
 Die `ICLRDataTarget` Objekt wird vom Writer der Debuganwendung implementiert. Die Implementierung hängt vom Typ des Zielelements dargestellt wird. Das Zielelement ist möglicherweise ein Prozess, Speicherabbild Remotecomputer und So weiter.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** ClrData.idl  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Debuggen von globalen statischen Funktionen](../../../../docs/framework/unmanaged-api/debugging/debugging-global-static-functions.md)
