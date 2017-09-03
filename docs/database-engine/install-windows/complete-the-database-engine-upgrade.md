---
title: "完成資料庫引擎升級 | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 581e8cd7a43dd1e4c878cc56b49644e51d7a3a79
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="complete-the-database-engine-upgrade"></a>完成資料庫引擎升級

升級 SQL Server 完成之後，您可能需要採取一些其他步驟。 這些選項包括：  
  
在升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]之後，請完成下列工作：  
  
- **備份資料庫**︰為每個資料庫執行完整備份。  

- **啟用新功能**︰在 SQL Server 2016 和 SQL Server 2017 中，某些變更只有在資料庫的 DATABASE_COMPATIBILITY 層級變更為 130 或更大值之後才會啟用。  如需詳細資訊及建議的工作流程，請參閱 [變更資料庫相容性模式並使用查詢存放區](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)。  
  
- **Integration Services：**  
  
     將 Integration Services 封裝移轉到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 格式。 如需詳細資訊，請參閱 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
- **Reporting Services：** 若為新的安裝升級，請還原 Reporting Services 加密金鑰。 如需詳細資訊，請參閱 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。  
  
- **Master Data Services**：升級 MDS 資料庫結構描述，並建立 SQL Server 2017 Web 應用程式。 如需詳細資訊，請參閱 [升級 Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md)。  
  
- **Data Quality Services：** 升級 DQS 資料庫結構描述，並驗證 DQS 資料庫結構描述升級。 如需詳細資訊，請參閱 [升級 Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)。  
  
- **全文檢索搜尋：** 重新擴展全文檢索目錄以確保查詢結果中語意的一致性。 如需詳細資訊，請參閱 [擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  

