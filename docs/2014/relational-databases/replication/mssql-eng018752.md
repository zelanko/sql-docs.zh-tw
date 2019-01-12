---
title: MSSQL_ENG018752 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018752 error
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0558ded6ed10284df39270ddeca9d92434daf40e
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133728"
---
# <a name="mssqleng018752"></a>MSSQL_ENG018752
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|18752|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|一次只有一個記錄讀取器代理程式或記錄檔相關程序 (sp_repldone, sp_replcmds, and sp_replshowcmds) 可連接到資料庫。 若您已執行記錄檔相關程序，請卸除執行程序的連接，或者利用該連接執行 sp_replflush 之後，再啟動記錄讀取器代理程式或執行其他記錄檔相關程序。|  
  
## <a name="explanation"></a>說明  
 目前有多個連接嘗試執行下列任一項目： **sp_repldone**、 **sp_replcmds**或 **sp_replshowcmds**。 [sp_repldone &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldone-transact-sql) 和 [sp_replcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql) 是一種預存程序，可供記錄讀取器代理程式在已發行資料庫中尋找及更新已複寫異動的資訊。 [sp_replshowcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql) 預存程序是用來對特定類型的異動複寫問題進行疑難排解。  
  
 此錯誤在下列情況下產生：  
  
-   如果已發行資料庫的「記錄讀取器代理程式」正在執行，而第二個「記錄讀取器代理程式」嘗試針對相同的資料庫執行，則錯誤就會在第二個代理程式中產生，並且出現在代理程式記錄中。  
  
     若出現多個代理程式的情況，則可能其中一個代理程式是被遺棄處理的結果。  
  
-   如果已發行資料庫的「記錄讀取器代理程式」已啟動，而使用者針對相同的資料庫執行 **sp_repldone**、 **sp_replcmds**或 **sp_replshowcmds** ，則錯誤就會在執行預存程序 (例如 **sqlcmd**) 的應用程式中產生。  
  
-   如果已發行資料庫的「記錄讀取器代理程式」未在執行，且使用者執行了 **sp_repldone**、 **sp_replcmds**或 **sp_replshowcmds** ，之後也未關閉執行該程序的連接，則當「記錄讀取器代理程式」嘗試連接到資料庫時就會產生錯誤。  
  
## <a name="user-action"></a>使用者動作  
 下列步驟可以幫助您對此問題進行疑難排解。 如果任一步驟允許「記錄讀取器代理程式」在沒有錯誤的情況下啟動，則無需完成剩餘步驟。  
  
-   檢查「記錄讀取器代理程式」的記錄，以便尋找可能導致此錯誤的其他任何錯誤。 在複寫監視器中檢視代理程式狀態和錯誤詳細資料的相關資訊，請參閱[View Information and Perform Tasks 使用 「 複寫監視器](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
-   檢查 [sp_who &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) 的輸出，以尋找連接到已發行資料庫之特定處理序識別碼 (SPID)。 關閉可能已執行 **sp_repldone**、 **sp_replcmds**或 **sp_replshowcmds**的任何連接。  
  
-   重新啟動「記錄讀取器代理程式」。 如需詳細資訊，請參閱[啟動和停止複寫代理程式 &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
-   在「散發者」上重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務 (使其在叢集中離線或上線)。 如果已排程作業可能已經從其他任何 **執行個體執行**sp_repldone **、** sp_replcmds **或** sp_replshowcmds [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則重新啟動那些執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。 如需詳細資訊，請參閱[啟動、停止或暫停 SQL Server Agent 服務](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)。  
  
-   在發行集資料庫上的「發行者」端執行 [sp_replflush &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replflush-transact-sql)，然後重新啟動記錄讀取器代理程式。  
  
-   若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和 (或) 其他錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)   
 [複寫記錄讀取器代理程式](agents/replication-log-reader-agent.md)  
  
  
