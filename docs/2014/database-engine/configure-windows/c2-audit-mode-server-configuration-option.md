---
title: c2 audit mode 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
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
manager: craigg
ms.openlocfilehash: f631968f5570060441e22c18a9ee0b59d3e386d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48175538"
---
# <a name="c2-audit-mode-server-configuration-option"></a>C2 稽核模式伺服器組態選項
  C2 稽核模式可以透過 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 **sp_configure** 中的 [C2 稽核模式] 選項來設定。 選取這個選項，會將伺服器設定為將存取陳述式和物件的失敗嘗試和成功嘗試都記錄下來。 這項資訊可協助您分析系統活動並追蹤可能的安全性原則違規。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]通用條件憑證已取代 C2 安全性標準。 請參閱 [通用條件符合已啟用伺服器組態選項](common-criteria-compliance-enabled-server-configuration-option.md)。  
  
## <a name="audit-log-file"></a>稽核記錄檔  
 C2 稽核模式資料會儲存在執行個體之預設資料目錄的檔案中。 如果稽核記錄檔已達到 200 MB 的大小限制， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將建立新檔案、關閉舊檔案，並將所有新稽核記錄寫入新檔案。 在填滿稽核資料目錄或關閉稽核之前，會繼續進行這個程序。 若要判斷 C2 追蹤的狀態，請查詢 sys.traces 目錄檢視。  
  
> [!IMPORTANT]  
>  C2 稽核模式會將大量的事件資訊儲存到記錄檔，因此該記錄檔會快速成長。 如果儲存記錄檔的資料目錄已用盡空間， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將自行關閉。 如果將稽核設為自動啟動，您必須以 **-f** 旗標 (略過稽核) 重新啟動執行個體，或為稽核記錄釋放額外的磁碟空間。  
  
## <a name="permissions"></a>Permissions  
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
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
