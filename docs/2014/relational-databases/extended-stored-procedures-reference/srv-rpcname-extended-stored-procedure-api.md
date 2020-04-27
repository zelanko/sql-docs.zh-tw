---
title: srv_rpcname (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcname
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcname
ms.assetid: 0a1424e4-3319-4836-b8d8-5e0344cc683f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f309349b2867412d552372e83ed1947b34242336
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046643"
---
# <a name="srv_rpcname-extended-stored-procedure-api"></a>srv_rpcname (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回目前遠端預存程序的程序名稱元件。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBCHAR * srv_rpcname (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (在這個狀況之下，該控制代碼會收到遠端預存程序)。 此結構包含了一些資訊，擴充預存程序 API 程式庫會使用這些資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *len*  
 這是整數變數的指標，此變數會接收資料庫名稱的長度。 如果 *len* 為 NULL，則不會傳回遠端預存程序名稱的長度。  
  
## <a name="returns"></a>傳回值  
 目前遠端預存程序之遠端預存程序名稱元件中以 Null 結尾字串的 DBCHAR 指標。 如果目前沒有遠端預存程序，則會傳回 NULL 且 *len* 設定為 - 1。  
  
## <a name="remarks"></a>備註  
 此函數只會傳回遠端預存程序的名稱。 這不包含擁有者、資料庫名稱和遠端預存程序號碼的選擇性規範。  
  
 由於沒有遠端預存程序時呼叫 **srv_rpcname** 是有效的做法 (不會出現任何參考用錯誤)，所以這個函式會提供一種方法來判斷遠端預存程序是否存在。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
