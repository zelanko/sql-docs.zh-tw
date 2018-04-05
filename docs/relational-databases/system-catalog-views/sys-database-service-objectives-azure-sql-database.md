---
title: sys.database_service_objectives (Azure SQL Database) |Microsoft 文件
ms.custom: ''
ms.date: 08/30/2016
ms.prod: ''
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
keywords:
- 彈性集區
- 彈性集區管理
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
caps.latest.revision: 16
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 40f4d0d98cd33a57d6ab1e6f9c46ebd2174c9a15
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2018
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>sys.database_service_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

傳回版本 （服務層）、 （定價層） 的服務目標與彈性集區名稱，如果有的話，Azure SQL database 或 Azure SQL 資料倉儲。 如果登入至 master 資料庫中的 Azure SQL Database 伺服器，傳回所有資料庫相關資訊。 Azure SQL 資料倉儲，您必須連接到 master 資料庫。  
  
  
 如需定價資訊，請參閱[SQL Database 選項及效能： SQL Database 定價](https://azure.microsoft.com/en-us/pricing/details/sql-database/)和[SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。  
  
 若要變更服務設定，請參閱[ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)和[ALTER DATABASE （Azure SQL 資料倉儲）](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)。  
  
 Sys.database_service_objectives 檢視包含下列資料行。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|database_id|int|資料庫中的 Azure SQL Database 伺服器執行個體的唯一識別碼。 可加入與[sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|版本|sysname|資料庫或資料倉儲的服務層：**基本**，**標準**， **Premium**，**一般用途**， **重要商務資料**，或**資料倉儲**。|  
|service_objective|sysname|資料庫的定價層。 如果資料庫是彈性集區中，會傳回**ElasticPool**。<br /><br /> 在**基本**層，傳回**基本**。<br /><br /> Standard 服務層中的單一資料庫傳回此階層的目前有效值。<br /><br /> Premium 層中的單一資料庫傳回針對此服務層目前有效的值。<br /><br />一般用途的服務層中的單一資料庫傳回針對此服務層目前有效的值。<br /><br />商務關鍵性的服務層中的單一資料庫傳回針對此服務層目前有效的值。<br /><br /> SQL 資料倉儲的 SQL 資料倉儲，傳回目前有效的值。|  
|elastic_pool_name|sysname|名稱[彈性集區](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)所屬的資料庫。 傳回**NULL**如果資料庫是單一資料庫或資料 warehoue。|  
  
## <a name="permissions"></a>Permissions  
 需要**dbManager** master 資料庫的權限。  在資料庫層級中，使用者必須建立者或擁有者。  
  
## <a name="examples"></a>範例  
 可以執行此範例中，使用者資料庫或主要資料庫上。 查詢會傳回名稱、 服務和資料庫的效能層資訊。  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
