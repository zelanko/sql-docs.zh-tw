---
description: catalog.projects (SSISDB 資料庫)
title: catalog.projects (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 874d4a89af11ab022ce2714334b9aefb506de1a6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421992"
---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對 **SSISDB** 目錄中出現的所有專案顯示詳細資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|project_id|**bigint**|專案的唯一識別碼 (ID)。|  
|folder_id|**bigint**|專案所在資料夾的唯一識別碼。|  
|NAME|**sysname**|專案的名稱。|  
|description|**nvarchar(1024)**|專案的選擇性描述。|  
|project_format_version|**int**|用來開發專案的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。|  
|deployed_by_sid|**varbinary(85)**|安裝專案之使用者的安全性識別碼 (SID)。|  
|deployed_by_name|**nvarchar(128)**|安裝專案的使用者名稱。|  
|last_deployed_time|**datetimeoffset(7)**|部署或重新部署專案的日期和時間。|  
|created_time|**datetimeoffset(7)**|建立專案的日期和時間。|  
|object_version_lsn|**bigint**|專案的版本。 無法保證這個數字是連續的。|  
|validation_status|**char(1)**|驗證狀態。|  
|last_validation_time|**datetimeoffset(7)**|上一次驗證的時間。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示目錄中每個專案的資料列。  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   專案的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **sysadmin** 伺服器角色的成員資格。  
  
> [!NOTE]  
>  如果您有專案的 READ 權限，您也會具有與該專案相關聯之所有封裝與環境參考的 READ 權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
