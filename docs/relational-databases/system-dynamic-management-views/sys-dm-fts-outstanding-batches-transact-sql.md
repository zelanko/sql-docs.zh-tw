---
description: sys.dm_fts_outstanding_batches (Transact-SQL)
title: sys.dm_fts_outstanding_batches (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_outstanding_batches
- dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches
dev_langs:
- TSQL
helpviewer_keywords:
- troubleshooting [SQL Server], full-text search
- sys.dm_fts_outstanding_batches dynamic management view
ms.assetid: c4d697ed-c906-4c28-b137-036a25e13c84
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 98faf34f1af430bfe870f8a9ea91fb1d751f0b52
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2020
ms.locfileid: "97323853"
---
# <a name="sysdm_fts_outstanding_batches-transact-sql"></a>sys.dm_fts_outstanding_batches (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回有關每個全文檢索索引批次的資訊。  
  
  |資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**int**|資料庫的識別碼|  
|catalog_id|**int**|全文檢索目錄的識別碼|  
|table_id|**int**|包含全文檢索索引之資料表識別碼的識別碼。|  
|batch_id|**int**|批次識別碼|  
|memory_address|**varbinary(8)**|批次物件記憶體位址|  
|crawl_memory_address|**varbinary(8)**|搜耙物件記憶體位址 (父物件)|  
|memregion_memory_address|**varbinary(8)**|篩選背景程式主機 (fdhost.exe) 之輸出共用記憶體的記憶體區域記憶體位址|  
|hr_batch|**int**|此批次最近一次的錯誤碼|  
|is_retry_batch|**bit**|指示這是否為重試批次：<br /><br /> 0 = 否<br /><br /> 1 = 是|  
|retry_hints|**int**|批次所需的重試類型：<br /><br /> 0 = 無重試<br /><br /> 1 = 多執行緒重試<br /><br /> 2 = 單一執行緒重試<br /><br /> 3 = 單一和多執行緒重試<br /><br /> 5 = 多執行緒最後重試<br /><br /> 6 = 單一執行緒最後重試<br /><br /> 7 = 單一和多執行緒最後重試|  
|retry_hints_description|**nvarchar(120)**|所需之重試類型的描述：<br /><br /> NO RETRY<br /><br /> MULTI THREAD RETRY<br /><br /> SINGLE THREAD RETRY<br /><br /> SINGLE AND MULTI THREAD RETRY<br /><br /> MULTI THREAD FINAL RETRY<br /><br /> SINGLE THREAD FINAL RETRY<br /><br /> SINGLE AND MULTI THREAD FINAL RETRY|  
|doc_failed|**bigint**|批次中失敗的文件數目|  
|batch_timestamp|**timestamp**|建立批次時取得的時間戳記值。|  
  
## <a name="permissions"></a>權限  

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在 SQL Database Basic、S0 和 S1 服務目標上，以及針對彈性集區中的資料庫，則 `Server admin` `Azure Active Directory admin` 需要或帳戶。 在所有其他 SQL Database 服務目標上， `VIEW DATABASE STATE` 資料庫中都需要有許可權。   
  
## <a name="examples"></a>範例  
 下列範例會了解目前針對伺服器執行個體內每一個資料表所處理的批次數。  
  
```  
SELECT database_id, table_id, COUNT(*) AS batch_count FROM sys.dm_fts_outstanding_batches GROUP BY database_id, table_id ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的全文檢索搜尋和語義搜尋動態管理檢視和函數 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)  
  
  
