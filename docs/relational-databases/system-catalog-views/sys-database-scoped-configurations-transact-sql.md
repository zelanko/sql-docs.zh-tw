---
title: sys.database_scoped_configurations & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: af6c2996877f4ab7d8a2305c4f6fe4b30a0127cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "64774564"
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含每個組態的一個資料列。 
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|組態選項的識別碼。|  
|**name**|**nvarchar(60)**|組態選項的名稱。 如需可能的組態資訊，請參閱[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|  
|**value**|**sqlvariant**|設定主要複本的這個組態選項的值。|  
|**value_for_secondary**|**sqlvariant**|設定次要複本的這個組態選項的值。|  
|**is_value_default**|**bit** |指定設定的值是否為預設值。|
  
##  <a name="Permissions"></a> 權限  
需要 **public** 角色的成員資格。  
  
## <a name="remarks"></a>備註  
當傳回 NULL 時做為值**value_for_secondary**，這表示，次要資料庫會設定為主要。  
 
資料庫範圍組態設定會伴隨著資料庫。 這意謂著還原或附加指定的資料庫時，現有的組態設定會持續存留。
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
