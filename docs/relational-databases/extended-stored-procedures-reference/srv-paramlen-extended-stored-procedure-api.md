---
title: "srv_paramlen (擴充預存程序 API) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_paramlen
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_paramlen
ms.assetid: d1fe92ff-cad6-4396-8216-125e5642e81e
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3604a89d5b85d861963741d86342a34f1e09f7c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="srvparamlen-extended-stored-procedure-api"></a>srv_paramlen (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回遠端預存程序呼叫參數的資料長度。 此函式已被 **srv_paraminfo** 函式取代。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_paramlen (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (在這個狀況之下，該控制代碼會收到遠端預存程序呼叫)。 此結構包含了一些資訊，擴充預存程序 API 程式庫會使用這些資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *n*  
 這指出參數的數目。 第一個參數是 1。  
  
## <a name="returns"></a>傳回值  
 這是參數資料的實際長度 (以位元組為單位)。 如果沒有第 *n* 個參數，或者沒有遠端預存程序，則傳回 -1。 如果第 *n* 個參數為 NULL，它會傳回 0。  
  
 如果參數是下列其中一個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 系統資料類型，此函式會傳回下列值。  
  
|新的資料類型|輸入資料長度|  
|--------------------|-----------------------|  
|**BITN**|**NULL：**1<br /><br /> **ZERO：**1<br /><br /> **>=255：**N/A<br /><br /> **<255：**N/A|  
|**BIGVARCHAR**|**NULL：**0<br /><br /> **ZERO：**1<br /><br /> **>=255:** 255<br /><br /> **<255：**實際 *len*|  
|**BIGCHAR**|**NULL：**0<br /><br /> **ZERO：**255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|**BIGBINARY**|**NULL：**0<br /><br /> **ZERO：**255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|**BIGVARBINARY**|**NULL：**0<br /><br /> **ZERO：**1<br /><br /> **>=255:** 255<br /><br /> **<255：**實際 *len*|  
|**NCHAR**|**NULL：**0<br /><br /> **ZERO：**255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|**NVARCHAR**|**NULL：**0<br /><br /> **ZERO：**1<br /><br /> **>=255:** 255<br /><br /> **<255：**實際 *len*|  
|**NTEXT**|**NULL：**-1<br /><br /> **ZERO：**-1<br /><br /> **>=255:** -1<br /><br /> **\<255:** -1|  
  
 \*   實際 *len* = 多位元組字元字串 (cch) 的長度  
  
## <a name="remarks"></a>備註  
 每個遠端預存程序參數都具有實際和最大的資料長度。 對於不允許 null 值的標準固定長度資料類型，實際和最大的長度是相同的。 對於可變長度資料類型，長度則可以有所不同。 例如，宣告為 **varchar(30)** 的參數可能擁有只有 10 個位元組長的資料。 參數的實際長度為 10，而其最大長度為 30。 **srv_paramlen** 函式會取得遠端預存程序的實際資料長度 (以位元組為單位)。 若要取得參數的最大資料長度，請使用 **srv_parammaxlen**。  
  
 當遠端預存程序呼叫是用參數產生時，該參數可以依名稱或位置 (未命名) 傳遞。 如果遠端預存程序呼叫是藉由一些依名稱傳遞的參數和一些依位置傳遞的參數來進行時，就會發生錯誤。 雖然仍會呼叫 SRV_RPC 處理常式，但是看起來好像沒有參數，而且 **srv_rpcparams** 會傳回 0。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_paraminfo &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
