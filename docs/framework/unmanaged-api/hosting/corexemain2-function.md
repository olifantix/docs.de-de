---
title: _CorExeMain2-Funktion
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: _CorExeMain2
api_location: mscoree.dll
api_type: DLLExport
f1_keywords: _CorExeMain2
helpviewer_keywords: _CorExeMain2 function [.NET Framework hosting]
ms.assetid: 72ea68b4-689f-4733-9416-9664b75e8892
topic_type: apiref
caps.latest.revision: "16"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 7c705627de8e8157212ae3e6a2ab4f2c12246653
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="corexemain2-function"></a><span data-ttu-id="6fb18-102">_CorExeMain2-Funktion</span><span class="sxs-lookup"><span data-stu-id="6fb18-102">_CorExeMain2 Function</span></span>
<span data-ttu-id="6fb18-103">Führt den Einstiegspunkt im angegebenen Speicherabbildcode aus.</span><span class="sxs-lookup"><span data-stu-id="6fb18-103">Executes the entry point in the specified memory-mapped code.</span></span> <span data-ttu-id="6fb18-104">Diese Funktion wird vom Betriebssystemladeprogramm aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="6fb18-104">This function is called by the operating system loader.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6fb18-105">Syntax</span><span class="sxs-lookup"><span data-stu-id="6fb18-105">Syntax</span></span>  
  
```  
__int32 STDMETHODCALLTYPE _CorExeMain2 (  
   [in] PBYTE           pUnmappedPE,  
   [in] DWORD           cUnmappedPE,  
   [in] __in LPWSTR     pImageNameIn,  
   [in] __in LPWSTR     pLoadersFileName,  
   [in] __in LPWSTR     pCmdLine  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="6fb18-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="6fb18-106">Parameters</span></span>  
 `pUnmappedPE`  
 <span data-ttu-id="6fb18-107">[in] Ein Zeiger auf den Speicherabbildcode.</span><span class="sxs-lookup"><span data-stu-id="6fb18-107">[in] A pointer to the memory-mapped code.</span></span>  
  
 `cUnmappedPE`  
 <span data-ttu-id="6fb18-108">[in] Die Anzahl der Elemente `pUnmappedPE` aufnehmen kann.</span><span class="sxs-lookup"><span data-stu-id="6fb18-108">[in] The number of elements `pUnmappedPE` can hold.</span></span>  
  
 `pImageNameIn`  
 <span data-ttu-id="6fb18-109">[in] Ein Zeiger auf den Namen des ausführbaren Images.</span><span class="sxs-lookup"><span data-stu-id="6fb18-109">[in] A pointer to the name of the executable image.</span></span>  
  
 `pLoadersFileName`  
 <span data-ttu-id="6fb18-110">[in] Der Name der Ladeprogrammdatei.</span><span class="sxs-lookup"><span data-stu-id="6fb18-110">[in] The name of the loader file.</span></span>  
  
 `pCmdLine`  
 <span data-ttu-id="6fb18-111">[in] Befehlszeilenparameter, sofern vorhanden.</span><span class="sxs-lookup"><span data-stu-id="6fb18-111">[in] Command-line parameters, if any.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6fb18-112">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="6fb18-112">Requirements</span></span>  
 <span data-ttu-id="6fb18-113">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="6fb18-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6fb18-114">**Header:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="6fb18-114">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="6fb18-115">**Bibliothek:** als Ressource in MsCorEE.dll enthalten</span><span class="sxs-lookup"><span data-stu-id="6fb18-115">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="6fb18-116">**.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6fb18-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6fb18-117">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="6fb18-117">See Also</span></span>  
 [<span data-ttu-id="6fb18-118">Globale statische Metadatenfunktionen</span><span class="sxs-lookup"><span data-stu-id="6fb18-118">Metadata Global Static Functions</span></span>](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)