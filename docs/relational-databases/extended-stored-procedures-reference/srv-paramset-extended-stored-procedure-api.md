---
title: srv_paramset (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_paramset
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramset
ms.assetid: 2a509206-a1b8-4b20-b0a2-ef680cef7bd8
caps.latest.revision: 31
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c76f1dc82a04ae14150833df75fd23db83b7fecc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="srvparamset-extended-stored-procedure-api"></a>srv_paramset (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 設定遠端預存程序呼叫傳回參數的值。 此函式已被 **srv_paramsetoutput** 函式取代。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_paramset (  
SRV_PROC *  
srvproc  
,  
int  
n  
,   
void *  
data  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (在這個狀況之下，該控制代碼會收到遠端預存程序呼叫)。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *n*  
 表示要設定的參數數目。 第一個參數是 1。  
  
 *data*  
 這是指向要當做遠端預存程序傳回參數傳回給用戶端之資料值的指標。  
  
 *len*  
 指定要傳回之資料的實際長度。 如果參數的資料類型具有固定長度，而且不允許 null 值 (例如 *srvbit* 或 *srvint1*)，則會忽略 *len*。  
  
## <a name="returns"></a>傳回值  
 如果參數值設定成功則會傳回 SUCCEED，否則會傳回 FAIL。 會傳回 FAIL，當目前沒有遠端預存程序，沒有任何*n*個遠端預存程序參數、 參數不是傳回參數而且*len*引數不是合法的。  
  
 如果 *len* 是 0，它會傳回 NULL。 將 *len* 設定為 0 是將 NULL 傳回給用戶端的唯一方法。  
  
 如果參數是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料類型的一種，則此函式會傳回下列值。  
  
|新的資料類型|傳回資料長度|  
|--------------------|------------------------|  
|**BITN**|**NULL：***len* = 0、data = IG、RET = 0<br /><br /> **ZERO：**N/A<br /><br /> **>=255：**N/A<br /><br /> **<255：**N/A|  
|**BIGVARCHAR**|**NULL：***len* = 0、data = IG、RET = 1<br /><br /> **ZERO：***len* = IG、data = IG、RET = 0<br /><br /> **>=255：***len* = max8k、data = valid、RET = 0<br /><br /> **<255：***len* = <8k、data = valid、RET = 1|  
|**BIGCHAR**|**NULL：***len* = 0、data = IG、RET = 1<br /><br /> **ZERO：***len* = IG、data = IG、RET = 0<br /><br /> **>=255：***len* = max8k、data = valid、RET = 0<br /><br /> **<255：***len* = <8k、data = valid、RET = 1|  
|**BIGBINARY**|**NULL：***len* = 0、data = IG、RET = 1<br /><br /> **ZERO：***len* = IG、data = IG、RET = 0<br /><br /> **>=255：***len* = max8k、data = valid、RET = 0<br /><br /> **<255：***len* = <8k、data = valid、RET = 1|  
|**BIGVARBINARY**|**NULL：***len* = 0、data = IG、RET = 1<br /><br /> **ZERO：***len* = IG、data = IG、RET = 0<br /><br /> **>=255：***len* = max8k、data = valid、RET = 0<br /><br /> **<255：***len* = <8k、data = valid、RET = 1|  
|NCHAR|**NULL：***len* = 0、data = IG、RET = 1<br /><br /> **ZERO：***len* = IG、data = IG、RET = 0<br /><br /> **>=255：***len* = max8k、data = valid、RET = 0<br /><br /> **<255：***len* = <8k、data = valid、RET = 1|  
|NVARCHAR|**NULL：***len* = 0、data = IG、RET = 1<br /><br /> **ZERO：***len* = IG、data = IG、RET = 0<br /><br /> **>=255：***len* = max8k、data = valid、RET = 0<br /><br /> **<255：***len* = <8k、data = valid、RET = 1|  
|**NTEXT**|**NULL：***len* = IG、data = IG、RET = 0<br /><br /> **ZERO：***len* = IG、data = IG、RET = 0<br /><br /> **>=255：***len* = IG、data = IG、RET = 0<br /><br /> **\<255：***len* = IG、data = IG、RET = 0|  
|RET = srv_paramset 的傳回值||  
|IG = 值將會被略過||  
|valid = 資料的任何有效指標||  
  
## <a name="remarks"></a>備註  
 參數包含了在用戶端和應用程式之間傳遞的資料，其中包含遠端預存程序。 用戶端可以將某些參數指定為傳回參數。 這些傳回參數可包含「開放式資料服務」伺服器應用程式傳回給用戶端的值。 使用傳回參數類似於依參考方式傳遞參數。  
  
 您不能針對未當做傳回參數叫用的參數來設定傳回值。 您可以使用 **srv_paramstatus** 來決定要如何叫用此參數。  
  
 這個函數會設定參數的傳回值，但是實際上並不會將傳回值傳給用戶端。 當呼叫 **srv_senddone** 並有設定狀態旗標 SRV_DONE_FINAL 時，所有傳回參數 (不論是否已經使用 **srv_paramset** 來設定其傳回值) 都會自動傳給用戶端。  
  
 當遠端預存程序呼叫是用參數產生時，該參數可以依名稱或位置 (未命名) 傳遞。 如果遠端預存程序呼叫是藉由一些依名稱傳遞的參數和一些依位置傳遞的參數來進行時，就會發生錯誤。 雖然仍會呼叫 SRV_RPC 處理常式，但是看起來好像沒有參數，而且 **srv_rpcparams** 會傳回 0。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_paramsetoutput &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-paramsetoutput-extended-stored-procedure-api.md)  
  
  
