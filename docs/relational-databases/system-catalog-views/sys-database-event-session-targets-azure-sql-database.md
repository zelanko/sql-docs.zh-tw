---
title: "sys.database_event_session_targets (Azure SQL Database) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: Azure SQL Database
ms.assetid: 38d775ee-1fe1-4820-88c6-02b2f875a66b
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e06bf788cb8d5b2b66a1470fff431015d2df0ec
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatabaseeventsessiontargets-azure-sql-database"></a>sys.database_event_session_targets (Azure SQL Database)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回事件工作階段中每一個事件目標的資料列。  
  
||  
|-|  
|**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 及任何更新的版本。|  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件工作階段的識別碼。 不可為 Null。|  
|target_id|**int**|目標的識別碼。 這個識別碼在事件工作階段物件中是唯一的。 不可為 Null。|  
|name|**sysname**|事件目標的名稱。 不可為 Null。|  
|封裝|**sysname**|包含此事件目標之事件封裝的名稱。 不可為 Null。|  
|module|**sysname**|包含此事件目標之模組的名稱。 不可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW DATABASE STATE 權限。  
  
## <a name="remarks"></a>備註  
 此檢視有下列關聯性基數。  
  
||||  
|-|-|-|  
|來源|若要|關聯性|  
|sys.database_event_session_targets.event_session_id|sys.database_event_sessions.event_session_id|多對一|  
  
## <a name="see-also"></a>請參閱＜  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
