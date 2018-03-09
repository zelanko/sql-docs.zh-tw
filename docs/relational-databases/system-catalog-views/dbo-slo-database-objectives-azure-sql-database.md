---
title: "dbo.slo_database_objectives (Azure SQL Database) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.slo_database_objectives
- dbo.slo_database_objectives_TSQL
- slo_database_objectives_TSQL
- slo_database_objectives
dev_langs:
- TSQL
helpviewer_keywords:
- slo_database_objectives
- dbo.slo_database_objectives
ms.assetid: a522569d-8cfc-4643-a170-1cd291e61eee
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10227990cb6c5928fcc403ee35a978cbf93ad6ca
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2018
---
# <a name="dboslodatabaseobjectives-azure-sql-database"></a>dbo.slo_database_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **這只適用於[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11。**  
>   
>  針對 [！包含[ssSDSfull](../system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) （在 master) ALTER DATABASE 作業。   
  
 傳回 SQL Database 中服務等級目標 (SLO) 的指派狀態。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|資料庫的名稱。|  
|current_slo|**sysname**|資料庫目前的 SLO。|  
|target_slo|**sysname**|資料庫的目標 SLO，如同 SLO 變更要求中所指定。|  
|state_desc|**nvarchar**|SLO 變更要求的狀態：已完成或暫止。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視可用於所有的使用者角色有權連接到虛擬**主要**資料庫。  
  
## <a name="examples"></a>範例  
  
```  
SELECT   
database_name=database_name.name   
    , current_slo=current_slo.name   
    , target_slo=target_slo.name   
    , state_desc=database_slo.state_desc   
FROM slo_database_objectives AS database_slo  
INNER JOIN slo_service_objectives AS current_slo ON database_slo.current_objective_id = current_slo.objective_id  
INNER JOIN slo_service_objectives AS target_slo ON database_slo.configured_objective_id = target_slo.objective_id  
INNER JOIN sys.databases AS database_name  ON database_slo.database_id = database_name.database_id;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [管理高階資料庫](http://go.microsoft.com/fwlink/?LinkID=311927)  
[sys.dm_operation_status (Azure SQL Database)](../system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 
