---
description: catalog.set_customized_logging_level_value
title: catalog.set_customized_logging_level_value | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: d83fb763-c7c6-4e20-bd10-0f995598b198
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3f5e101e0413381a2b633e758e0d67a0c4c8167b
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129700"
---
# <a name="catalogset_customized_logging_level_value"></a>catalog.set_customized_logging_level_value 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

  變更現有自訂記錄層級所記錄的統計資料或事件。 如需自訂記錄層次的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_customized_logging_level_value [ @level_name = ] level_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>引數  
 [ @level_name = ] *level_name*  
 現有自訂記錄層次的名稱。  
  
 *level_name* 是 **nvarchar(128)**。  
  
 [ @property_name = ] *property_name*  
 要變更的屬性名稱。 有效值為 **PROFILE** 和 **EVENTS**。  
  
 *property_name* 是 **nvarchar(128)**。  
  
 [ @property_value = ] *property_value*  
 指定自訂記錄層級之指定屬性的新值。  
  
 如需設定檔和事件的有效值清單，請參閱 [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md)。  
  
 *property_value* 是 **bigint**。  
  
## <a name="remarks"></a>備註  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   **ssis_admin** 資料庫角色中的成員資格  
  
-   **sysadmin** 伺服器角色中的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   使用者沒有必要權限。  
  
  
