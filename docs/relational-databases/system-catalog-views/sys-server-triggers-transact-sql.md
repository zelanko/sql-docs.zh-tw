---
title: "sys.server_triggers (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- server_triggers
- sys.server_triggers_TSQL
- server_triggers_TSQL
- sys.server_triggers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_triggers catalog view
ms.assetid: 25926ff4-9271-45bf-bc32-d5d3344bd47a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: efbd010533b9c11d974db2ae20c8455ce4274231
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sysservertriggers-transact-sql"></a>sys.server_triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含所有 object_type 為 TR 或 TA 的伺服器層級 DDL 觸發程序組。 CLR 觸發程序，在組件必須載入到**主要**資料庫。 所有的伺服器層級 DDL 觸發程序名稱，都在一個全域範圍內。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|觸發程序的名稱。|  
|**object_id**|**int**|物件的識別碼。|  
|**parent_class**|**tinyint**|父系的類別。 它一律是：<br /><br /> 100 = 伺服器|  
|**parent_class_desc**|**nvarchar （60)**|父類別的描述。 它一律是：<br /><br /> SERVER。|  
|**sys.internal_tables**|**int**|SERVER 上的觸發程序，一律為 0。|  
|**型別**|**char(2)**|物件類型：<br /><br /> TA = 組件 (CLR) 觸發程序<br /><br /> TR = SQL 觸發程序|  
|**type_desc**|**nvarchar （60)**|物件類型類別的描述。<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|建立觸發程序的日期。|  
|**modify_date**|**datetime**|上次利用 ALTER 陳述式來修改觸發程序的日期。|  
|**is_ms_shipped**|**bit**|利用內部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件來代表使用者所建立的觸發程序。|  
|**sys.indexes**|**bit**|1 = 觸發程序已停用。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
