---
title: srv_paramdata (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramdata
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramdata
ms.assetid: 3104514d-b404-47c9-b6d7-928106384874
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8740e97d1c12cc0fc9198048ea58c12e01e6771c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666797"
---
# <a name="srvparamdata-extended-stored-procedure-api"></a>srv_paramdata (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回遠端預存程序呼叫參數的值。 此函式已被 **srv_paraminfo** 函式取代。  
  
## <a name="syntax"></a>語法  
  
```  
  
void * srv_paramdata (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (在這個狀況之下，該控制代碼會收到遠端預存程序呼叫)。 擴充預存程序程式庫會使用該結構所包含的資訊，來管理應用程式與用戶端之間的通訊和資料。  
  
 *n*  
 這是參數的數目。 第一個參數是數字 1。  
  
## <a name="returns"></a>傳回值  
 參數值的指標。 如果第 *n* 個參數為 NULL、沒有第 *n* 個參數，或是沒有任何遠端預存程序，會傳回 NULL。 如果參數值為字串，則可能不會以 Null 結束。 請使用 **srv_paramlen** 來判斷字串的長度。  
  
 如果參數是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的一種，則此函式會傳回下列值。 指標資料包含資料類型的指標是否為有效 (VP)、NULL 或不適用 (N/A)，以及資料所指向的內容。  
  
|新的資料類型|輸入資料長度|  
|--------------------|-----------------------|  
|BITN|**NULL：** VP、NULL<br /><br /> **ZERO：** VP、NULL<br /><br /> **>=255：** N/A<br /><br /> **<255：** N/A|  
|BIGVARCHAR|**NULL：** NULL、N/A<br /><br /> **ZERO：** VP、NULL<br /><br /> **>=255：** VP、255 個字元<br /><br /> **<255：** VP、實際資料|  
|BIGCHAR|**NULL：** NULL、N/A<br /><br /> **ZERO：** VP、255 個空格<br /><br /> **>=255：** VP、255 個字元<br /><br /> **<255：** VP、實際資料 + 填補 (最多 255)|  
|BIGBINARY|**NULL：** NULL、N/A<br /><br /> **ZERO：** VP、255 0x00<br /><br /> **>=255：** VP、255 個位元組<br /><br /> **<255：** VP、實際資料 + 填補 (最多 255)|  
|BIGVARBINARY|**NULL：** NULL、N/A<br /><br /> **ZERO：** VP、0x00<br /><br /> **>=255：** VP、255 個位元組<br /><br /> **<255：** VP、實際資料|  
|NCHAR|**NULL：** NULL、N/A<br /><br /> **ZERO：** VP、255 個空格<br /><br /> **>=255：** VP、255 個字元<br /><br /> **<255：** VP、實際資料 + 填補 (最多 255)|  
|NVARCHAR|**NULL：** NULL、N/A<br /><br /> **ZERO：** VP、NULL<br /><br /> **>=255：** VP、255 個字元<br /><br /> **<255：** VP、實際資料|  
|NTEXT|**NULL：** N/A<br /><br /> **ZERO：** N/A<br /><br /> **>=255：** N/A<br /><br /> **\<255：** N/A|  
  
 \*   資料不是以 Null 結束；在截斷 >255 個字元的資料時，不會發出警告。  
  
## <a name="remarks"></a>Remarks  
 如果您知道參數名稱，可以使用 **srv_paramnumber** 來取得參數數目。 若要判斷參數是否為 NULL，請使用 **srv_paramlen**。  
  
 當遠端預存程序呼叫是用參數進行時，可以依名稱或位置 (未命名) 傳遞參數。 如果遠端預存程序呼叫是藉由一些依名稱傳遞的參數和一些依位置傳遞的參數來進行時，就會發生錯誤。 如果發生錯誤，則仍會呼叫 SRV_RPC 處理常式，但會看來好像沒有參數一般，而且 **srv_rpcparams** 會傳回 0。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_rpcparams &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
