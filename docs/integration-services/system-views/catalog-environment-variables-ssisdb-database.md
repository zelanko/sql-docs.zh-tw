---
title: "catalog.environment_variables (SSISDB 資料庫) | Microsoft Docs"
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
ms.assetid: 45f5aacd-505a-443b-8fc2-c7929e78cff8
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 936d4f9346b4f8e3e58f88bbadf60127b7dc122f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="catalogenvironmentvariables-ssisdb-database"></a>catalog.environment_variables (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有環境顯示環境變數詳細資料。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|variable_id|**bigint**|環境變數的唯一識別碼 (ID)。|  
|environment_id|**bigint**|與變數相關聯之環境的唯一識別碼。|  
|name|**sysname**|環境變數的名稱。|  
|description|**nvarchar(1024)**|環境變數的描述。|  
|型別|**nvarchar(128)**|環境變數的資料類型。|  
|sensitive|**bit**|當值為 `1` 時，變數為敏感值，會在儲存時加密。 當值為 `0` 時，變數則不是敏感值，且會在儲存為純文字。|  
|value|**sql_variant**|環境變數的值。 當 sensitive 為 `0` 時，會顯示純文字值。 當 sensitive 是 `1` 時，會顯示 **NULL**。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示目錄中每個環境變數的資料列。  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   對應環境的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **sysadmin** 伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
