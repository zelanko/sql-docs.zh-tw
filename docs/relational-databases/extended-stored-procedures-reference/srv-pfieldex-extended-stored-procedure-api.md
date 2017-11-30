---
title: "srv_pfieldex (擴充預存程序 API) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_pfieldex
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 11e0eeb19711c6070eeca4fdae23607d420289b3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="srvpfieldex-extended-stored-procedure-api"></a>srv_pfieldex (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回含有要求之 SRV_PROC 欄位的資料的指標。  
  
## <a name="syntax"></a>語法  
  
```  
  
void *srv_pfieldex(SRV_PROC *   
srvproc  
, int   
field  
, int *   
len  
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *field*  
 指定要傳回的 *srvproc* 欄位。  
  
|欄位|Description|傳回類型|  
|-----------|-----------------|------------------|  
|SRV_MSGLCID|目前的工作階段訊息 LCID。|ULONG*|  
|SRV_INSTANCENAME|執行個體名稱 (如果是具名的)；否則，傳回 NULL。|WCHAR*|  
  
 *len*  
 這是指向 **int** 變數的指標，該變數含有傳回 *field* 值的長度 (以位元組為單位)。 如果 *len* 為 NULL，則不會傳回長度。 當傳回 NULL 時，**len* 會設定為 0。  
  
## <a name="returns"></a>傳回值  
 指向資料的指標，其資料類型取決於 *field*。 當 *len* 為 NULL 或 *srvproc* 為 NULL 時，會傳回 NULL。 如果 *field* 為未知，則傳回 NULL。 當傳回 NULL 時，**len* 會設定為 0。  
  
> [!IMPORTANT]  
>  從伺服器傳回的緩衝區應該是唯讀的。 否則，伺服器狀態可能會損毀。  
  
## <a name="remarks"></a>備註  
 **安全性注意事項**：您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
  
