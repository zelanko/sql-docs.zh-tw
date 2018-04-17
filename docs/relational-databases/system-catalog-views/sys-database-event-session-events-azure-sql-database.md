---
title: sys.database_event_session_events (Azure SQL Database) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.service: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
ms.assetid: f4c9eb0a-173c-4c66-8dd8-6f7176b2657f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1bb0aba27809cbf8588449f4cfe779389585736e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysdatabaseeventsessionevents-azure-sql-database"></a>sys.database_event_session_events (Azure SQL Database)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回事件工作階段中每一個事件的資料列。  
  
||  
|-|  
|**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 及任何更新的版本。|  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件工作階段的識別碼。 不可為 Null。|  
|event_id|**int**|事件的識別碼。 這個識別碼在事件工作階段物件中是唯一的。 不可為 Null。|  
|name|**sysname**|事件的名稱。 不可為 Null。|  
|封裝|**sysname**|包含此事件之事件封裝的名稱。 不可為 Null。|  
|module|**sysname**|包含此事件之模組的名稱。 不可為 Null。|  
|predicate|**nvarchar(3000)**|套用至事件的述詞運算式。 可為 Null。|  
|predicate_xml|**nvarchar(3000)**|套用至事件的 XML 述詞運算式。 可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW DATABASE STATE 權限。  
  
## <a name="remarks"></a>備註  
 此檢視有下列關聯性基數。  
  
||||  
|-|-|-|  
|來源|若要|關聯性|  
|sys.database_event_session_events.event_session_id|sys.database_event_sessions.event_session_id|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
