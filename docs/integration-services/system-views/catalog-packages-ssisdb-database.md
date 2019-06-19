---
title: catalog.packages (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- packages view [Integration Services]
- catalog.packages view [Integration Services]
ms.assetid: a634e94d-f492-4dfd-9611-a35f545106a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a82624d43f63ff8e774c61198021e29cd080366e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65714514"
---
# <a name="catalogpackages-ssisdb-database"></a>catalog.packages (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 **SSISDB** 目錄中出現的所有套件顯示詳細資料。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|package_id|**bigint**|封裝的唯一識別碼 (ID)。|  
|NAME|**nvarchar(256)**|封裝的唯一名稱。|  
|package_guid|**uniqueidentifier**|用來識別封裝的全域唯一識別碼 (GUID)。|  
|description|**nvarchar(1024)**|封裝的選擇性描述。|  
|package_format_version|**int**|用來開發封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。|  
|version_major|**int**|封裝的主要版本。|  
|version_minor|**int**|封裝的次要版本。|  
|version_build|**int**|封裝的組建版本。|  
|version_comments|**nvarchar(1024)**|封裝版本的選擇性註解。|  
|version_guid|**uniqueidentifier**|唯一識別封裝版本的 GUID。|  
|project_id|**bigint**|專案的唯一識別碼。|  
|entry_point|**bit**|`1` 值表示封裝是直接啟動。 `0` 值表示封裝是由具有執行封裝工作的其他封裝啟動。 預設值是 `1`。|  
|validation_status|**char(1)**|驗證的狀態。|  
|last_validation_time|**datetimeoffset(7)**|上一次驗證的時間。|  
  
## <a name="remarks"></a>Remarks  
 這個檢視會顯示目錄中每個封裝的資料列。  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   對應專案的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **sysadmin** 伺服器角色的成員資格。  
  
> [!NOTE]  
>  如果您有專案的 READ 權限，您也會具有與該專案相關聯之所有封裝與環境參考的 READ 權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
