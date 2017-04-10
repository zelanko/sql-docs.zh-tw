---
title: "管理和監視 R 方案 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# 管理和監視 R 方案
  資料庫管理員必須將競爭專案和優先順序整合至單一窗口︰資料庫伺服器。 他們不只應將資料存取權提供給資料科學家，還必須提供給各種報表開發人員、商務分析人員和商務資料取用者，同時維護操作和報告資料存放區的健康情況。 在企業中，DBA 是建置與部署適用於資料科學之有效基礎結構的一個重要部分。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 若要支援的資料科學角色的資料庫系統管理員提供許多好處。  
  
-   **安全性。** 架構的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會將資料庫保留在安全和隔離的資料庫執行個體的作業 R 工作階段執行。  
  
     您可以指定有權執行 R 指令碼的對象，並確保 R 工作中使用的資料是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中所定義之相同安全性角色來管理。  
  
-   **可靠性。** R 工作階段會在不同處理序中執行，以確保即使 R 工作階段發生問題，您的伺服器還是會如往常般繼續執行。 低權限之實體的使用者帳戶用來包含和隔離 R 執行個體。   
  
-   **資源管理。** 您可以控制配置給 R 執行階段的資源數量，以避止從大量計算危及整體伺服器效能。  
  
  
## 本節內容  
 [監視 R 服務](../../advanced-analytics/r-services/monitoring-r-services.md)
 
 [R 服務的資源管理](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
 
[安裝和管理的 R 封裝](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)
  
[組態](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 

+ [設定及管理進階分析擴充功能](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)  
  
+  [修改 SQL Server R 服務的使用者帳戶集區](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  

 [在 SQL Server 中 R 執行階段的安全性考量](../../advanced-analytics/r-services/security-considerations-for-the-r-runtime-in-sql-server.md)  
  
 
  
## 另請參閱  
 [SQL Server R 服務功能及工作](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
  