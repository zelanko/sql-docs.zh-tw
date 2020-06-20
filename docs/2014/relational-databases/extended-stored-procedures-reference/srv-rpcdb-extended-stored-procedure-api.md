---
title: srv_rpcdb (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcdb
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcdb
ms.assetid: d52bfd22-7a7c-4ab0-af65-df96ff359e6f
author: rothja
ms.author: jroth
ms.openlocfilehash: 581b8b6514ddeb7f6a55ac797ab838f933a702f2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050627"
---
# <a name="srv_rpcdb-extended-stored-procedure-api"></a>srv_rpcdb (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回目前遠端預存程序的資料庫名稱元件。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBCHAR * srv_rpcdb (  
SRV_PROC * srvproc,int *len );  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *len*  
 `int` 變數的指標，此變數會接收資料庫名稱的長度。 如果 *len* 為 NULL，則不會傳回資料庫名稱的長度。  
  
## <a name="returns"></a>傳回  
 目前遠端預存程序的資料庫名稱部分以 null 結尾字串的 DBCHAR 指標。 如果沒有目前遠端預存程序，則會傳回 NULL 且 *len* 參數設定為 - 1。  
  
## <a name="remarks"></a>備註  
 函數只會傳回遠端預存程序物件名稱的資料庫元件。 其中不包含擁有人、遠端預存程序名稱和遠端預存程序號碼的選擇性規範。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
