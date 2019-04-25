---
title: srv_rpcnumber (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcnumber
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcnumber
ms.assetid: 3094085e-fe9e-423d-bf87-7852352c2d26
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1036cbe649a2448b3eb4838621ec8be0590b1c3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62745559"
---
# <a name="srvrpcnumber-extended-stored-procedure-api"></a>srv_rpcnumber (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回目前遠端預存程序呼叫的數字元件。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_rpcnumber ( SRV_PROC *  
srvproc   
)  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (在這個狀況之下，該控制代碼會收到遠端預存程序)。 此結構包含了一些資訊，擴充預存程序 API 程式庫會使用這些資訊來管理應用程式與用戶端之間的通訊和資料。  
  
## <a name="returns"></a>傳回值  
 目前遠端預存程序的數字元件。 如果用戶端在執行遠端預存程序時未使用數字元件，或者並沒有目前的遠端預存程序，則會傳回 – 1。  
  
## <a name="remarks"></a>備註  
 此函數只會傳回遠端預存程序的數字元件。 不包含擁有人、遠端預存程序名稱和資料庫名稱的選擇性規範。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
