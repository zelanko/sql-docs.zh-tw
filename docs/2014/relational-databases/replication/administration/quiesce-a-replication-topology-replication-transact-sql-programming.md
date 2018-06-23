---
title: 停止複寫拓撲 (複寫 Transact-SQL 程式設計) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- administering replication, quiescing
- quiesce [SQL Server replication]
- transactional replication, backup and restore
ms.assetid: 7626d575-9994-47be-b772-5b6f1b7ef7ca
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 01a72047c0dfc83dcb39be6749d523db228fd727
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034763"
---
# <a name="quiesce-a-replication-topology-replication-transact-sql-programming"></a>停止複寫拓撲 (複寫 Transact-SQL 程式設計)
  *「停止」* (Quiesce) 系統包括停止所有節點上已發行資料表的活動，並確定每個節點已收到來自其他所有節點的所有變更。 本主題說明如何停止複寫拓撲 (此為數項管理工作所需)，以及如何確定節點已從其他節點接收到所有變更。  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-read-only-subscriptions"></a>若要使用唯讀訂閱停止異動複寫拓撲  
  
1.  停止在「發行者」端的所有已發行資料表上的活動。  
  
2.  在發行集資料庫的發行者端，執行 [sp_posttracertoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql)。  
  
3.  在發行集資料庫的「發行者」端，執行 [sp_helptracertokenhistory](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql)。  
  
4.  確保每個「訂閱者」已接收追蹤 Token。  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-updatable-subscriptions"></a>若要使用可更新的訂閱停止異動複寫拓撲  
  
1.  停止在「發行者」端和所有「訂閱者」端的所有已發行資料表上的活動。  
  
2.  如果任何「訂閱者」使用佇列更新訂閱：  
  
    1.  如果「佇列讀取器代理程式」並非以連續模式執行，請執行該代理程式。 如需執行代理程式的詳細資訊，請參閱[複寫代理程式可執行檔概念](../concepts/replication-agent-executables-concepts.md)或[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
    2.  若要確認佇列是空的，請在每個「訂閱者」端執行 [sp_replqueuemonitor](/sql/relational-databases/system-stored-procedures/sp-replqueuemonitor-transact-sql) 。  
  
3.  在發行集資料庫的「發行者」端，執行 [sp_posttracertoken](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql)。  
  
4.  在發行集資料庫的「發行者」端，執行 [sp_helptracertokenhistory](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql)。  
  
5.  確保每個「訂閱者」已接收追蹤 Token。  
  
### <a name="to-quiesce-a-peer-to-peer-transactional-replication-topology"></a>若要停止點對點異動複寫拓撲  
  
1.  停止在所有節點的所有已發行資料表上的活動。  
  
2.  在拓撲中的每個發行集資料庫上執行 [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) 。  
  
3.  如果「記錄讀取器代理程式」或「散發代理程式」並非以連續模式執行，請執行該代理程式。 「記錄讀取器代理程式」必須在「散發代理程式」之前啟動。 如需執行代理程式的詳細資訊，請參閱[複寫代理程式可執行檔概念](../concepts/replication-agent-executables-concepts.md)或[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
4.  在拓撲中的每個發行集資料庫上執行 [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql) 。 確定結果集包含其他每個節點的回應。  
  
### <a name="to-ensure-a-peer-to-peer-node-has-received-all-prior-changes"></a>若要確定對等節點已接收所有先前的變更  
  
1.  在您所檢查之節點的發行集資料庫上執行 [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) 。  
  
2.  如果「記錄讀取器代理程式」或「散發代理程式」並非以連續模式執行，請執行該代理程式。 「記錄讀取器代理程式」必須在「散發代理程式」之前啟動。 如需執行代理程式的詳細資訊，請參閱[複寫代理程式可執行檔概念](../concepts/replication-agent-executables-concepts.md)或[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
3.  在您所檢查之節點的發行集資料庫上執行 [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql) 。 確定結果集包含其他每個節點的回應。  
  
### <a name="to-quiesce-a-merge-replication-topology"></a>若要停止合併式複寫拓撲  
  
1.  停止在「發行者」端和所有「訂閱者」端的所有已發行資料表上的活動。  
  
2.  針對每項訂閱執行合併代理程式兩次：同步處理所有訂閱一次，然後再同步處理每個訂閱一次。 這可確保所有的變更都會複寫到所有節點。 如需執行代理程式的詳細資訊，請參閱[複寫代理程式可執行檔概念](../concepts/replication-agent-executables-concepts.md)或[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
    > [!NOTE]  
    >  如果在同步處理期間發生衝突，則在執行「合併代理程式」兩次之後，衝突解決所需的變更有可能不會傳播到所有節點。  
  
## <a name="see-also"></a>另請參閱  
 [管理點對點拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [針對異動複寫測量延遲及驗證連接](../monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
