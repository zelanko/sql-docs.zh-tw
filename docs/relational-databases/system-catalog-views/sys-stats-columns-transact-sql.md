---
title: sys.stats_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- stats_columns_TSQL
- stats_columns
- sys.stats_columns
- sys.stats_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.stats_columns catalog view
ms.assetid: 93414d07-97e9-4501-8577-f35b8d68fbe9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f173a21db91f5566caea01114865a228d0f34ec5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62854802"
---
# <a name="sysstatscolumns-transact-sql"></a>sys.stats_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  包含屬於的每個資料行的資料列**sys.stats**統計資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|這個資料行所屬的物件識別碼。|  
|**stats_id**|**int**|這個資料行所屬的統計資料識別碼。<br /><br />如果統計資料對應到索引， *stats_id*值是相同*index_id*中的值[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目錄檢視。|  
|**stats_column_id**|**int**|在統計資料行集當中，以 1 為基底的序數。|  
|**column_id**|**int**|從資料行的識別碼**sys.columns**。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
 [統計資料](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)  
  
  
