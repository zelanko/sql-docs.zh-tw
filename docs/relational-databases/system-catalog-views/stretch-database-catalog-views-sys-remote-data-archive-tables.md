---
title: sys.remote_data_archive_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_tables
- sys.remote_data_archive_tables_TSQL
- remote_data_archive_tables
- remote_data_archive_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_tables catalog view
ms.assetid: 765069b7-60fd-414c-875f-3455460b75cd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 65e42e6303b467abd38ddadb6be0c0d0fece46e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018187"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>Stretch Database 目錄檢視-sys.remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含針對每個遠端資料表會儲存從已啟用延展功能的本機資料表資料的一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|已啟用延展功能的本機資料表物件識別碼。|  
|**remote_database_id**|**int**|自動產生區域識別項的遠端資料庫。|  
|**remote_table_name**|**sysname**|對應到已啟用 Stretch 的資料表本機遠端資料庫中的資料表名稱。|  
|**filter_predicate**|**nvarchar(max)**|篩選述詞中，如果有的話，可識別要移轉的資料表中的資料列。 若值為 Null，則整個資料表都適合進行移轉。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 為資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)並[選取使用篩選述詞來移轉的資料列](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)。|  
|**migration_direction**|**tinyint**|在其中的資料目前正在移轉的方向。 以下是可用的值。<br/>1 （輸出）<br/>2 （輸入）|  
|**migration_direction_desc**|**nvarchar(60)**|在其中的資料目前正在移轉的方向的描述。 以下是可用的值。<br/>輸出 (1)<br/>輸入 (2)|  
|**is_migration_paused**|**bit**|指出是否移轉目前已暫停。|  
|**is_reconciled**|**bit**| 指出是否同步遠端資料表及 SQL Server 資料表。<br/><br/>當 windows 7 **is_reconciled**是 1 (true)，遠端資料表和 SQL Server 資料表會進行同步處理，您可以執行包含遠端資料的查詢。<br/><br/>當 windows 7 **is_reconciled**為 0 (false)、 遠端資料表和 SQL Server 資料表不同步。最近移轉的資料列必須一次移轉。 會發生這種情況是當您還原遠端的 Azure 資料庫中，或當您刪除資料列以手動方式從遠端資料表。 直到您協調資料表時，您無法執行，包含遠端資料的查詢。 若要先協調資料表，執行[sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)。 |  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

