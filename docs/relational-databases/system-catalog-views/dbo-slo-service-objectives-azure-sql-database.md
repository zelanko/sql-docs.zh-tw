---
title: "dbo.slo_service_objectives (Azure SQL Database) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: Azure SQL Database
f1_keywords:
- dbo.slo_service_objectives
- dbo.slo_service_objectives_TSQL
- slo_service_objectives
- slo_service_objectives_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dbo.slo_service_objectives
- slo_service_objectives
ms.assetid: d5dd7ed9-440a-4432-ad45-644e4e72318f
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f91dccf478821047e4c3a25ea19d35d1a2774fd
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="dbosloserviceobjectives-azure-sql-database"></a>dbo.slo_service_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  這項功能處於預覽狀態，並在已被取代[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V12。 不要採用此功能的特定實作的相依性，因為在未來的版本中可能會變更或移除此功能。  
  
 傳回有關目前伺服器的服務等級目標 (SLO) 資訊。  
  
||  
|-|  
|**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11。|  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|objective_id|**uniqueidentifier**|服務等級目標的識別碼。|  
|NAME|**sysname**|服務等級目標的名稱。|  
|description|**nvarchar**|服務等級目標的描述。|  
|create_date|**datetimeoffset(7)**|服務等級目標在伺服器上的建立日期。|  
|is_system|**bit**|1 = 系統服務等級目標|  
|is_default|**bit**|1 = 服務等級目標為預設 SLO。|  
|state|**tinyint**|1 = 服務等級目標已啟用。<br /><br /> 2 = 服務等級目標已停用。|  
|state_desc|**nvarchar**|服務等級目標的描述。|  
|metadata_version|**decimal**|服務等級目標的版本。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視可用於所有的使用者角色有權連接到虛擬**主要**資料庫。  
  
## <a name="see-also"></a>請參閱  
 [管理高階資料庫](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
