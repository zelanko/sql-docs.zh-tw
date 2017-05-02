---
title: "Oracle 發行者的備份與還原 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- recovery [SQL Server replication], Oracle publishing
- backups [SQL Server replication], Oracle publishing
- Oracle publishing [SQL Server replication], backup and restore
- restoring [SQL Server replication], Oracle publishing
ms.assetid: e5f181d0-cacf-442b-8b7a-202b3cfc358b
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 802d157cd886f5656513904c0b519a65b61d67b3
ms.lasthandoff: 04/11/2017

---
# <a name="backup-and-restore-for-oracle-publishers"></a>Oracle 發行者的備份與還原
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  在備份與還原時，請遵循下列指導方針：  
  
-   確定「記錄讀取器代理程式」未執行，並且已發行資料表中的其他資料庫活動不會在備份「發行者」時出現。  
  
-   同時備份「發行者」和「散發者」。  
  
-   如果必須還原「發行者」或「散發者」，請重新初始化所有訂閱。  
  
-   若要從備份還原「訂閱者」(無需重新初始化訂閱)，則在上次訂閱資料庫備份完成後，傳遞到散發資料庫的交易必須仍然可用。 交易的時間長短可視散發保留設定而定。 如需這些設定的詳細資訊，請參閱[訂閱逾期與停用](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
-   如果「發行者」或「散發者」在還原資料庫後無法變得不一致，則複寫代理程式將記錄錯誤訊息。 此時，您必須卸除並重新建立所有相關的發行集和訂閱：  
  
    1.  為發行集和訂閱的定義編寫指令碼。 如需詳細資訊，請參閱 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
         如果發行集定義在「發行者」與「散發者」各版本之間作變更，則您需要修改指令碼。  
  
    2.  卸除發行集和訂閱。  
  
    3.  執行在步驟 1 中建立的指令碼。  
  
     如果必須卸除並重新設定「發行者」，請使用 **CASCADE** 選項卸除 **MSSQLSERVERDISTRIBUTOR** 公用同義字和設定的 Oracle 複寫使用者，以便從「Oracle 發行者」上移除所有複寫物件。  
  
## <a name="see-also"></a>另請參閱  
 [備份及還原複寫的資料庫](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
