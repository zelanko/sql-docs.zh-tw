---
title: "srv_setutype (擴充預存程序 API) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_setutype
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a5a94b2cae880ab79ce97768e7666c352a16db23
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="srvsetutype-extended-stored-procedure-api"></a>srv_setutype (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 針對資料列中的資料行設定使用者定義資料類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_setutype (  
SRV_PROC *  
srvproc  
,  
int   
column  
,   
DBINT  
user_type   
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *column*  
 指出要設定的資料行。 資料行的編號會從 1 開始。  
  
 *user_type*  
 指定使用者定義資料類型程式碼。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。 如果此資料行不存在，則會傳回 FAIL。  
  
## <a name="remarks"></a>備註  
 一個資料行有兩個資料類型：其實際資料類型與其使用者定義資料類型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用使用者定義資料類型來儲存資料行的實際使用者定義資料類型，以及資料行描述資訊 (如果有的話)，例如資料行的可 NULL 性和可更新性。  
  
 利用 **srv_describe** 定義 *column* 時，以及最後一個資料列送出之前，可以呼叫 **srv_setutype** 函式。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_describe &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
