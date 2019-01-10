---
title: srv_wsendmsg (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_wsendmsg
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_wsendmsg
ms.assetid: f2153076-32c9-4a52-8e1b-fc9618153543
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 18b166472cff011b3766645dde61f562c766ff2c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366190"
---
# <a name="srvwsendmsg-extended-stored-procedure-api"></a>srv_wsendmsg (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 將 Unicode 訊息傳送給用戶端。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_wsendmsg(SRV_PROC *   
srvproc  
, int   
msgnum  
, int   
severity  
, WCHAR *   
message  
, int   
msglen  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *Msgnum*  
 這是 4 位元組的訊息編號。  
  
 *Severity*  
 指定錯誤的嚴重性。 嚴重性小於或等於 10 視為參考用訊息，否則就是錯誤。  
  
 *message*  
 這是要傳送給用戶端之 Unicode 字串的指標。  
  
 *msglen*  
 指定 *message* 的長度 (以字元為單位)。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 使用這個函數來以 Unicode 傳送訊息。 這類似於 **srv_sendmsg**，但是它所傳送的訊息是 WCHAR 字串，而不是 DBCHAR 類型的字串。 請注意，訊息長度是以字元報告，而不是以位元組報告，而且 *msglen* 絕對不會等於 SRV_NULLTERM。  
  
 此函數在下列情況下會傳回 FAIL  
  
-   指定的 *msglen* 不在 0-32242 範圍內。  
  
-   指定的 *msglen* 為 0，但是訊息指標為 NULL。  
  
-   當透過網路傳送錯誤訊息時發生錯誤。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_sendmsg &#40;擴充預存程序 API&#41;](srv-sendmsg-extended-stored-procedure-api.md)  
  
  
