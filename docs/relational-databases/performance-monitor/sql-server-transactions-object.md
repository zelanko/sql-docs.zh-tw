---
title: "SQL Server 的 Transactions 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:Transactions
- Transactions object
ms.assetid: 85240267-78fd-476a-9ef6-010d6cf32dd8
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 642a22206b25ec2963fae4fa04e6b10a5329f0e6
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-transactions-object"></a>SQL Server 的 Transactions 物件
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 Transactions 物件會提供計數器，可監視 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的使用中交易數，以及這些交易在資源上產生的影響，例如 **tempdb** 中的快照隔離資料列版本存放區。 交易是邏輯工作單位；必須全部成功或全部從資料庫清除的一組作業，才能維持資料的邏輯完整性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的所有資料修改都是透過交易來完成。  
  
 資料庫設定為允許快照隔離等級時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須維護資料庫中每個資料列的修改記錄。 每次修改資料列時， **tempdb**的資料列版本存放區會記錄修改之前的資料列副本。 **Transaction** 物件中有許多計數器，可用來監視 **tempdb**中資料列版本存放區的大小和成長率。  
  
 **Transactions** 物件計數器會報告一個 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體中的所有交易。  
  
 下表描述 **SQLServer:Transactions** 計數器。  
  
|SQL Server Transactions 計數器|描述|  
|--------------------------------------|-----------------|  
|**Free Space in tempdb (KB)**|**tempdb**中可用的空間量 (以 KB 為單位)。 必須有足夠的可用空間，以容納快照隔離等級版本存放區和這個 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體中建立的所有新暫存物件。|  
|**Longest Transaction Running Time**|自交易啟動以來的時間長度 (以秒為單位)，此交易在其他任何目前的交易中維持最久的使用狀態。 當資料庫是在讀取認可快照隔離層級之下時，此計數器只會顯示活動。 如果資料庫是在其他任何隔離等級中，則不會記錄任何活動。|  
|**NonSnapshot Version Transactions**|目前使用中的交易數，這些交易未使用快照隔離等級，且已修改資料而在 **tempdb** 版本存放區產生資料列版本。|  
|**Snapshot Transactions**|目前使用快照隔離等級的使用中交易數。<br /><br /> 注意： **Snapshot Transactions** 物件計數器會在第一次進行資料存取時回應，而不是在發出 `BEGIN TRANSACTION` 陳述式時回應。|  
|**Transactions**|目前使用中的所有類型之交易數。|  
|**Update conflict ratio**|使用快照隔離等級的交易在上一秒內發生更新衝突的百分比。 快照隔離等級交易嘗試修改資料列時，如果先前有另一個交易已修改此資料列，但在快照隔離等級交易啟動時尚未認可此交易，這時就會發生更新衝突。|  
|**Update conflict ratio base**|僅供內部使用。|
|**Update Snapshot Transactions**|目前使用快照隔離等級且已修改資料的使用中交易數。|  
|**Version Cleanup rate (KB/s)**|從 **tempdb**的快照隔離版本存放區中移除資料列版本的速度 (KB/sec)。|  
|**Version Generation rate (KB/s)**|新資料列版本加入 **tempdb**之快照隔離版本存放區的速度 (KB/sec)。|  
|**Version Store Size (KB)**|**tempdb** 中用來儲存快照隔離等級資料列版本的空間量 (以 KB 為單位)。|  
|**Version Store unit count**|**tempdb**中快照隔離版本存放區的使用中配置單位數。|  
|**Version Store unit creation**|自從 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體啟動之後，已在快照隔離存放區中建立的配置單位數。|  
|**Version Store unit truncation**|自從 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體啟動之後，已從快照隔離存放區中移除的配置單位數。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
