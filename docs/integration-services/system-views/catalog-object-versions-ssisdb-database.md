---
title: catalog.object_versions (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 59f757c4c3ae851131059bbac059decc643ec385
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912489"
---
# <a name="catalogobject_versions-ssisdb-database"></a>catalog.object_versions (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的物件版本。 在這個版本中，這個檢視僅支援部分專案版本。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|物件版本的唯一識別碼 (ID)。 無法保證這個數字是連續的。|  
|object_id|**bigint**|物件的唯一識別碼。|  
|object_type|**smallint**|物件的類型。 將會針對專案顯示 `20` 的值。|  
|object_name|**sysname(nvarchar(128))**|物件的名稱。|  
|description|**nvarchar(1024)**|專案的描述。|  
|created_by|**nvarchar(128)**|將物件加入至目錄的使用者名稱。|  
|created_time|**datetimeoffset**|物件加入目錄的日期和時間。|  
|restored_by|**nvarchar(128)**|還原物件的使用者名稱。|  
|last_restored_time|**datetimeoffset**|上次還原物件的日期和時間。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示目錄中每個物件版本的資料列。  
  
## <a name="permissions"></a>權限  
 若要查看這個檢視中的資料列，您必須具有下列任何一個權限：  
  
-   物件的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **sysadmin** 伺服器角色中的成員資格。  
  
> [!NOTE]  
>  強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
