---
title: "手動容錯移轉資料庫鏡像工作階段 (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "容錯移轉 [SQL Server], 資料庫鏡像"
  - "手動容錯移轉 [SQL Server]"
  - "資料庫鏡像 [SQL Server], 容錯移轉"
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
caps.latest.revision: 32
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 32
---
# 手動容錯移轉資料庫鏡像工作階段 (Transact-SQL)
  鏡像資料庫已同步處理時 (亦即，資料庫為 SYNCHRONIZED 狀態時)，資料庫擁有者可以初始化至鏡像伺服器的手動容錯移轉。 手動容錯移轉只能從主體伺服器中起始。  
  
### 手動容錯移轉資料庫鏡像工作階段  
  
1.  連接到主體伺服器。  
  
2.  將資料庫內容設定為 **master** 資料庫：  
  
     **USE master;**  
  
3.  在主體伺服器上發出下列陳述式：  
  
     [ALTER DATABASE](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md) *database_name* SET PARTNER FAILOVER，其中 *database_name* 是鏡像資料庫。  
  
     如此可將鏡像伺服器立即轉換為主體角色。  
  
 在先前的主體伺服器上，用戶端與資料庫的連接會中斷，進行中的交易則會回復。  
  
> [!NOTE]  
>  在容錯移轉發生時，凡是已利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器準備好但尚未認可的交易，都會在資料庫完成容錯移轉後視為已中止。  
  
## 另請參閱  
 [ALTER DATABASE 資料庫鏡像 &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [手動容錯移轉資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)   
 [資料庫鏡像工作階段期間的角色切換 &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)  
  
  