---
title: c2 audit mode 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], C2 Audit Mode option
- C2 auditing
- C2 Audit Mode option
- recording attempts
ms.assetid: 5a8d73a6-c4f6-4967-ba11-ecbcfc90b9cc
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 2b962821437013f6aa086d472e284ed0fef21138
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799563"
---
# <a name="c2-audit-mode-server-configuration-option"></a>C2 稽核模式伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  C2 稽核模式可以透過 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 **sp_configure** 中的 [C2 稽核模式]  選項來設定。 選取這個選項，會將伺服器設定為將存取陳述式和物件的失敗嘗試和成功嘗試都記錄下來。 這項資訊可協助您分析系統活動並追蹤可能的安全性原則違規。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]通用條件憑證已取代 C2 安全性標準。 請參閱 [通用條件符合已啟用伺服器組態選項](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)。  
  
## <a name="audit-log-file"></a>稽核記錄檔  
 C2 稽核模式資料會儲存在執行個體之預設資料目錄的檔案中。 如果稽核記錄檔已達到 200 MB 的大小限制， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將建立新檔案、關閉舊檔案，並將所有新稽核記錄寫入新檔案。 在填滿稽核資料目錄或關閉稽核之前，會繼續進行這個程序。 若要判斷 C2 追蹤的狀態，請查詢 sys.traces 目錄檢視。  
  
> [!IMPORTANT]  
>  C2 稽核模式會將大量的事件資訊儲存到記錄檔，因此該記錄檔會快速成長。 如果儲存記錄檔的資料目錄已用盡空間， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將自行關閉。 如果將稽核設為自動啟動，您必須以 **-f** 旗標 (略過稽核) 重新啟動執行個體，或為稽核記錄釋放額外的磁碟空間。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="example"></a>範例  
 下列範例會開啟 C2 稽核模式。  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
sp_configure 'c2 audit mode', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
