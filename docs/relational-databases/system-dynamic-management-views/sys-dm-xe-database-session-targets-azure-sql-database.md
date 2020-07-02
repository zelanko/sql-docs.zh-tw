---
title: sys.dm_xe_database_session_targets
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 7cc1e66845d07dca1dcb5efeb597751fc3ae55e9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85675974"
---
# <a name="sysdm_xe_database_session_targets-azure-sql-database"></a>sys.dm_xe_database_session_targets (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  會傳回工作階段目標的相關資訊。  
  
||  
|-|  
|**適用**于： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何未來版本。|  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件工作階段的記憶體位址。 與 sys.databases 具有多對一關聯性。 dm_xe_database_sessions 位址。 不可為 Null。|  
|target_name|**nvarchar(60)**|工作階段內的目標名稱。 不可為 Null。|  
|target_package_guid|**uniqueidentifier**|包含目標之封裝的 GUID。 不可為 Null。|  
|execution_count|**bigint**|此目標已針對工作階段執行的次數。 不可為 Null。|  
|execution_duration_ms|**bigint**|此目標已經執行的總時間 (以毫秒為單位)。 不可為 Null。|  
|target_data|**nvarchar(max)**|此目標所維護的資料，例如事件彙總資訊。 可為 Null。|  
  
## <a name="permissions"></a>權限  
 需要 VIEW DATABASE STATE 權限。  
  
### <a name="relationship-cardinalities"></a>關聯性基數  
  
|從|至|關聯性|  
|----------|--------|------------------|  
|dm_xe_database_session_targets. event_session_address|dm_xe_database_sessions 位址|多對一|  
  
  
