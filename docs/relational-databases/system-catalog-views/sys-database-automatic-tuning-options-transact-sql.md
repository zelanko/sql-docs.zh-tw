---
title: "sys.database_automatic_tuning_options (TRANSACT-SQL) |Microsoft 文件"
description: "瞭解如何檢視 SQL database 的自動微調選項"
ms.custom: 
ms.date: 07/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs:
- TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: 
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4208b9e294273444c24ac9e3a05e60b43d4274c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>sys.database\_automatic\_tuning_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  傳回這個資料庫的自動調整選項。  

|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|自動微調選項的名稱。 請參閱[ALTER DATABASE SET AUTOMATIC_TUNING &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)可用選項。|  
|**desired_state**|**smallint**|表示自動調整的選項，明確地設定使用者的所需的作業模式。<br />0 = OFF<br />1 = ON |  
|**desired_state_desc**|**nvarchar(60)**|所需的作業模式自動微調選項的文字描述。<br />OFF<br />ON|  
|**actual_state**|**smallint**|表示自動微調選項的作業模式。<br />0 = OFF<br />1 = ON |  
|**actual_state_desc**|**nvarchar(60)**|自動微調選項的實際作業模式的文字描述。<br />OFF<br />ON|  
|**reason**|**smallint**|表示實際和所需的狀態為何不同。<br />2 = 已停用<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|實際和所需的狀態為何不同的原因的文字描述。<br />停用 = 系統會停用選項<br />QUERY_STORE_OFF = 查詢存放區已關閉<br />QUERY_STORE_READ_ONLY = 查詢存放區處於唯讀模式<br />NOT_SUPPORTED = 可用只有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise edition| 
  
## <a name="permissions"></a>Permissions  
 需要`VIEW DATABASE STATE`權限。  
  
## <a name="see-also"></a>另請參閱  
 [自動調整](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
