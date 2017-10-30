---
title: "catalog.object_versions （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3ea7c5ae054a002b9bb4f150e60f323ae03d702a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogobjectversions-ssisdb-database"></a>catalog.object_versions (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的物件版本。 在這個版本中，這個檢視僅支援部分專案版本。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|物件版本的唯一識別碼 (ID)。 無法保證這個數字是連續的。|  
|object_id|**bigint**|物件的唯一識別碼。|  
|object_type|**smallint**|物件的類型。 將會針對專案顯示 `20` 的值。|  
|object_name|**sysname(nvarchar(128))**|物件的名稱。|  
|description|**nvarchar （1024)**|專案的描述。|  
|created_by|**nvarchar （128)**|將物件加入至目錄的使用者名稱。|  
|created_time|**datetimeoffset**|物件加入目錄的日期和時間。|  
|restored_by|**nvarchar （128)**|還原物件的使用者名稱。|  
|last_restored_time|**datetimeoffset**|上次還原物件的日期和時間。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示目錄中每個物件版本的資料列。  
  
## <a name="permissions"></a>Permissions  
 若要查看這個檢視中的資料列，您必須具有下列任何一個權限：  
  
-   物件的 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   中的成員資格**sysadmin**伺服器角色。  
  
> [!NOTE]  
>  強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  

