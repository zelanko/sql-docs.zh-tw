---
title: srv_pfieldex (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_pfieldex
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8bacfd4f955f60b17b439c8066a3b1cba2c52392
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126947"
---
# <a name="srv_pfieldex-extended-stored-procedure-api"></a>srv_pfieldex (擴充預存程序 API)
    
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
  
|欄位|描述|傳回類型|  
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
 **安全性注意事項**：您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
