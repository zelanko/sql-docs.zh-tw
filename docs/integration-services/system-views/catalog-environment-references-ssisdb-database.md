---
title: "catalog.environment_references (SSISDB 資料庫) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: efec53ef-3e5a-4b76-b71d-a0cf9e11ac00
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 33641abcbfab429763b319e34ca52ffd6780c25a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="catalogenvironmentreferences-ssisdb-database"></a>catalog.environment_references (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 **SSISDB** 目錄中的所有專案顯示環境參考。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|reference_id|**bigint**|參考的唯一識別碼 (ID)。|  
|project_id|**bigint**|專案的唯一識別碼。|  
|reference_type|**char(1)**|指出環境會位於與專案相同的資料夾 (相對參考) 中，或是在不同的資料夾 (絕對參考) 中。 當值為 `R` 時，會使用相對參考找出環境的所在位置。 當值為 `A` 時，會使用絕對參考找出環境的所在位置。|  
|environment_folder_name|**sysname**|資料夾的名稱 (如果使用絕對參考找出環境的所在位置)。|  
|environment_name|**sysname**|專案參考之環境的名稱。|  
|validation_status|**char(1)**|驗證的狀態。|  
|last_validation_time|**datatimeoffset(7)**|上一次驗證的時間。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示目錄中每個環境參考的資料列。  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   對應專案的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **sysadmin** 伺服器角色的成員資格。  
  
> [!NOTE]  
>  如果您有專案的 READ 權限，您也會具有與該專案相關聯之所有封裝與環境參考的 READ 權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
## <a name="remarks"></a>備註  
 專案可以具有相對或絕對的環境參考。 相對參考會依名稱參考環境，並且需要位於與專案相同的資料夾中。 絕對參考會依名稱和資料夾參考環境，且可以參考位於與專案不同資料夾中的環境。 專案可以參考多個環境。  
  
  
