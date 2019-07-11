---
title: sys.database_service_objectives (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- 彈性集區
- 彈性集區管理
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 1bd16b4ac7fb0b27296fb2cc7e47ec683d761ed4
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716653"
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>sys.database_service_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

傳回的版本 （服務層）、 服務目標 （定價層） 和彈性集區名稱，如果有的話，將 Azure SQL database 或 Azure SQL 資料倉儲。 如果登入 Azure SQL Database 伺服器中的 master 資料庫，傳回所有資料庫相關資訊。 針對 Azure SQL 資料倉儲，您必須連接到 master 資料庫。  
  
  
 如需定價資訊，請參閱[SQL Database 選項和效能：SQL Database 定價](https://azure.microsoft.com/pricing/details/sql-database/)並[SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。  
  
 若要變更服務設定，請參閱[ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)並[ALTER DATABASE （Azure SQL 資料倉儲）](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)。  
  
 Sys.database_service_objectives 檢視包含下列資料行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|ssNoversion|資料庫中的 Azure SQL Database 伺服器執行個體的唯一識別碼。 可與聯結[sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|版本|sysname|資料庫或資料倉儲服務層：**基本**， **Standard**， **Premium**或是**資料倉儲**。|  
|service_objective|sysname|資料庫的定價層。 如果資料庫是在彈性集區中，會傳回**ElasticPool**。<br /><br /> 在 **基本**層，會傳回**基本**。<br /><br /> **在標準服務層中的單一資料庫**傳回下列其中之一：S0、 S1、 S2、 S3、 S4、 S6、 S7、 S9 或 S12。<br /><br /> **進階層中的單一資料庫**傳回下列動作：P1、 P2、 P4、 P6、 P11 或 P15。<br /><br /> **SQL 資料倉儲**傳回 DW100 到 DW30000c。|  
|elastic_pool_name|sysname|名稱[彈性集區](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)所屬的資料庫。 傳回**NULL**如果資料庫是單一資料庫或資料 warehoue。|  
  
## <a name="permissions"></a>Permissions  
 需要**dbManager** master 資料庫的權限。  在資料庫層級中，使用者必須是建立者或擁有者。  
  
## <a name="examples"></a>範例  
 可以執行此範例中，master 資料庫或 Azure SQL Database 使用者資料庫。 查詢會傳回名稱、 服務和資料庫的效能層資訊。  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
