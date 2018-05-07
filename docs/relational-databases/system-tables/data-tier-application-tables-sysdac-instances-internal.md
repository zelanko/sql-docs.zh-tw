---
title: sysdac_instances_internal (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdac_instances_internal_TSQL
- sysdac_instances_internal
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_instances_internal
ms.assetid: d2d52cc4-3463-431a-b779-6fbfdeee1dfc
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1fb935b6f35c5fe31b9a477782a59e8fff841f90
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="data-tier-application-tables---sysdacinstancesinternal"></a>資料層應用程式資料表 sysdac_instances_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對部署至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的每個資料層應用程式 (DAC) 執行階段，各顯示一個資料列。 此資料表會儲存在 msdb 資料庫中的 dbo 結構描述。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|DAC 執行個體的識別碼。|  
|instance_name|**sysname**|部署執行個體時指定之 DAC 執行個體的名稱。|  
|type_name|**sysname**|建立 DAC 封裝時指定之 DAC 的名稱。|  
|type_version|**nvarchar(64)**|建立 DAC 封裝時指定之 DAC 的版本。|  
|description|**nvarchar(4000)**|建立 DAC 封裝時寫入之 DAC 的描述。|  
|type_stream|**varbinary(max)**|包含 DAC 中之邏輯物件編碼表示法的位元資料流，例如，資料表和檢視表。|  
|date_created|**datetime**|建立 DAC 執行個體的日期和時間。|  
|created_by|**sysname**|建立 DAC 執行個體的登入。|  
  
## <a name="remarks"></a>備註  
 此檢視的唯讀存取可供所有使用者有權連接到 master 資料庫。  
  
## <a name="permissions"></a>Permissions  
 需要系統管理員 (sysadmin) 固定伺服器角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)  
  
  
