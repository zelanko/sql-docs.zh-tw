---
title: srv_rpcowner (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcowner
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcowner
ms.assetid: e81a60e6-14ea-47bc-a11c-3d7635344447
author: rothja
ms.author: jroth
ms.openlocfilehash: b589d55c8e30e3882ebb25bc46c51bc382e3e2df
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050577"
---
# <a name="srv_rpcowner-extended-stored-procedure-api"></a>srv_rpcowner (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回目前遠端預存程序的擁有者元件。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBCHAR * srv_rpcowner (  
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
 這是整數變數的指標，此變數會接收擁有者名稱的長度。 參數 *len* 可以是 NULL，在此情況下將不會傳回擁有者元件的長度。  
  
## <a name="returns"></a>傳回  
 DBCHAR 指標，指向目前遠端預存程序之以 null 結尾的擁有者元件。 如果目前沒有遠端預存程序，則會傳回 NULL 且 *len* 設定為 - 1。  
  
## <a name="remarks"></a>備註  
 此函數只會傳回遠端預存程序的擁有者元件。 這不包含名稱、遠端預存程序名稱和遠端預存程序號碼的選擇性規範。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
