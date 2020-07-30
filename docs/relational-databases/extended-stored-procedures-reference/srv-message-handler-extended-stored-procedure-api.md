---
title: srv_message_handler (擴充預存程序 API)
description: 瞭解 srv_message_handler 以及它如何呼叫已安裝的擴充預存程式 API 訊息處理常式。
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_message_handler
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_message_handler
ms.assetid: 41bcd057-436f-4fa8-8293-fc8057a30877
author: rothja
ms.author: jroth
ms.openlocfilehash: 2edc96558c00b43dfe9d9b346ad75c32b42af1cd
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332353"
---
# <a name="srv_message_handler-extended-stored-procedure-api"></a>srv_message_handler (擴充預存程序 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 呼叫安裝的擴充預存程序 API 訊息處理常式。 此函數通常用來 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 從擴充預存程式呼叫，以便在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔中記錄錯誤（由擴充預存程式所定義）。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_message_handler (  
SRV_PROC *  
srvproc  
,  
int  
errornum  
,  
BYTE   
severity  
,  
BYTE  
state  
,  
int  
oserrnum  
,  
char *  
errtext  
,  
int  
errtextlen  
,  
char *  
oserrtext  
,  
int  
oserrtextlen  
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼。 *srvproc* 參數所包含的資訊可用來管理應用程式與用戶端之間的通訊和資料。  
  
 *errornum*  
 這是擴充預存程序所定義的錯誤號碼。 這個數字的範圍必須是從 50,001 到 2,147,483,647。  
  
 *severity*  
 這是錯誤的標準 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 嚴重性值。 這個數字的範圍必須是從 0 到 24。  
  
 *state*  
 這是錯誤的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 狀態值。  
  
 *oserrnum*  
 這是作業系統錯誤號碼。 忽略這個引數。  
  
 *errtext*  
 這是擴充預存程序錯誤 *errornum* 的描述。  
  
 *errtextlen*  
 這是擴充預存程序錯誤字串 *errtext* 的長度。  
  
 *oserrtext*  
 這是作業系統錯誤 *oserrnum* 的描述。 忽略這個引數。  
  
 *oserrtextlen*  
 這是作業系統錯誤字串 *oserrtext* 的長度。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **srv_message_handler** 函式讓擴充預存程序可以與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的集中式錯誤記錄和報告功能進行整合。 您可以從擴充預存程序為事件建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 警示，而 SQL Server Agent 會針對這些警示條件進行監視。  
  
 如果錯誤訊息較長，就會截斷為 412 個位元組。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://msdn.microsoft.com/security/)。  
  
  
