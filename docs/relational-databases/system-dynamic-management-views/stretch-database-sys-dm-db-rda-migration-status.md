---
title: "sys.dm_db_rda_migration_status (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_migration_status
- sys.dm_db_rda_migration_status_TSQL
- dm_db_rda_migration_status
- dm_db_rda_migration_status_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_rda_migration_status dynamic management view
ms.assetid: faf3901c-a0e0-4e0c-8b1b-86d9f15f34dd
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 088300f865265f330a06e40b7712fa63fd89f02a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>Stretch Database-sys.dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含一個資料列的每個已啟用 Stretch 的資料表上的本機執行個體的已移轉資料的每個批次[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 由其開始時間和結束時間識別批次。  
  
 **sys.dm_db_rda_migration_status**範圍是目前資料庫內容。 請確定您是在您要查看移轉狀態的啟用 「 延展 」 資料表的資料庫內容中。  
  
 在[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]的輸出**sys.dm_db_rda_migration_status**限制為 200 個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|要從中移轉的資料列之資料表的識別碼。|  
|**database_id**|**int**|資料列已從中移轉的資料庫識別碼。|  
|**migrated_rows**|**bigint**|這個批次中，移轉的資料列數目。|  
|**start_time_utc**|**datetime**|批次開始的 UTC 時間。|  
|**end_time_utc**|**datetime**|完成批次的 UTC 時間。|  
|**error_number**|**int**|如果批次失敗，發生; 之錯誤的錯誤號碼否則為 null。|  
|**error_severity**|**int**|如果批次失敗，發生; 之錯誤的嚴重性否則為 null。|  
|**error_state**|**int**|如果批次失敗，發生; 之錯誤的狀態否則為 null。<br /><br /> **Error_state**表示的條件或發生錯誤的位置。|  
  
## <a name="see-also"></a>請參閱＜  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
