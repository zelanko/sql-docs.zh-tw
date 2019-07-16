---
title: sys.database_automatic_tuning_options (TRANSACT-SQL) |Microsoft Docs
description: 了解如何檢視在 SQL Database 上的自動調整選項
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 437dbbc4ea7deb32a9723febb443cc67941fdc5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940229"
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>sys.database\_自動\_tuning_options & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  傳回這個資料庫的自動調整選項。  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|自動調整選項的名稱。 請參閱[ALTER DATABASE 設定 AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)如需可用的選項。|  
|**desired_state**|**smallint**|表示自動調整選項，明確地設定使用者的所需的作業模式。<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar(60)**|自動調整選項的所需的作業模式的文字描述。<br />OFF<br />ON|  
|**actual_state**|**smallint**|表示自動調整選項的作業模式。<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar(60)**|自動調整選項的實際作業模式的文字描述。<br />OFF<br />ON|  
|**reason**|**smallint**|表示實際和所需的狀態為何不同。<br />2 = 已停用<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|實際和所需的狀態不同的原因的文字描述。<br />停用 = 系統停用選項<br />QUERY_STORE_OFF = 查詢存放區已關閉<br />QUERY_STORE_READ_ONLY = 查詢存放區處於唯讀模式<br />NOT_SUPPORTED = 可用只能在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise edition| 
  
## <a name="permissions"></a>Permissions  
 需要 `VIEW DATABASE STATE` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [自動調整](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_query_store_options &#40;-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
