---
title: ICorDebugClass::GetStaticFieldValue-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugClass.GetStaticFieldValue
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugClass::GetStaticFieldValue
helpviewer_keywords:
- GetStaticFieldValue method, ICorDebugClass interface [.NET Framework debugging]
- ICorDebugClass::GetStaticFieldValue method [.NET Framework debugging]
ms.assetid: 56e718b4-fabd-418b-a5b3-3cc33c745683
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 15491728e225799eb0e934c9cc42a3967c19202e
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugclassgetstaticfieldvalue-method"></a><span data-ttu-id="74b39-102">ICorDebugClass::GetStaticFieldValue-Methode</span><span class="sxs-lookup"><span data-stu-id="74b39-102">ICorDebugClass::GetStaticFieldValue Method</span></span>
<span data-ttu-id="74b39-103">Ruft den Wert des angegebenen statischen Felds ab.</span><span class="sxs-lookup"><span data-stu-id="74b39-103">Gets the value of the specified static field.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="74b39-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="74b39-104">Syntax</span></span>  
  
```  
HRESULT GetStaticFieldValue (  
    [in]  mdFieldDef         fieldDef,  
    [in]  ICorDebugFrame     *pFrame,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="74b39-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="74b39-105">Parameters</span></span>  
 `fieldDef`  
 <span data-ttu-id="74b39-106">[in] Ein Feld `Def` Token, verweist das Feld abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="74b39-106">[in] A field `Def` token that references the field to be retrieved.</span></span>  
  
 `pFrame`  
 <span data-ttu-id="74b39-107">[in] Ein Zeiger auf eine ICorDebugFrame-Objekt, das verwendet werden, um den Thread, Kontext, Anwendung Domäne Mehrdeutigkeit zwischen oder den Frame darstellt.</span><span class="sxs-lookup"><span data-stu-id="74b39-107">[in] A pointer to an ICorDebugFrame object that represents the frame to be used to disambiguate among thread, context, or application domain statics.</span></span>  
  
 <span data-ttu-id="74b39-108">Wenn das statische Feld relativ zu einem Thread, einem Kontext oder eine Anwendungsdomäne, wird der Frame den richtigen Wert bestimmt.</span><span class="sxs-lookup"><span data-stu-id="74b39-108">If the static field is relative to a thread, a context, or an application domain, the frame will determine the proper value.</span></span>  
  
 `ppValue`  
 <span data-ttu-id="74b39-109">[out] Ein Zeiger auf die Adresse eines ICorDebugValue-Objekts, das den Wert des statischen Felds darstellt.</span><span class="sxs-lookup"><span data-stu-id="74b39-109">[out] A pointer to the address of an ICorDebugValue object that represents the value of the static field.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="74b39-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="74b39-110">Remarks</span></span>  
 <span data-ttu-id="74b39-111">Ist der Wert eines statischen Felds für parametrisierte Typen relativ zu bestimmten Instanziierung.</span><span class="sxs-lookup"><span data-stu-id="74b39-111">For parameterized types, the value of a static field is relative to the particular instantiation.</span></span> <span data-ttu-id="74b39-112">Aus diesem Grund Wenn Parameter vom Typ der Klassenkonstruktor <xref:System.Type>, rufen Sie [ICorDebugType:: GetStaticFieldValue](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getstaticfieldvalue-method.md) anstelle von `ICorDebugClass::GetStaticFieldValue`.</span><span class="sxs-lookup"><span data-stu-id="74b39-112">Therefore, if the class constructor takes parameters of type <xref:System.Type>, call [ICorDebugType::GetStaticFieldValue](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getstaticfieldvalue-method.md) instead of `ICorDebugClass::GetStaticFieldValue`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="74b39-113">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="74b39-113">Requirements</span></span>  
 <span data-ttu-id="74b39-114">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="74b39-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="74b39-115">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="74b39-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="74b39-116">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="74b39-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="74b39-117">**.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="74b39-117">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>