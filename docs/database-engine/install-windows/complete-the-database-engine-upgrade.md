---
title: "完成資料庫引擎升級 | Microsoft Docs"
ms.custom: ""
ms.date: "09/22/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: 10
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 10
---
# 完成資料庫引擎升級
  升級至 SQL Server 2016 完成後，有一些您可能需要採取的其他步驟。 這些選項包括：  
  
 在升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 之後，請完成下列工作：  
  
-   **備份您的資料庫︰**為每個升級的資料庫執行完整備份。  
  
-   **啟用新功能︰**在 SQL Server 2016 中，某些變更只有在資料庫的 DATABASE_COMPATIBILITY 層級變更為 130 之後才會啟用。  如需詳細資訊及建議的工作流程，請參閱[變更資料庫相容性模式並使用查詢存放區](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)。  
  
-   **Integration Services：**  
  
     將 Integration Services 封裝移轉到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 格式。 如需詳細資訊，請參閱 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
-   **Reporting Services：**若為新的安裝升級，請還原 Reporting Services 加密金鑰。 如需詳細資訊，請參閱[備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/back-up-and-restore-reporting-services-encryption-keys.md)。  
  
-   **Master Data Services：**升級 MDS 資料庫結構描述，並建立 SQL Server 2016 Web 應用程式。 如需詳細資訊，請參閱[升級 Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md)。  
  
-   **Data Quality Services：**升級 DQS 資料庫結構描述，並驗證 DQS 資料庫結構描述升級。 如需詳細資訊，請參閱[升級 Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)。  
  
-   **全文檢索搜尋：**重新擴展全文檢索目錄以確保查詢結果中語意的一致性。 如需詳細資訊，請參閱[擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
## 這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
 您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Complete%20the%20Database%20Engine%20Upgrade%20page)  
  
  