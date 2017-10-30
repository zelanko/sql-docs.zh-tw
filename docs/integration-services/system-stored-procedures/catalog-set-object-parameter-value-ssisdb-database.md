---
title: "catalog.set_object_parameter_value （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 3a5dc70b1e955b3c702dc9e9dbe4776cc4ebd5ac
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="catalogsetobjectparametervalue-ssisdb-database"></a>catalog.set_object_parameter_value (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的參數值。 建立關聯的環境變數的值，或指派任何其他值會指派預設使用常值。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_object_parameter_value [@object_type =] object_type   
    , [@folder_name =] folder_name   
    , [@project_name =] project_name   
    , [@parameter_name =] parameter _name   
    , [@parameter_value =] parameter_value   
 [  , [@object_name =] object_name ]  
 [  , [@value_type =] value_type ]  
```  
  
## <a name="arguments"></a>引數  
 [@object_type =] *object_type*  
 參數類型。 使用 `20` 值表示專案參數，或使用 `30` 值表示封裝參數。 *Object_type*是**smallInt**。  
  
 [@folder_name =] *folder_name*  
 包含參數之資料夾的名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [@project_name =] *project_name*  
 包含參數之專案的名稱。 *Project_name*是**nvarchar （128)**。  
  
 [@parameter_name =] *parameter_name*  
 參數的名稱。 *Parameter_name*是**nvarchar （128)**。  
  
 [@parameter_value =] *parameter_value*  
 參數的值。 *Parameter_value*是**sql_variant**。  
  
 [@object_name =] *object_name*  
 封裝名稱。 參數為封裝參數時，就需要這個引數。 *Object_name*是**nvarchar （260)**。  
  
 [@value_type =] *value_type*  
 參數值的類型。 使用字元`V`表示*parameter_value*是在執行前會不指派任何其他值時，依預設會使用常值。 使用字元`R`表示*parameter_value*這個參考值，而且已設定為環境變數的名稱。 這是選擇性引數，根據預設，會使用字元 `V`。 *Value_type*是**char （1)**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 和 MODIFY 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會造成預存程序引發錯誤的某些條件：  
  
-   參數類型無效  
  
-   專案名稱無效  
  
-   封裝名稱對封裝參數來說無效  
  
-   值類型無效  
  
-   使用者未具備適當的權限  
  
## <a name="remarks"></a>備註  
  
-   如果沒有*value_type*指定的常值*parameter_value*預設會使用。 使用常值時， *value_set*中[object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)檢視設`1`。 不允許 NULL 參數值。  
  
-   如果*value_type*包含字元`R`，這表示受參考的值， *parameter_value*參考環境變數的名稱。  
  
-   值`20`可用於*object_type*表示專案參數。 在此案例中的值*object_name*不是有必要，而且指定的任何值*object_name*會被忽略。 當使用者想要設定專案參數時，可以使用這個值。  
  
-   值`30`可用於*object_type*代表封裝參數。 在此案例中的值*object_name*用來表示對應的封裝。 如果*object_name*未指定，則預存程序會傳回錯誤並結束。  
  
  

