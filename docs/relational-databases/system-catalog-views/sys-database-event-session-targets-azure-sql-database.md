---
description: sys.database_event_session_targets (Azure SQL Database)
title: sys. database_event_session_targets (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 38d775ee-1fe1-4820-88c6-02b2f875a66b
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68b6b8bab06f78e3e04991b5f89cc34b6f497fc6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460667"
---
# <a name="sysdatabase_event_session_targets-azure-sql-database"></a>sys.database_event_session_targets (Azure SQL Database)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  傳回事件工作階段中每一個事件目標的資料列。  
  
||  
|-|  
|**適用于**： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何較新版本。|  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件工作階段的識別碼。 不可為 Null。|  
|target_id|**int**|目標的識別碼。 這個識別碼在事件工作階段物件中是唯一的。 不可為 Null。|  
|NAME|**sysname**|事件目標的名稱。 不可為 Null。|  
|套件|**sysname**|包含此事件目標之事件封裝的名稱。 不可為 Null。|  
|name|**sysname**|包含此事件目標之模組的名稱。 不可為 Null。|  
  
## <a name="permissions"></a>權限  
 需要伺服器的 VIEW DATABASE STATE 權限。  
  
## <a name="remarks"></a>備註  
 此檢視有下列關聯性基數。  
  
|寄件者|收件者|關聯性|  
|-|-|-|  
|sys. database_event_session_targets. event_session_id|sys. database_event_sessions. event_session_id|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
