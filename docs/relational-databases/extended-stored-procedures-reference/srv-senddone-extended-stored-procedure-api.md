---
title: srv_senddone (擴充預存程序 API) | Microsoft Docs
description: 瞭解擴充預存程式 API 中的 srv_senddone 如何將結果完成訊息傳送至用戶端。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_senddone
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_senddone
ms.assetid: 1fc4f1d5-56d4-43f6-b5e4-0c0cc295cba3
author: rothja
ms.author: jroth
ms.openlocfilehash: 424ef5a1050def714e7f42483cb2c8d16ecfb99b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248243"
---
# <a name="srv_senddone-extended-stored-procedure-api"></a>srv_senddone (擴充預存程序 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
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
  
 *資訊*  
 這是保留的 2 位元組欄位。 將這個值設定為 0。  
  
 *計數*  
 這是用來指示目前結果集計數的 4 位元組欄位。 如果在 *status* 欄位中設定 SRV_DONE_COUNT 旗標，*count* 會保留有效的計數。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL  
  
## <a name="remarks"></a>備註  
 用戶端要求會造成伺服器執行一些命令，並傳回一些結果集。 **srv_senddone** 必須針對每一個結果集傳回結果完成訊息給用戶端。  
  
 *count* 欄位指出受到命令影響的資料列數。 如果 *count* 欄位包含計數，就應該在 *status* 欄位中設定 SRV_DONE_COUNT 旗標。 此設定可讓用戶端區分 0 的 *count* 值及未使用的 *count* 欄位。  
  
 請勿從 SRV_CONNECT 處理常式呼叫 **srv_senddone**。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
