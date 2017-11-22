---
title: MSSQL_ENG014151 | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG014151 error
ms.assetid: 54b45e70-46b3-4c7a-a5bf-06f6dd028ceb
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fe57faa9cfded07a70e5b47c910b03734f717c65
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="mssqleng014151"></a>MSSQL_ENG014151
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|14151|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|複寫 -%s：代理程式 %s 失敗。 %s|  
  
## <a name="explanation"></a>說明  
 任何複寫代理程式的失敗均會導致錯誤。 訊息結尾處的文字視失敗的內容而定。  
  
## <a name="user-action"></a>使用者動作  
 此錯誤在許多情況下都會出現；請視需要使用下列方法：  
  
-   重新啟動失敗的代理程式，查看現在執行是否已無錯誤。 如需詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
-   請檢查代理程式記錄和作業記錄是否同時發生其他錯誤。 如需有關檢視代理程式狀態以及複寫監視器中的錯誤詳細資料，請參閱下列主題：  
  
    -   如需了解快照集代理程式、記錄讀取器代理程式和佇列讀取器代理程式，請參閱[檢視與發行集相關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)。  
  
    -   如需了解散發代理程式和合併代理程式，請參閱[檢視與訂閱相關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
-   確認在由代理程式存取的電腦之間是否使用基本連接，然後使用類似 [sqlcmd Utility](../../tools/sqlcmd-utility.md)的公用程式連接到各台電腦。 連接時，請使用代理程式建立連接的相同帳戶。 如需各代理程式帳戶所需權限的詳細資訊，請參閱＜ [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
-   如果在建立或套用快照集時發生錯誤，則請檢查快照集目錄中的檔案以找到錯誤。  
  
-   若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和 (或) 其他錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [複寫散發代理程式](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [複寫記錄讀取器代理程式](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [複寫合併代理程式](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [複寫佇列讀取器代理程式](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
