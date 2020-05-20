---
title: sys.dm_xe_database_session_object_columns
titleSuffix: Azure SQL Database
ms.custom: seo-dt-2019
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 0e6adc54-4d97-4ef0-bf4f-b4538d69f136
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d24f6413d9641b58795dc9950aba27dae974d7b1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826702"
---
# <a name="sysdm_xe_database_session_object_columns-azure-sql-database"></a>sys.dm_xe_database_session_object_columns (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  顯示繫結至工作階段之物件的組態值。  
  
||  
|-|  
|**適用**于： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更新版本。|  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件工作階段的記憶體位址。 與 sys.databases 具有多對一關聯性。 dm_xe_database_sessions 位址。 不可為 Null。|  
|column_name|**nvarchar(60)**|組態值的名稱。 不可為 Null。|  
|column_id|**int**|資料行的識別碼。 在物件中，這是唯一的。 不可為 Null。|  
|column_value|**nvarchar(2048)**|資料行的設定值。 可為 Null。|  
|object_type|**nvarchar(60)**|物件的型別。  不可為 null。 object_type 是下列其中一個：<br /><br /> event<br /><br /> 目標|  
|object_name|**nvarchar(60)**|這個資料行所屬之物件的名稱。 不可為 Null。|  
|object_package_guid|**uniqueidentifier**|包含物件之封裝的 GUID。 不可為 Null。|  
  
## <a name="permissions"></a>權限  
 需要 VIEW DATABASE STATE 權限。  
  
### <a name="relationship-cardinalities"></a>關聯性基數  
  
|從|至|關聯性|  
|----------|--------|------------------|  
|dm_xe_database_session_object_columns。 object_name<br /><br /> dm_xe_database_session_object_columns。 object_package_guid|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|多對一|  
|dm_xe_database_session_object_columns。 column_name<br /><br /> dm_xe_database_session_object_columns。 column_id|sys.dm_xe_object_columns.name<br /><br /> sys.dm_xe_object_columns.column_id|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
