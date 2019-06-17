---
title: srv_sendrow (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_sendrow
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_sendrow
ms.assetid: a08f608a-10e6-4bff-9b48-0d02e8026cdb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f39355222b491be27cc1b914401dcc459151e4bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62718055"
---
# <a name="srvsendrow-extended-stored-procedure-api"></a>srv_sendrow (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 將資料的資料列傳送到用戶端。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_sendrow ( SRV_PROC *  
srvproc   
);  
  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (此案例中為接收語言要求的控制代碼)。 此結構包含了一些資訊，擴充預存程序 API 程式庫會使用這些資訊來管理應用程式與用戶端之間的通訊和資料。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 系統會針對傳送到用戶端的每個資料列，呼叫 **srv_sendrow** 函式一次。 所有資料列都必須在使用 **srv_sendmsg**、**srv_status** 或 **srv_senddone** 傳送任何訊息、狀態值或完成狀態之前，傳送到用戶端。  
  
 傳送已經使用 **srv_describe** 定義其所有資料行的資料列時，會使擴充預存程序 API 應用程式引發參考用錯誤訊息，並將 FAIL 傳回到用戶端。 在此情況下，不會傳送資料列。  
  
> [!NOTE]  
>  擴充預存程序 API 不支援將計算資料列傳送到用戶端。 同時，如果將包含 `ntext`、`text` 或 `image` 資料的資料列傳送到用戶端，則不會包括文字指標與文字時間戳記。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_describe &#40;擴充預存程序 API&#41;](srv-describe-extended-stored-procedure-api.md)  
  
  
