---
title: sys.databases remote_data_archive_tables （Transact-sql） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018187"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_tables"></a>Stretch Database 目錄 Views-sys. remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  針對每個遠端資料表，各包含一個資料列，其中儲存已啟用延展功能之本機資料表中的資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|已啟用 Stretch 之本機資料表的物件識別碼。|  
|**remote_database_id**|**int**|自動產生的遠端資料庫本機識別碼。|  
|**remote_table_name**|**sysname**|遠端資料庫中對應至已啟用延展功能之本機資料表的資料表名稱。|  
|**filter_predicate**|**nvarchar(max)**|篩選器述詞（如果有的話），用來識別要遷移之資料表中的資料列。 如果值為 Null，便代表整個資料表皆符合移轉資格。<br /><br /> 如需詳細資訊，請參閱[啟用資料表的 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)和[使用篩選器述詞選取要遷移的資料列](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)。|  
|**migration_direction**|**tinyint**|目前正在遷移資料的方向。 可用的值如下所示。<br/>1（輸出）<br/>2（輸入）|  
|**migration_direction_desc**|**Nvarchar （60）**|目前正在遷移資料之方向的描述。 可用的值如下所示。<br/>輸出（1）<br/>輸入（2）|  
|**is_migration_paused**|**bit**|指出遷移目前是否已暫停。|  
|**is_reconciled**|**bit**| 指出遠端資料表和 SQL Server 資料表是否同步。<br/><br/>當**is_reconciled**的值為1（true）時，遠端資料表和 SQL Server 資料表會同步，而且您可以執行包含遠端資料的查詢。<br/><br/>當**is_reconciled**的值為0（false）時，遠端資料表和 SQL Server 資料表不會同步。最近遷移的資料列必須重新遷移。 當您還原遠端 Azure 資料庫，或從遠端資料表手動刪除資料列時，就會發生這種情況。 在您協調資料表之前，您無法執行包含遠端資料的查詢。 若要協調資料表，請執行[sys. sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)。 |  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

