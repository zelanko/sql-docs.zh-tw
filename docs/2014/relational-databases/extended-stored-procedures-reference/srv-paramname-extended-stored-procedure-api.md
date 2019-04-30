---
title: srv_paramname (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramname
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramname
ms.assetid: 1a53d707-7b06-49cc-a0df-ac727cfe953f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8a5eca5aef966d205ef550b05eff2d7055e4cb28
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127170"
---
# <a name="srvparamname-extended-stored-procedure-api"></a>srv_paramname (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回遠端預存程序呼叫參數的名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBCHAR * srv_paramname (  
SRV_PROC * srvproc,intn, int *len );  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (在這個狀況之下，該控制代碼會收到遠端預存程序呼叫)。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *n*  
 這指出參數的數目。 第一個參數是 1。  
  
 *len*  
 提供包含參數名稱長度 (以位元組為單位) 之 `int` 變數的指標。 如果 *len* 為 NULL，則不會傳回遠端預存程序參數名稱的長度。  
  
## <a name="returns"></a>傳回值  
 包含參數名稱且以 Null 結束之字元字串的指標。 參數名稱的長度會儲存在 *len* 中。 如果沒有第 *n* 個參數或沒有任何遠端預存程序，其會傳回 NULL、將 *len* 設定為 -1，並會傳送參考用錯誤訊息。 如果參數名稱為 NULL，*len* 就會設定為 0，而且傳回以 Null 結束的空字串。  
  
## <a name="remarks"></a>備註  
 這個函數會取得遠端預存程序呼叫參數的名稱。 當遠端預存程序呼叫是用參數產生時，該參數可以依名稱或位置 (未命名) 傳遞。 如果遠端預存程序呼叫是藉由一些依名稱傳遞的參數和一些依位置傳遞的參數來進行時，就會發生錯誤。 雖然仍會呼叫 SRV_RPC 處理常式，但是看起來好像沒有參數，而且 **srv_rpcparams** 會傳回 0。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_rpcparams &#40;擴充預存程序 API&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
