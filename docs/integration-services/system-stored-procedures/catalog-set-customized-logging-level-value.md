---
title: "catalog.set_customized_logging_level_value |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d83fb763-c7c6-4e20-bd10-0f995598b198
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 75ef405fe4550e81ec2d5178a1d3242d405755af
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetcustomizedlogginglevelvalue"></a>catalog.set_customized_logging_level_value
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  變更統計資料或現有的自訂的記錄層級所記錄的事件。 如需自訂的記錄層級的詳細資訊，請參閱[Integration Services &#40;SSIS &#41;記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="syntax"></a>語法  
  
```sql  
set_customized_logging_level_value [ @level_name = ] level_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
  
```  
  
## <a name="arguments"></a>引數  
 [ @level_name =] *l*  
 名稱的現有自訂記錄層級。  
  
 *l*是**nvarchar （128)**。  
  
 [ @property_name =] *property_name*  
 若要變更屬性的名稱。 有效值為**設定檔**和**事件**。  
  
 *Property_name*是**nvarchar （128)**。  
  
 [ @property_value =] *property_value*  
 指定之屬性的新值的自訂記錄層次。  
  
 如需有效的值，設定檔和事件的清單，請參閱[catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md)。  
  
 *Property_value*是**bigint**。  
  
## <a name="remarks"></a>備註  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   **ssis_admin** 資料庫角色中的成員資格  
  
-   **sysadmin** 伺服器角色中的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   使用者沒有必要的權限。  
  
  
