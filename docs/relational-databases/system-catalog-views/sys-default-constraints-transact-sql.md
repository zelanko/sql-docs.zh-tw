---
title: sys.databases default_constraints （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.default_constraints
- sys.default_constraints_TSQL
- default_constraints
- default_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.default_constraints catalog view
ms.assetid: 096e3659-edeb-4440-a016-f847acd6166b
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 816f5c563713eaa59337d765a7ccadafbd5c73a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079386"
---
# <a name="sysdefault_constraints-transact-sql"></a>sys.default_constraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  包含每個物件的資料列，這是預設定義（建立為 CREATE TABLE 或 ALTER TABLE 語句的一部分，而不是 CREATE DEFAULT 語句），具有**sys.databases。類型**= D。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<繼承自 sys.databases 的資料行>**||如需此視圖所繼承之資料行的清單，請參閱[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**parent_column_id**|**int**|此預設所屬**parent_object_id**中資料行的識別碼。|  
|**清晰**|**nvarchar(max)**|定義這個預設值的 SQL 運算式。|  
|**is_system_named**|**bit**|1 = 名稱是系統所產生。<br /><br /> 0 = 名稱是使用者所提供。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回已套用到 `VacationHours` 資料表中 `HumanResources.Employee` 資料行之 DEFAULT 條件約束的定義。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT d.definition   
FROM sys.default_constraints AS d  
INNER JOIN sys.columns AS c  
ON d.parent_object_id = c.object_id
AND d.parent_column_id = c.column_id  
WHERE d.parent_object_id = OBJECT_ID(N'HumanResources.Employee', N'U')  
AND c.name = 'VacationHours';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
