---
title: srv_setcollen (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setcollen
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setcollen
ms.assetid: 3c60f1c3-4562-463a-a259-12df172788bd
author: rothja
ms.author: jroth
ms.openlocfilehash: 15bd83b902ad64213fcde3ef15a185d69fde8cd4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68119644"
---
# <a name="srv_setcollen-extended-stored-procedure-api"></a>srv_setcollen (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 以位元組為單位，指定可變長度資料行或允許 NULL 值之資料行目前的資料長度。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_setcollen (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *排*  
 這表示要指定其資料長度的資料行編號。 資料行的編號會從 1 開始。  
  
 *len*  
 這表示資料行資料的長度 (以位元組為單位)。 0 的長度代表資料行資料值為 Null。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 資料列的每個資料行必須先用 **srv_describe** 定義。 資料行的資料長度是由對 **srv_describe** 或 **srv_setcollen** 的最後呼叫所設定。 如果資料列的可變長度資料 (以 Null 結束的資料) 變更，則必須先使用 **srv_setcollen** 來將它設定為新長度，再呼叫 **srv_sendrow**。 如果是允許 Null 值的資料行，則必須以 *desttype* 設定為允許 Null 的資料類型 (例如 SRVINTN) 來呼叫 **srv_describe**，而且以設定為 0 的 *len* 呼叫 **srv_setcollen** 來指定 Null 資料。 零長度的資料不能使用擴充預存程序 API 指定。  
  
 請注意，當資料行的資料類型是可變長度時，就不會檢查 *len*。 如果針對固定長度資料行呼叫此函數，此函數會傳回 FAIL。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_describe &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
