---
title: srv_getbindtoken (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_getbindtoken
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_getbindtoken
ms.assetid: c947d011-08ac-4fb8-b925-3da6e0999277
caps.latest.revision: 36
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3934bc259fc1d69b2a4bf00e52fdb57b176978fb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32936223"
---
# <a name="srvgetbindtoken-extended-stored-procedure-api"></a>srv_getbindtoken (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 在目前的用戶端工作階段中取得叫用擴充預存程序之交易的繫結 Token。  
  
 接著，擴充預存程序可以使用 **sp_bindsession**，將針對相同伺服器建立的任何新工作階段繫結至現有的交易，讓新的工作階段可以與叫用擴充預存程序的用戶端工作階段共用相同的交易鎖定空間。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_getbindtoken (  
SRV_PROC*  
srvproc  
,  
char*  
bindtoken  
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼。 此結構包含了擴充預存程序 API 程式庫用來管理應用程式與用戶端之間之通訊和資料的所有資訊。  
  
 *bindtoken*  
 這是將複製繫結 Token 所在緩衝區的指標。 繫結 Token 會表示為以 null 結尾的字串。 您指定的緩衝區長度至少應該為 255 個位元組。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>Remarks  
  
### <a name="to-bind-an-extended-stored-procedure-session-to-the-client-session-that-called-it-so-they-share-the-same-transaction-lock-space"></a>將擴充預存程序工作階段繫結到呼叫它的用戶端工作階段，讓它們可以共用相同的交易鎖定空間  
  
1.  擴充預存程序會呼叫 **svr_getbindtoken** 來取得工作階段中目前交易的繫結 Token。 此 Token 會以指定的 *bindtoken* 參數傳回。  
  
2.  擴充預存程序會針對相同的伺服器開啟新的工作階段。 在該工作階段內部，擴充預存程序會搭配 **sp_bindsession** 使用繫結 Token，將新的工作階段繫結到相同的交易。 擴充預存程序可以建立多個工作階段，並將所有工作階段繫結到相同的交易。  
  
3.  當外部預存程序傳回時，或使用空字串呼叫 **sp_bindsession** 時，會取消繫結已繫結的工作階段。  
  
    > [!NOTE]  
    >  一次只有一個繫結的工作階段可以存取共用連接。 如果某個工作階段目前正在伺服器上執行陳述式或等待伺服器的暫止結果，共用相同繫結連接的其他工作階段都無法存取伺服器，直到目前的工作階段完成執行目前的陳述式為止。 如果有工作階段嘗試在伺服器忙線時存取連接，就會將錯誤傳回到發生衝突的工作階段，表示連接正在使用中，而且工作階段應該在稍後重試。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [sp_bindsession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)  
  
  
