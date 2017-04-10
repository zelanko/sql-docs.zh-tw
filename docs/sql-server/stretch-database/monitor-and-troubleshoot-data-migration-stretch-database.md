---
title: "監視和疑難排解資料移轉 (Stretch Database) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/14/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Stretch Database，監視"
  - "監視 Stretch Database"
ms.assetid: 06950858-8c02-4ec6-9c59-42b787316a2d
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# 監視和疑難排解資料移轉 (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  若要在 Stretch Database 監視器中監視資料移轉，請針對 SQL Server Management Studio 中的資料庫，選取 [工作 | Stretch | 監視]。  
  
## 在 Stretch Database 監視器中檢查資料移轉的狀態  
 針對 SQL Server Management Studio 中的資料庫選取 [工作 | Stretch | 監視]，以開啟 Stretch Database 監視器並監視資料移轉。  
  
-   監視器的上半部會顯示啟用延展的 SQL Server 資料庫與遠端 Azure 資料庫的一般資訊。  
  
-   監視的下半部會顯示資料庫中每個已啟用延展的資料表資料移轉狀態。  
  
 ![Stretch Database Monitor](../../sql-server/stretch-database/media/stretch-monitor.PNG "Stretch Database Monitor")  
  
##  <a name="Migration"></a> 在動態管理檢視中檢查資料移轉狀態  
 開啟動態管理檢視 **sys.dm_db_rda_migration_status** 查看已移轉的批次和資料列數目。 如需詳細資訊，請參閱 [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../Topic/sys.dm_db_rda_migration_status%20\(Transact-SQL\).md)。  
  
##  <a name="Firewall"></a> 對資料移轉進行疑難排解  
 **已啟用延展的資料表資料列沒有移轉到 Azure。 是什麼問題？**  
 有幾個問題會影響移轉。 請檢查下列事項。  
  
-   檢查 SQL Server 電腦的網路連線。  
  
-   檢查 Azure 防火牆是否封鎖 SQL Server 連線到遠端端點。  
  
-   查看動態管理檢視 **sys.dm_db_rda_migration_status** 以取得最新批次的狀態。 如果發生錯誤，請檢查批次的 error_number、error_state 和 error_severity 各值。  
  
    -   如需檢視的詳細資訊，請參閱 [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../Topic/sys.dm_db_rda_migration_status%20\(Transact-SQL\).md)。  
  
    -   如需 SQL Server 錯誤訊息內容的詳細資訊，請參閱 [sys.messages &#40;Transact-SQL&#41;](../Topic/sys.messages%20\(Transact-SQL\).md)。  
  
 **Azure 防火牆封鎖了我的本機伺服器連線。**  
 您可能要在 Azure 伺服器的 Azure 防火牆設定中加入規則，讓 SQL Server 與遠端的 Azure 伺服器進行通訊。  
  
## 另請參閱  
 [管理 Stretch Database 並對其進行疑難排解](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  