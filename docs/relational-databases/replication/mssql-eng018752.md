---
description: MSSQL_ENG018752
title: MSSQL_ENG018752 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018752 error
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 50ff8dde3d4c15217630500b07786674b518afc1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473389"
---
# <a name="mssql_eng018752"></a>MSSQL_ENG018752
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|18752|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|一次只有一個記錄讀取器代理程式或記錄檔相關程序 (sp_repldone, sp_replcmds, and sp_replshowcmds) 可連接到資料庫。 若您已執行記錄檔相關程序，請卸除執行程序的連接，或者利用該連接執行 sp_replflush 之後，再啟動記錄讀取器代理程式或執行其他記錄檔相關程序。|  
  
## <a name="explanation"></a>說明  
 目前有多個連接嘗試執行下列任一項目： **sp_repldone**、 **sp_replcmds** 或 **sp_replshowcmds**。 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) 和 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 是一種預存程序，可供記錄讀取器代理程式在已發行資料庫中尋找及更新已複寫異動的資訊。 [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) 預存程序是用來對特定類型的異動複寫問題進行疑難排解。  
  
 此錯誤在下列情況下產生：  
  
-   如果已發行資料庫的「記錄讀取器代理程式」正在執行，而第二個「記錄讀取器代理程式」嘗試針對相同的資料庫執行，則錯誤就會在第二個代理程式中產生，並且出現在代理程式記錄中。  
  
     若出現多個代理程式的情況，則可能其中一個代理程式是被遺棄處理的結果。  
  
-   如果已發行資料庫的「記錄讀取器代理程式」已啟動，而使用者針對相同的資料庫執行 **sp_repldone**、 **sp_replcmds** 或 **sp_replshowcmds** ，則錯誤就會在執行預存程序 (例如 **sqlcmd**) 的應用程式中產生。  
  
-   如果已發行資料庫的「記錄讀取器代理程式」未在執行，且使用者執行了 **sp_repldone**、 **sp_replcmds** 或 **sp_replshowcmds** ，之後也未關閉執行該程序的連接，則當「記錄讀取器代理程式」嘗試連接到資料庫時就會產生錯誤。  
  
## <a name="user-action"></a>使用者動作  
 下列步驟可以幫助您對此問題進行疑難排解。 如果任一步驟允許「記錄讀取器代理程式」在沒有錯誤的情況下啟動，則無需完成剩餘步驟。  
  
-   檢查「記錄讀取器代理程式」的記錄，以便尋找可能導致此錯誤的其他任何錯誤。 如需有關在「複寫監視器」中檢視代理程式狀態和錯誤詳細資料的資訊，請參閱[使用複寫監視器來檢視資訊及執行工作](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
-   檢查 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) 的輸出，以尋找連接到已發行資料庫之特定處理序識別碼 (SPID)。 關閉可能已執行 **sp_repldone**、 **sp_replcmds** 或 **sp_replshowcmds** 的任何連接。  
  
-   重新啟動「記錄讀取器代理程式」。 如需詳細資訊，請參閱[啟動和停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
-   在「散發者」上重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務 (使其在叢集中離線或上線)。 如果已排程作業可能已經從其他任何 **執行個體執行** sp_repldone **、** sp_replcmds **或** sp_replshowcmds [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則重新啟動那些執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。 如需詳細資訊，請參閱[啟動、停止或暫停 SQL Server Agent 服務](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)。  
  
-   在發行集資料庫上的「發行者」端執行 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)，然後重新啟動記錄讀取器代理程式。  
  
-   若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和 (或) 其他錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [複寫記錄讀取器代理程式](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
