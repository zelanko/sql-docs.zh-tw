---
title: sys.databases database_automatic_tuning_options （Transact-sql） |Microsoft Docs
description: 瞭解如何在 SQL Database 上查看自動調整選項
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67940229"
---
# <a name="sysdatabase_automatic_tuning_options-transact-sql"></a>sys.databases\_自動\_tuning_options （transact-sql）
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  傳回此資料庫的自動調整選項。  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|自動調整選項的名稱。 如需可用的選項，請參閱[ALTER DATABASE SET AUTOMATIC_TUNING &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) 。|  
|**desired_state**|**smallint**|表示自動調整選項所需的作業模式，由使用者明確設定。<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**Nvarchar （60）**|自動調整選項所需作業模式的文字描述。<br />OFF<br />開啟|  
|**actual_state**|**smallint**|表示自動調整選項的作業模式。<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**Nvarchar （60）**|自動調整選項實際作業模式的文字描述。<br />OFF<br />開啟|  
|**原因**|**smallint**|指出實際和 desired 狀態為何不同。<br />2 = 已停用<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**Nvarchar （60）**|實際和所需狀態為何不同的文字描述。<br />DISABLED = 選項已由系統停用<br />QUERY_STORE_OFF = 查詢存放區已關閉<br />QUERY_STORE_READ_ONLY = 查詢存放區處於唯讀模式<br />NOT_SUPPORTED = 僅適用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition| 
  
## <a name="permissions"></a>權限  
 需要 `VIEW DATABASE STATE` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [自動調整](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [dm_db_tuning_recommendations &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
