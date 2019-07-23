---
title: catalog.object_parameters (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 907678a77620f432411b1714ec7a1603e147129e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104821"
---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中出現的所有封裝和專案顯示參數。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|參數的唯一識別碼 (ID)。|  
|project_id|**bigint**|專案的唯一識別碼。|  
|object_type|**smallint**|參數類型。 專案參數的值會是 `20`，而封裝參數的值則會是 `30`。|  
|object_name|**sysname**|對應專案或封裝的名稱。|  
|parameter_name|**sysname(nvarchar(128))**|參數的名稱。|  
|data_type|**nvarchar(128)**|參數的資料類型。|  
|required|**bit**|當值為 `1` 時，必須有參數值才能開始執行。 當值為 `0` 時，不需要參數值即可開始執行。|  
|sensitive|**bit**|當值為 `1` 時，參數值為敏感值。 當值為 `0` 時，參數值則不是敏感值。|  
|description|**nvarchar(1024)**|封裝的選擇性描述。|  
|design_default_value|**sql_variant**|參數的預設值已在專案或封裝的設計期間指派。|  
|default_value|**sql_variant**|目前伺服器正在使用的預設值。|  
|value_type|**char(1)**|指出參數值的參數類型。 當 parameter_value 為常值時，這個欄位會顯示 `V`，而當此值是透過參考環境變數指派時，會顯示 `R`。|  
|value_set|**bit**|當值為 `1` 時，表示參數值已指派。 當值為 `0` 時，表示參數值未指派。|  
|referenced_variable_name|**nvarchar(128)**|指派給參數值之環境變數的名稱。 預設值是 **NULL**。|  
|validation_status|**char(1)**|僅供參考之用。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不使用。|  
|last_validation_time|**datetimeoffset(7)**|僅供參考之用。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不使用。|  
  
## <a name="permissions"></a>權限  
 若要查看這個檢視中的資料列，您必須具有下列任何一個權限：  
  
-   專案的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **sysadmin** 伺服器角色中的成員資格。  
  
 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
