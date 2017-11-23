---
title: "sys.database_scoped_configurations (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords: sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
caps.latest.revision: "13"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70b0f5c2ecb1f15828d5ac1c219033c337bb3a8f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含每個組態的一個資料列。 
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|組態選項的識別碼。|  
|**name**|**nvarchar （60)**|組態選項的名稱。 如需可能的設定資訊，請參閱[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|  
|**值**|**sqlvariant**|此為主要複本的組態選項所設定的值。|  
|**value_for_secondary**|**sqlvariant**|設定次要複本的此組態選項的值。|  
  
##  <a name="Permissions"></a> Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="remarks"></a>備註  
 當傳回做為值的 NULL **value_for_secondary**，這表示次要資料庫會設定為主要。  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
