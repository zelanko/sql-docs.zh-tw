---
title: srv_got_attention (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_got_attention
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1b2b13668c9402d947937b4cc7aeb581c253d6a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127295"
---
# <a name="srvgotattention-extended-stored-procedure-api"></a>srv_got_attention (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 檢查是否需要中止目前的連接或工作，並在連接遭到清除或批次遭到中止時傳回 TRUE  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL srv_got_attention  
(SRV_PROC *  
srvproc  
);  
  
```  
  
#### <a name="parameters"></a>參數  
 *srvproc*  
 識別資料庫連接的指標。  
  
## <a name="return-value"></a>傳回值  
 如果連接遭到清除或批次遭到中止，則為 TRUE。 如果連接或批次作用中，則為 FALSE。  
  
## <a name="remarks"></a>備註  
 長時間執行的擴充預存程序應該透過定期呼叫 **srv_got_attention** 來檢查伺服器的注意事項，讓該程序可以在連線到終止或批次遭到中止時自行結束。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
  
