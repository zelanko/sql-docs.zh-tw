---
description: sys.dm_xe_database_sessions (Azure SQL Database)
title: sys. dm_xe_database_sessions (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 33ea5179-16bb-4abd-96cc-9bc696e80987
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 4af2c0fafeae67291043d990c1bbaff175de9f5a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546377"
---
# <a name="sysdm_xe_database_sessions-azure-sql-database"></a>sys.dm_xe_database_sessions (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  傳回有關工作階段事件的資訊。 事件是不連續的執行點。 述詞可以套用至事件，以便在事件不包含必要資訊時阻止事件引發。  
  
||  
|-|  
|**適用于**： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何較新版本。|  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件工作階段的記憶體位址。 不可為 Null。|  
|event_name|**nvarchar(60)**|動作繫結之事件的名稱。 不可為 Null。|  
|event_package_guid|**uniqueidentifier**|包含此事件之封裝的 GUID。 不可為 Null。|  
|event_predicate|**nvarchar(2048)**|套用至事件之述詞樹狀結構的 XML 表示。 可為 Null。|  
  
## <a name="permissions"></a>權限  
 需要 VIEW DATABASE STATE 權限。  
  
### <a name="relationship-cardinalities"></a>關聯性基數  
從2015-07-13，' sys. dm_xe_objects ' 是在其名稱中未包含 ' _database ' 的其中一個 XEvents Dmv。 下表右邊的資料行不是錯誤或錯誤。 Microsoft SQL Server 和 Azure SQL Database 中的名稱相同。  
  
|寄件者|收件者|關聯性|  
|--------|------|----------------|  
|sys. dm_xe_database_session_events. event_session_address|sys. dm_xe_database_sessions 位址|多對一|  
|sys. dm_xe_database_session_events. event_package_guid、sys. dm_xe_database_session_events. event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|多對一|  
  
## <a name="see-also"></a>另請參閱  
[Azure SQL Database 中的擴充事件](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
[擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
 
