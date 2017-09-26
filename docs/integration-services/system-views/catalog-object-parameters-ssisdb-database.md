---
title: "catalog.object_parameters （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9d538e5b55ef4e8880afb2d008b11c17d9a03189
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中出現的所有封裝和專案顯示參數。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|參數的唯一識別碼 (ID)。|  
|project_id|**bigint**|專案的唯一識別碼。|  
|object_type|**smallint**|參數類型。 專案參數的值會是 `20`，而封裝參數的值則會是 `30`。|  
|object_name|**sysname**|對應專案或封裝的名稱。|  
|parameter_name|**sysname(nvarchar(128))**|參數的名稱。|  
|data_type|**nvarchar （128)**|參數的資料類型。|  
|required|**bit**|當值為 `1` 時，必須有參數值才能開始執行。 當值為 `0` 時，不需要參數值即可開始執行。|  
|sensitive|**bit**|當值為 `1` 時，參數值為敏感值。 當值為 `0` 時，參數值則不是敏感值。|  
|description|**nvarchar （1024)**|封裝的選擇性描述。|  
|design_default_value|**sql_variant**|參數的預設值已在專案或封裝的設計期間指派。|  
|default_value|**sql_variant**|目前伺服器正在使用的預設值。|  
|value_type|**char （1)**|指出參數值的參數類型。 這個欄位會顯示`V`parameter_value 時常值和`R`當透過參考環境變數指派值。|  
|value_set|**bit**|當值為 `1` 時，表示參數值已指派。 當值為 `0` 時，表示參數值未指派。|  
|referenced_variable_name|**nvarchar （128)**|指派給參數值之環境變數的名稱。 預設值是**NULL**。|  
|validation_status|**char （1)**|僅供參考之用。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不使用。|  
|last_validation_time|**datetimeoffset(7)**|僅供參考之用。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不使用。|  
  
## <a name="permissions"></a>Permissions  
 若要查看這個檢視中的資料列，您必須具有下列任何一個權限：  
  
-   專案的 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   中的成員資格**sysadmin**伺服器角色。  
  
 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
