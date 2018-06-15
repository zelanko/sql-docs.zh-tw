---
title: sys.remote_data_archive_tables (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5d71c317ef36f254f83af70b3b4a2b2428fcbfa4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32974643"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>Stretch Database 目錄檢視-sys.remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含已啟用延展功能的本機資料表中的資料會儲存每個遠端資料表的一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|已啟用 Stretch 的本機資料表物件識別碼。|  
|**remote_database_id**|**int**|自動產生本機識別碼的遠端資料庫。|  
|**remote_table_name**|**sysname**|對應已啟用 Stretch 的資料表本機至遠端資料庫中的資料表名稱。|  
|**filter_predicate**|**nvarchar(max)**|篩選器述詞中，如果有的話，可識別要移轉的資料表中的資料列。 若值為 Null，則整個資料表都適合進行移轉。<br /><br /> 如需詳細資訊，請參閱[針對資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)和[選取使用篩選器述詞來移轉的資料列](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)。|  
|**migration_direction**|**tinyint**|在其中目前移轉資料的方向。 可用的值如下所示。<br/>1 （輸出）<br/>2 （輸入）|  
|**migration_direction_desc**|**nvarchar(60)**|在其中資料目前正在移轉的方向的描述。 可用的值如下所示。<br/>輸出 (1)<br/>輸入 (2)|  
|**is_migration_paused**|**bit**|指出是否移轉目前已暫停。|  
|**is_reconciled**|**bit**| 指出是否同步遠端資料表及 SQL Server 資料表。<br/><br/>當值**is_reconciled**為 1 (true)、 遠端資料表和 SQL Server 資料表是否為同步，而且您可以執行包含遠端資料的查詢。<br/><br/>當值**is_reconciled**為 0 (false)、 遠端資料表和 SQL Server 資料表不同步。最近已移轉的資料列必須再次移轉。 會發生這種情況是當您還原遠端 Azure 資料庫，或當您刪除資料列以手動方式從遠端資料表。 除非您先協調資料表，您無法執行，包含遠端資料的查詢。 若要先協調資料表，執行[sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)。 |  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

