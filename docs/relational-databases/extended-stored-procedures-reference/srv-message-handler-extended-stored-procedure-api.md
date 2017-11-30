---
title: "srv_message_handler (擴充預存程序 API) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_message_handler
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_message_handler
ms.assetid: 41bcd057-436f-4fa8-8293-fc8057a30877
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb7035564c0247098181f633dbdd2aef53551d9f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="srvmessagehandler-extended-stored-procedure-api"></a>srv_message_handler (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 呼叫安裝的擴充預存程序 API 訊息處理常式。 此函式通常用來從擴充預存程序呼叫 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔中記錄錯誤 (由擴充預存程序定義)。  
  
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
 這是作業系統錯誤號碼。 會忽略這個引數。  
  
 *errtext*  
 這是擴充預存程序錯誤 *errornum* 的描述。  
  
 *errtextlen*  
 這是擴充預存程序錯誤字串 *errtext* 的長度。  
  
 *oserrtext*  
 這是作業系統錯誤 *oserrnum* 的描述。 會忽略這個引數。  
  
 *oserrtextlen*  
 這是作業系統錯誤字串 *oserrtext* 的長度。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **srv_message_handler** 函式讓擴充預存程序可以與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的集中式錯誤記錄和報告功能進行整合。 您可以從擴充預存程序為事件建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 警示，而 SQL Server Agent 會針對這些警示條件進行監視。  
  
 如果錯誤訊息較長，就會截斷為 412 個位元組。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
  
