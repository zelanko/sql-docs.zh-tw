---
title: MSSQL_ENG021797 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021797 error
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 88f9fff576b52e83073bbf917a43edf0a7648086
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63023583"
---
# <a name="mssqleng021797"></a>MSSQL_ENG021797
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|21797|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|'%s' 必須是有效的 Windows 登入，格式：'MACHINE\Login' 或 'DOMAIN\Login'。 請參閱 '%s' 的文件集。|  
  
## <a name="explanation"></a>說明  
 如果為 **@job_login** 參數指定的值為 Null 或無效，則此錯誤是由下列複寫預存程序引發。 如果 **db_owner** 固定資料庫角色成員從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行指令碼，則可能發生此錯誤。 安全性模型在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中已變更，同時必須更新這些指令碼。  
  
-   [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)  
  
-   [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql)  
  
-   [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)  
  
-   [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)  
  
-   [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)  
  
-   [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)  
  
-   [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)  
  
 這些預存程序可由適當伺服器上的 **sysadmin** 固定伺服器角色之成員執行，或可由適當資料庫中的 **db_owner** 固定資料庫角色之成員來執行。 每個預存程序均會建立一個代理程式作業，並允許您指定代理程式執行所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 對於 **sysadmin** 角色中的使用者，即使未指定 Windows 帳戶(如果帳戶已指定，則其必須是有效帳戶)，也會隱含建立代理程式作業；代理程式會在適當伺服器端的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式服務帳戶內容下執行。 雖然不需要此帳戶，但安全性最佳做法是為代理程式指定不同的帳戶。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](security/replication-agent-security-model.md)。  
  
## <a name="user-action"></a>使用者動作  
 確定為每個程序的 **@job_login** 參數指定有效的 Windows 帳戶。 若您有上一版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]複寫指令碼，請更新這些指令碼以納入 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]所需的預存程序和參數。 如需詳細資訊，請參閱[升級複寫指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
