---
title: catalog.set_object_parameter_value (SSISDB 資料庫)| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 36d73a0248be0bd8f9a0873e5ae8445ee68af2e4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295284"
---
# <a name="catalogset_object_parameter_value-ssisdb-database"></a>catalog.set_object_parameter_value (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的參數值。 將值與環境變數建立關聯，或指派常值，在沒有指派其他值時預設會使用此常值。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_object_parameter_value [@object_type =] object_type   
    , [@folder_name =] folder_name   
    , [@project_name =] project_name   
    , [@parameter_name =] parameter_name   
    , [@parameter_value =] parameter_value   
 [  , [@object_name =] object_name ]  
 [  , [@value_type =] value_type ]  
```  
  
## <a name="arguments"></a>引數  
 [@object_type =] *object_type*  
 參數類型。 使用 `20` 值表示專案參數，或使用 `30` 值表示封裝參數。 *object_type* 是 **smallInt**。  
  
 [@folder_name =] *folder_name*  
 包含參數之資料夾的名稱。 *folder_name* 是 **nvarchar(128)** 。  
  
 [@project_name =] *project_name*  
 包含參數之專案的名稱。 *project_name* 是 **nvarchar(128)** 。  
  
 [@parameter_name =] *parameter_name*  
 參數名稱。 *parameter_name* 是 **nvarchar(128)** 。  
  
 [@parameter_value =] *parameter_value*  
 參數的值。 *parameter_value* 是 **sql_variant**。  
  
 [@object_name =] *object_name*  
 封裝名稱。 參數為封裝參數時，就需要這個引數。 *object_name* 是 **nvarchar(260)** 。  
  
 [@value_type =] *value_type*  
 參數值的類型。 使用字元 `V` 表示如果執行前沒有指派任何值，就會預設使用常值 *parameter_value*。 使用字元 `R` 表示 *parameter_value* 這個參考值已設定為環境變數的名稱。 這是選擇性引數，根據預設，會使用字元 `V`。 *value_type* 是 **char(1)** 。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 和 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會造成預存程序引發錯誤的某些條件：  
  
-   參數類型無效  
  
-   專案名稱無效  
  
-   封裝名稱對封裝參數來說無效  
  
-   值類型無效  
  
-   使用者未具備適當的權限  
  
## <a name="remarks"></a>備註  
  
-   如果沒有指定 *value_type*，預設會使用 *parameter_value* 的常值。 使用常值時，[object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) 檢視中的 *value_set* 會設定為 `1`。 不允許 NULL 參數值。  
  
-   如果 *value_type* 包含字元 `R` (表示受參考的值)，*parameter_value* 就會參考環境變數的名稱。  
  
-   *object_type* 可以使用 `20` 值表示專案參數。 在這個情況下，就不需要 *object_name* 的值，而且為 *object_name* 指定的任何值都會遭到忽略。 當使用者想要設定專案參數時，可以使用這個值。  
  
-   *object_type* 可以使用 `30` 值表示套件參數。 在這個情況下，*object_name* 的值會用來表示對應的套件。 如果未指定 *object_name*，則預存程序會傳回錯誤並結束。  
  
  
