---
title: "sys.database_scoped_configurations (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/16/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84a4da130f637e85e4ebc950db5568f1fa8876f2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含每個組態的一個資料列。 
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|組態選項的識別碼。|  
|**name**|**nvarchar(60)**|組態選項的名稱。 如需可能的設定資訊，請參閱[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|  
|**value**|**sqlvariant**|此為主要複本的組態選項所設定的值。|  
|**value_for_secondary**|**sqlvariant**|設定次要複本的此組態選項的值。|  
  
##  <a name="Permissions"></a> Permissions  
 需要 **public** 角色中的成員資格。  
  
## <a name="remarks"></a>備註  
 當傳回做為值的 NULL **value_for_secondary**，這表示次要資料庫會設定為主要。  
 
 資料庫範圍的組態設定會繼續使用與資料庫。 這表示，當指定的資料庫還原或附加，現有的組態設定就會持續。
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
