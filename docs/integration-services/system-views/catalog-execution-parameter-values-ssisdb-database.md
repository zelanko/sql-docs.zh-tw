---
title: catalog.execution_parameter_values (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: ec93e67b-04ce-4aae-ab96-3ad20e9793ad
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a018123080076cfcc3886395345e29df62feed79
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65714738"
---
# <a name="catalogexecutionparametervalues-ssisdb-database"></a>catalog.execution_parameter_values (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示執行執行個體期間由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝所使用的實際參數值。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|execution_parameter_id|**bigint**|執行參數的唯一識別碼 (ID)。|  
|execution_id|**bigint**|執行執行個體的唯一識別碼 (ID)。|  
|object_type|**smallint**|當值為 `20` 時，參數為專案參數。 當值為 `30` 時，參數為封裝參數。 當值為 `50` 時，參數為下列其中一項：<br /><br /> **LOGGING_LEVEL**<br /><br /> **DUMP_ON_ERROR**<br /><br /> **DUMP_ON_EVENT**<br /><br /> **DUMP_EVENT_CODE**<br /><br /> **CALLER_INFO**<br /><br /> **SYNCHRONIZED**|  
|parameter_data_type|**nvarchar(128)**|參數的資料類型。|  
|parameter_name|**sysname**|參數的名稱。|  
|parameter_value|**sql_variant**|參數的值。 當 sensitive 為 `0` 時，會顯示純文字值。 當 sensitive 為 `1` 時，會顯示 **NULL**。|  
|sensitive|**bit**|當值為 `1` 時，參數值為敏感值。 當值為 `0` 時，參數值則不是敏感值。|  
|required|**bit**|當值為 `1` 時，必須有參數值才能開始執行。 當值為 `0` 時，不需要參數值即可開始執行。|  
|value_set|**bit**|當值為 `1` 時，表示參數值已指派。 當值為 `0` 時，表示參數值未指派。|  
|runtime_override|**bit**|當值為 `1` 時，表示在開始執行之前，參數值已從原始值變更。 當值為 `0` 時，表示參數值為設定的原始參數值。|  
  
## <a name="remarks"></a>Remarks  
 這個檢視會顯示目錄中每個執行參數的資料列。 執行參數值是在單一執行執行個體期間指派給專案參數或封裝參數的值。  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   執行的執行個體之 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
