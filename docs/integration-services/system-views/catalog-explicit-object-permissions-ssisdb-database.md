---
title: catalog.explicit_object_permissions (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 49b09e0f-06e8-451f-b979-a0d91000bfe3
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e5d214e49e823cb0bff1a8473f93ec95987dc9b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="catalogexplicitobjectpermissions-ssisdb-database"></a>catalog.explicit_object_permissions (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  只顯示已明確指派給使用者的權限。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|安全性實體物件的類型。 安全性實體物件類型包括資料夾 (`1`)、專案 (`2`)、環境 (`3`) 和作業 (`4`)。|  
|object_id|**bigint**|安全性實體物件的唯一識別碼 (ID) 或主索引鍵。|  
|principal_id|**int**|資料庫主體的識別碼。|  
|permission_type|**smallint**|權限的類型。|  
|is_deny|**bit**|指出權限是否已授與或遭到拒絕。 當值為 `1` 時，表示權限遭到拒絕。 當值為 `0` 時，表示權限未遭到拒絕。|  
|grantor_id|**int**|授與權限之主體的識別碼。|  
  
## <a name="remarks"></a>Remarks  
 這個檢視會顯示下表列出的權限類型：  
  
|permission_type 值|權限名稱|權限描述|適用的物件類型|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|允許主體讀取會被視為物件一部分 (例如屬性) 的資訊。 它不允許主體列舉或讀取物件內所包含之其他主體的內容。|資料夾、專案、環境、作業|  
|`2`|MODIFY|允許主體修改會被視為物件一部分 (例如屬性) 的資訊。 它不允許主體修改物件內所包含之其他主體的內容。|資料夾、專案、環境、作業|  
|`3`|執行 CREATE 陳述式之前，請先執行|允許主體執行專案中所有的封裝。|專案|  
|`4`|MANAGE_PERMISSIONS|允許主體將權限指派至物件。|資料夾、專案、環境、作業|  
|`100`|CREATE_OBJECTS|允許主體在資料夾中建立物件。|資料夾|  
|`101`|READ_OBJECTS|允許主體讀取資料夾中的所有物件。|資料夾|  
|`102`|MODIFY_OBJECTS|允許主體修改資料夾中的所有物件。|資料夾|  
|`103`|EXECUTE_OBJECTS|允許主體執行來自資料夾中所有專案的所有封裝。|資料夾|  
|`104`|MANAGE_OBJECT_PERMISSIONS|允許主體管理資料夾中所有物件的權限。|資料夾|  
  
## <a name="permissions"></a>Permissions  
 這個檢視並不會為目前主體的權限提供完整的檢視。 使用者也必須檢查主體是否為已指派權限之角色和群組的成員。  
  
  
