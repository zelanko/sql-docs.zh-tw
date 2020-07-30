---
title: srv_paramtype (擴充預存程序 API) | Microsoft Docs
description: 瞭解擴充預存程式 API 中的 srv_paramtype 如何傳回遠端預存程序呼叫參數的資料類型。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramtype
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramtype
ms.assetid: badc6d36-8a87-42b5-b28c-9c4f5ded8552
author: rothja
ms.author: jroth
ms.openlocfilehash: 7dc2200fc0cfb526e78d3544dc5bba7ad0f3e52e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248312"
---
# <a name="srv_paramtype-extended-stored-procedure-api"></a>srv_paramtype (擴充預存程序 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回遠端預存程序呼叫參數的資料類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_paramtype (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (在這個狀況之下，該控制代碼會收到遠端預存程序呼叫)。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *n*  
 這指出參數的數目。 第一個參數是 1。  
  
## <a name="returns"></a>傳回  
 參數資料類型的 Token 值。 如需資料類型的資訊，請參閱[資料類型 &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)。 如果沒有第 *n* 個參數或是沒有任何遠端預存程序，會傳回 -1。  
  
 如果參數是其中一個資料類型，此函數會傳回下列值 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。  
  
|新的資料類型|傳回值|  
|--------------------|------------------|  
|**BITN**|SRVBIT|  
|**BIGVARCHAR**|VARCHAR|  
|**BIGCHAR**|CHAR|  
|**BIGBINARY**|BINARY|  
|**BIGVARBINARY**|VARBINARY|  
|**NCHAR**|CHAR|  
|**NVARCHAR**|VARCHAR|  
|**NTEXT**|-1|  
  
## <a name="remarks"></a>備註  
 當遠端預存程序呼叫是用參數產生時，該參數可以依名稱或位置 (未命名) 傳遞。 如果遠端預存程序呼叫是藉由一些依名稱傳遞的參數和一些依位置傳遞的參數來進行時，就會發生錯誤。 SRV_RPC 的處理常式仍會被呼叫，但看起來就好像沒有任何參數， **srv_rpcparams**會傳回0。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://www.microsoft.com/msrc?rtc=1)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_paraminfo &#40;擴充預存程式 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
