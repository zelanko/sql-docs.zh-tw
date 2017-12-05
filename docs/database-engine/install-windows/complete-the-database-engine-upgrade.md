---
title: "完成資料庫引擎升級 | Microsoft Docs"
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: "10"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: f02ff71df24b1e1a8f6c17fd8c6edbdfa02c60a5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="complete-the-database-engine-upgrade"></a>完成資料庫引擎升級
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] SQL Server 升級完成後，您可能需要採取一些其他步驟。 這些選項包括：  
  
在升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]之後，請完成下列工作：  
  
- **備份資料庫**︰為每個資料庫執行完整備份。  

- **啟用新功能**︰在 SQL Server 2016 和 SQL Server 2017 中，某些變更只有在資料庫的 DATABASE_COMPATIBILITY 層級變更為 130 或更大值之後才會啟用。  如需詳細資訊及建議的工作流程，請參閱 [變更資料庫相容性模式並使用查詢存放區](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)。 如果您的資料庫具有在 SQL Server 2014 中建立的記憶體最佳化資料表，請檢閱[記憶體最佳化資料表的統計資料](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md)。
  
- **Integration Services：**  
  
     將 Integration Services 封裝移轉到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 格式。 如需詳細資訊，請參閱 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
- **Reporting Services：** 若為新的安裝升級，請還原 Reporting Services 加密金鑰。 如需詳細資訊，請參閱 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。  
  
- **Master Data Services**：升級 MDS 資料庫結構描述，並建立 SQL Server 2017 Web 應用程式。 如需詳細資訊，請參閱 [升級 Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md)。  
  
- **Data Quality Services：** 升級 DQS 資料庫結構描述，並驗證 DQS 資料庫結構描述升級。 如需詳細資訊，請參閱 [升級 Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)。  
  
- **全文檢索搜尋：** 重新擴展全文檢索目錄以確保查詢結果中語意的一致性。 如需詳細資訊，請參閱 [擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
