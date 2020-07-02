---
title: srv_rpcoptions (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcoptions
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcoptions
ms.assetid: dbcce5d1-d5a1-4379-9597-04e43af5923d
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a4bc6bf4a8fe1b600ec7bd7b3ba1877023751db
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755882"
---
# <a name="srv_rpcoptions-extended-stored-procedure-api"></a>srv_rpcoptions (擴充預存程序 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回目前遠端預存程序的執行階段選項。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBUSMALLINT srv_rpcoptions ( SRV_PROC *  
srvproc   
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (在這個狀況之下，該控制代碼會收到遠端預存程序)。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
## <a name="returns"></a>傳回  
 是點陣圖，包含聯結在目前遠端預存程序的邏輯 OR 之執行階段旗標。 如果沒有目前遠端預存程序，則會傳回 0 ，並且產生訊息。  
  
## <a name="remarks"></a>備註  
 下表描述每個執行階段旗標。  
  
|執行階段旗標|描述|  
|--------------------|-----------------|  
|SRV_NOMETADATA|用戶端已要求不含中繼資料資訊的結果。 只有在用戶端與實例通訊時，才會使用這個旗標 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 擴充預存程序 API 應用程式無法省略中繼資料資訊。|  
|SRV_RECOMPILE|用戶端已經要求先重新編譯遠端預存程序，再執行它。 這個旗標可能無法套用至擴充預存程序 API 應用程式。|  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
