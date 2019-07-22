---
title: 完成資料庫引擎升級 | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.technology: install
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 72c5ff1bcb2162bbe3f3584222214ba448b67d68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054280"
---
# <a name="complete-the-database-engine-upgrade"></a>完成資料庫引擎升級

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

升級 SQL Server 完成之後，您可能需要採取一些其他步驟。 這些選項包括：  
  
在升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]之後，請完成下列工作：  
  
- **備份資料庫：** 執行每個資料庫的完整備份。  

- **啟用新功能：** 在 SQL Server 2016 和 SQL Server 2017 中，某些變更只有在資料庫的 DATABASE_COMPATIBILITY 層級變更至 130 或更高之後才會啟用。  如需詳細資訊及建議的工作流程，請參閱 [變更資料庫相容性模式並使用查詢存放區](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)。 如果您的資料庫具有在 SQL Server 2014 中建立的記憶體最佳化資料表，請檢閱[記憶體最佳化資料表的統計資料](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md)。
  
- **Integration Services：**  
  
     將 Integration Services 封裝移轉到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 格式。 如需詳細資訊，請參閱 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
- **Reporting Services：** 若為新的安裝升級，請還原 Reporting Services 加密金鑰。 如需詳細資訊，請參閱 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。  
  
- **Master Data Services：** 升級 MDS 資料庫結構描述，並建立 SQL Server 2017 Web 應用程式。 如需詳細資訊，請參閱 [升級 Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md)。  
  
- **Data Quality Services：** 升級 DQS 資料庫結構描述，並驗證 DQS 資料庫結構描述升級。 如需詳細資訊，請參閱 [升級 Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)。  
  
- **全文檢索搜尋：** 為確保查詢結果中語意的一致性，必須重新擴展全文檢索目錄。 如需詳細資訊，請參閱 [擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
