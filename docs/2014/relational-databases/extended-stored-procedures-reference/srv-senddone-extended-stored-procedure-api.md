---
title: srv_senddone (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- srv_senddone
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_senddone
ms.assetid: 1fc4f1d5-56d4-43f6-b5e4-0c0cc295cba3
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6a7ed324a068b81c2226a0b520d403f688a6ede7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033640"
---
# <a name="srvsenddone-extended-stored-procedure-api"></a>srv_senddone (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 將結果完成訊息傳送至用戶端。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_senddone (  
SRV_PROC *  
srvproc  
,  
DBUSMALLINT   
status  
,  
DBUSMALLINT  
info  
,  
DBINT  
count   
);  
  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (此案例中為接收語言要求的控制代碼)。 此結構包含了一些資訊，擴充預存程序 API 程式庫會使用這些資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *status*  
 這是各種 *status* 旗標的 2 位元組欄位。 可以搭配 *status* 旗標值使用 AND 和 OR 邏輯運算子來設定多個旗標。 下表列出可能的 *status* 旗標。  
  
|狀態旗標|描述|  
|-----------------|-----------------|  
|SRV_DONE_COUNT|*count* 參數包含有效的計數。|  
|SRV_DONE_ERROR|目前的用戶端命令收到錯誤。|  
  
 *info*  
 這是保留的 2 位元組欄位。 將這個值設定為 0。  
  
 *計數*  
 這是用來指示目前結果集計數的 4 位元組欄位。 如果在 *status* 欄位中設定 SRV_DONE_COUNT 旗標，*count* 會保留有效的計數。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL  
  
## <a name="remarks"></a>備註  
 用戶端要求會造成伺服器執行一些命令，並傳回一些結果集。 **srv_senddone** 必須針對每一個結果集傳回結果完成訊息給用戶端。  
  
 *count* 欄位指出受到命令影響的資料列數。 如果 *count* 欄位包含計數，就應該在 *status* 欄位中設定 SRV_DONE_COUNT 旗標。 此設定可讓用戶端區分 0 的 *count* 值及未使用的 *count* 欄位。  
  
 請勿從 SRV_CONNECT 處理常式呼叫 **srv_senddone**。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
  