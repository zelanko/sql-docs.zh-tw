---
title: sys.database_service_objectives
titleSuffix: Azure SQL Database
ms.custom: seo-dt-2019
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- 彈性集區
- 彈性集區，管理
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 465416e87966ba3a80c8e98394c0b1f2009f591b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73844455"
---
# <a name="sysdatabase_service_objectives-azure-sql-database"></a>sys.database_service_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

傳回 Azure SQL database 或 Azure SQL 資料倉儲的版本（服務層級）、服務目標（定價層）和彈性集區名稱（如果有的話）。 若已登入 Azure SQL Database 伺服器中的 master 資料庫，則傳回所有資料庫的相關資訊。 對於 Azure SQL 資料倉儲，您必須連線到 master 資料庫。  
  
  
 如需價格的相關資訊，請參閱[SQL Database 選項和效能： SQL Database 定價](https://azure.microsoft.com/pricing/details/sql-database/)和[SQL 資料倉儲定價](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。  
  
 若要變更服務設定，請參閱[ALTER database （Azure SQL Database）](../../t-sql/statements/alter-database-azure-sql-database.md)和[alter database （Azure SQL 資料倉儲）](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)。  
  
 [Sys.databases database_service_objectives] 視圖包含下列資料行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|int|資料庫的識別碼，在 Azure SQL Database server 的實例內是唯一的。 Joinable 與[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|edition|sysname|資料庫或資料倉儲的服務層級：**基本**、**標準**、 **Premium**或**資料倉儲**。|  
|service_objective|sysname|資料庫的定價層。 如果資料庫在彈性集區中，則會傳回**ElasticPool**。<br /><br /> 在**基本**層，會傳回**basic**。<br /><br /> **標準服務層級中的單一資料庫**會傳回下列其中一項： S0、S1、S2、S3、S4、S6、S7、S9 或 S12。<br /><br /> **Premium 層中的單一資料庫**會傳回下列內容： P1、P2、P4、P6、P11 或 P15。<br /><br /> **SQL 資料倉儲**會透過 DW30000C 傳回 DW100。<br /><br /> 如需詳細資訊，請參閱[單一資料庫](/azure/sql-database/sql-database-dtu-resource-limits-single-databases/)、[彈性](/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools/)集區、[資料](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu/)倉儲|  
|elastic_pool_name|sysname|資料庫所屬的[彈性集](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)區名稱。 如果資料庫是單一資料庫或資料 warehoue，則會傳回**Null** 。|  
  
## <a name="permissions"></a>權限  
 需要 master 資料庫的**dbManager**許可權。  在資料庫層級，使用者必須是「建立者」或「擁有者」。  
  
## <a name="examples"></a>範例  
 這個範例可以在 master 資料庫或 Azure SQL Database 使用者資料庫上執行。 此查詢會傳回資料庫的名稱、服務和效能層級資訊。  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
