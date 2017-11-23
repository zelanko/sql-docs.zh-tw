---
title: "dbo.slo_assignment_history (Azure SQL Database) |Microsoft 文件"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 06/10/2016
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.slo_assignment_history
- slo_assignment_history
- slo_assignment_history_TSQL
- dbo.slo_assignment_history_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dbo.slo_assignment_history
- slo_assignment_history
ms.assetid: 048a6fb5-2fc2-4d12-a436-4c53ecd413f3
caps.latest.revision: "9"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61bf1f0541df9085235dc00072624e1e91425cc5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="dbosloassignmenthistory-azure-sql-database"></a>dbo.slo_assignment_history (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **這只適用於[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11。**  
>   
>  這項功能處於預覽狀態。 不要採用此功能的特定實作的相依性，因為在未來的版本中可能會變更或移除此功能。  
  
 傳回伺服器中的資料庫 SLO 指派記錄，包括下列項目：  
  
-   伺服器中的資料庫 SLO 指派記錄。  
  
-   每個資料庫 SLO 變更要求的開始和結束時間。  
  
-   記錄在 error_code 和 error_desc 資料行中的任何 SLO 指派錯誤。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|資料庫的名稱。|  
|database_id|**int**|資料庫的識別碼。|  
|create_date|**datetimeoffset(7)**|資料庫建立日期。|  
|service_objective_name|**sysname**|服務等級目標 (SLO) 的名稱。|  
|service_objective_id|**uniqueidentifier**|SLO 的識別碼。|  
|operation_id|**uniqueidentifier**|作業的識別碼。|  
|operation_start_time|**datetimeoffset(7)**|資料庫 SLO 變更要求的開始時間。|  
|operation_end_time|**datetimeoffset(7)**|資料庫 SLO 變更要求的結束時間。|  
|error_code|**int**|資料庫 SLO 變更要求的錯誤碼。|  
|error_desc|**nvarchar**|資料庫 SLO 變更要求中的錯誤描述。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視可用於所有的使用者角色有權連接到虛擬**主要**資料庫。  
  
## <a name="examples"></a>範例  
 下列範例會針對指定資料庫傳回資料庫 SLO 指派的記錄。  
  
```  
SELECT *  
FROM dbo.slo_assignment_history   
WHERE database_name = '<DB NAME>’   
ORDER BY operation_start_time DESC;  
  
```  
  
## <a name="see-also"></a>請參閱＜  
 [管理高階資料庫](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
