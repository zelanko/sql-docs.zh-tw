---
title: "catalog.validate_package （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- validate_package stored procedure [Integration Services]
- catalog.validate_package stored procedure [Integration Services]
ms.assetid: 0dc03df1-b793-408f-af4c-c11188729abf
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 869b758e3ac922762c293eb8aa9a9537a4397bd6
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="catalogvalidatepackage-ssisdb-database"></a>catalog.validate_package (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  以非同步方式驗證 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的封裝。  
  
## <a name="syntax"></a>語法  
  
```sql
catalog.validate_package [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @package_name = ] package_name  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name =] *folder_name*  
 包含封裝之資料夾的名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =] *project_name*  
 包含封裝之專案的名稱。 *Project_name*是**nvarchar （128)**。  
  
 [ @package_name =] *package_name*  
 封裝名稱。 *Package_name*是**nvarchar （260)**。  
  
 [ @validation_id =] *validation_id*  
 傳回驗證的唯一識別碼 (ID)。 *Validation_id*是**bigint**。  
  
 [ @use32bitruntime =] *use32bitruntime*  
 指出是否要使用 32 位元執行階段，在 64 位元作業系統上執行封裝。 使用的值`1`在 64 位元作業系統上執行時執行 32 位元執行階段。 使用 `0` 值，即可在執行 64 位元作業系統時執行 64 位元執行階段。 這個參數是選擇性的。 *Use32bitruntime*是**元**。  
  
 [ @environment_scope =] *environment_scope*  
 指出由驗證考量的環境參考。 當值為 `A` 時，驗證中會包含與專案相關的所有環境參考。 當值為 `S` 時，只會包含單一環境參考。 當值為 `D` 時，不會包含任何環境參考，而且每個參數必須為常值預設值，才能通過驗證。 這個參數是選擇性的。 字元`D`預設會使用。 *Environment_scope*是**char （1)**。  
  
 [ @reference_id =] *e _ i d*  
 環境參考的唯一識別碼。 只有在單一環境參考包含在驗證時，就需要這個參數時*environment_scope*是`S`。 *E _ i d*是**bigint**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 權限，以及 (如果適用的話) 參考環境的 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   專案名稱或封裝名稱無效  
  
-   使用者未具備適當的權限  
  
-   驗證中包含的一個或多個參考環境不包含參考變數  
  
-   封裝驗證失敗  
  
-   受參考的環境不存在。  
  
-   驗證中包含的參考環境內找不到參考變數  
  
-   封裝參數中已參考變數，但驗證中沒有包含參考環境  
  
## <a name="remarks"></a>備註  
 驗證有助於識別問題，可能會導致無法成功執行封裝。 使用[catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md)或[catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md)来監視驗證狀態檢視。  
  
  
