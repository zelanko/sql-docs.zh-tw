---
title: sys.databases dm_db_rda_migration_status （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 21e5230e4f3efd86fe90382202f0b21a0187a214
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67937067"
---
# <a name="stretch-database---sysdm_db_rda_migration_status"></a>Stretch Database-sys. dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  針對本機實例上每個已啟用 Stretch 的資料表，各包含一個資料列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 批次是由其開始時間和結束時間所識別。  
  
 **dm_db_rda_migration_status**的範圍是目前的資料庫內容。 請確定您位於您想要查看其遷移狀態之 Stretch-enable 資料表的資料庫內容中。  
  
 在[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]中， **sys. dm_db_rda_migration_status**的輸出限制為200個數據列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|資料列遷移來源之資料表的識別碼。|  
|**database_id**|**int**|資料列遷移來源所在的資料庫識別碼。|  
|**migrated_rows**|**Bigint**|在此批次中遷移的資料列數目。|  
|**start_time_utc**|**datetime**|批次開始的 UTC 時間。|  
|**end_time_utc**|**datetime**|批次完成的 UTC 時間。|  
|**error_number**|**int**|如果批次失敗，則為發生錯誤的錯誤號碼;否則為 null。|  
|**error_severity**|**int**|如果批次失敗，則為發生之錯誤的嚴重性;否則為 null。|  
|**error_state**|**int**|如果批次失敗，則為發生的錯誤狀態;否則為 null。<br /><br /> **Error_state**指出發生錯誤的條件或位置。|  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
