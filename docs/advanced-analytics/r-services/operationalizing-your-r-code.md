---
title: "運用您的 R 程式碼 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 運用您的 R 程式碼
  資料庫開發人員負責將多項技術整合在一起，並集結所有的結果，讓整個企業一起共用。 資料庫開發人員可與應用程式開發人員、SQL 開發人員及資料科學家合作，來設計解決方案、建議資料管理方法，以及架構和部署解決方案。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 開發人員使用資料科學家提供許多好處。  
  
-   **使用 R 指令碼進行互動 [!INCLUDE[tsql](../../includes/tsql-md.md)]。** 應用程式和資料庫開發人員，以及撰寫報表，分析師可以叫用的 R 指令碼呼叫系統預存程序。  
  
     如需基本語法的詳細資訊，請參閱 [sp_execute_external_script & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 和 [在 T-SQL 中使用 R 程式碼](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)。  
 
    如需如何操作 R 的擴充範例程式碼使用預存程序，請參閱 [SQL 開發人員的資料庫中分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)。
  
     與整合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也表示您可以執行 R 指令碼使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和應用程式中內嵌的結果。 例如，您可以建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表執行 R 指令碼，然後在報表中顯示，以及預測的繪圖。  
  
-   **效能和延展性。** 已知的開放原始碼 R 語言有限制，雖然 RevoScaleR 封裝 Api 所提供 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以處理大型資料集，並受益於多執行緒、 多核心、 多處理序的資料庫中計算。  
  
     您的 R 解決方案若是使用複雜的彙總或牽涉到大型資料集，就能運用 SQL 的高效率記憶體內彙總及資料行存放區索引，讓 R 程式碼能夠處理統計計算與評分。  
  
-   **標準的開發和管理工具。** 無須額外的工具就能管理或部署，只要叫用預存程式，就能呼叫所有的 R 作業。  
  
     此外，您針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料執行的相同 R 程式碼也可針對其他資料來源 (例如 Hadoop) 使用。  
  
 本章節描述您需要了解成功轉換 R 解決方案，並將它們部署到生產環境使用的概念 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。  
  
## 本節內容

[使用 R 資料類型](../../advanced-analytics/r-services/working-with-r-data-types.md)

[在 R Services 中使用轉換 R 程式碼](../../advanced-analytics/r-services/converting-r-code-for-use-in-r-services.md)

##  <a name="bkmk_RelatedTasks"></a> 相關工作  
  
[適用於 SQL Server R 調整服務效能](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
## 另請參閱  
 [SQL Server R 服務功能及工作](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 [sp_execute_external_script & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  
  