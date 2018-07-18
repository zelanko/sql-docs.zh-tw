---
title: srv_setcollen (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- srv_setcollen
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_setcollen
ms.assetid: 3c60f1c3-4562-463a-a259-12df172788bd
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 668e6e0af87ac1a2c240c5b6a636b0529d23615c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272694"
---
# <a name="srvsetcollen-extended-stored-procedure-api"></a>srv_setcollen (擴充預存程序 API)
    
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
  
 *column*  
 這表示要指定其資料長度的資料行編號。 資料行的編號會從 1 開始。  
  
 *len*  
 這表示資料行資料的長度 (以位元組為單位)。 0 的長度代表資料行資料值為 Null。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 資料列的每個資料行必須先用 **srv_describe** 定義。 資料行的資料長度是由對 **srv_describe** 或 **srv_setcollen** 的最後呼叫所設定。 如果資料列的可變長度資料 (以 Null 結束的資料) 變更，則必須先使用 **srv_setcollen** 來將它設定為新長度，再呼叫 **srv_sendrow**。 如果是允許 Null 值的資料行，則必須以 *desttype* 設定為允許 Null 的資料類型 (例如 SRVINTN) 來呼叫 **srv_describe**，而且以設定為 0 的 *len* 呼叫 **srv_setcollen** 來指定 Null 資料。 零長度的資料不能使用擴充預存程序 API 指定。  
  
 請注意，當資料行的資料類型是可變長度時，就不會檢查 *len*。 如果針對固定長度資料行呼叫此函數，此函數會傳回 FAIL。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_describe &#40;擴充預存程序 API&#41;](srv-describe-extended-stored-procedure-api.md)  
  
  
