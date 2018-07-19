---
title: sys.dm_db_rda_migration_status (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_migration_status
- sys.dm_db_rda_migration_status_TSQL
- dm_db_rda_migration_status
- dm_db_rda_migration_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_rda_migration_status dynamic management view
ms.assetid: faf3901c-a0e0-4e0c-8b1b-86d9f15f34dd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e0ee1d106a9f52dd30518f9ead02847dc879ff2c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38048766"
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>Stretch Database-sys.dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含每個批次的每個已啟用 Stretch 的資料表上的本機執行個體的移轉資料的一個資料列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 批次是由其開始時間] 和 [結束時間識別。  
  
 **sys.dm_db_rda_migration_status**範圍為目前的資料庫內容。 請確定您是在您要查看移轉狀態已啟用 「 延展資料表的資料庫內容。  
  
 在  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，輸出**sys.dm_db_rda_migration_status**限制為 200 個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|要從中移轉的資料列之資料表的識別碼。|  
|**database_id**|**int**|資料列已從中移轉的資料庫識別碼。|  
|**migrated_rows**|**bigint**|這個批次中，移轉的資料列數目。|  
|**start_time_utc**|**datetime**|批次開始的 UTC 時間。|  
|**end_time_utc**|**datetime**|批次完成 UTC 時間。|  
|**error_number**|**int**|如果批次失敗，發生錯誤的錯誤號碼否則為 null。|  
|**error_severity**|**int**|如果批次失敗，發生錯誤的嚴重性否則為 null。|  
|**error_state**|**int**|如果批次失敗，發生錯誤的狀態否則為 null。<br /><br /> **Error_state**指示的條件或發生錯誤的位置。|  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
