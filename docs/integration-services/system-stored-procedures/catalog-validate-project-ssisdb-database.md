---
title: "catalog.validate_project （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 5270689a-46d4-4847-b41f-3bed1899e955
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 83439015694f4235af4a67e994e916651ec63cc1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogvalidateproject-ssisdb-database"></a>catalog.validate_project (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  以非同步方式驗證 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案。  
  
## <a name="syntax"></a>語法  
  
```  
  
validate_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @validate_type = ] validate_type  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name =] *folder_name*  
 包含專案之資料夾的名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =] *project_name*  
 專案的名稱。 *Project_name*是**nvarchar （128)**。  
  
 [ @validate_type =] *v*  
 指出執行的類型驗證。 使用字元 `F` 即可執行完整驗證。 *v*是**char （1)**。  
  
 [ @validation_id =] *validation_id*  
 傳回驗證的唯一識別碼 (ID)。 *Validation_id*是**bigint**。  
  
 [ @use32bitruntime =] *use32bitruntime*  
 指出是否要使用 32 位元執行階段，在 64 位元作業系統上執行封裝。 使用的值`1`在 64 位元作業系統上執行時執行 32 位元執行階段。 使用 `0` 值，即可在執行 64 位元作業系統時執行 64 位元執行階段。 這個參數是選擇性的。 *Use32bitruntime*是**元**。  
  
 [ @environment_scope =] *environment_scope*  
 指出由驗證考量的環境參考。 當值為 `A` 時，驗證中會包含與專案相關的所有環境參考。 當值為 `S` 時，只會包含單一環境參考。 當值為 `D` 時，不會包含任何環境參考，而且每個參數必須為常值預設值，才能通過驗證。 這是選擇性參數，根據預設，將會使用字元 `D`。 *Environment_scope*是**char （1)**。  
  
 [ @reference_id =] *e _ i d*  
 環境參考的唯一識別碼。 只有在單一環境參考包含在驗證時，就需要這個參數時*environment_scope*是`S`。 *E _ i d*是**bigint**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 驗證步驟的輸出會當做結果集中的不同區段傳回。  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 權限，以及 (如果適用的話) 參考環境的 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將提供可能會引發錯誤或警告的某些條件：  
  
-   專案中的一個或多個封裝未通過驗證  
  
-   如果驗證中包含的一個或多個參考環境與參考變數不相符，驗證就會失敗  
  
-   指定驗證類型無效  
  
-   專案名稱或環境參考識別碼無效  
  
-   使用者未具備適當的權限  
  
## <a name="remarks"></a>備註  
 驗證有助於識別讓專案中之封裝無法成功執行的問題。 使用[catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md)或[catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md)来監視驗證狀態檢視。  
  
 驗證中只能夠使用使用者可存取的環境。 驗證輸出會當做結果集傳送至用戶端。  
  
 在這個版本中，專案驗證不支援相依性驗證。  
  
 完整驗證會確認所有參考的環境變數皆可在驗證所包含的參考環境中找到。 完整驗證結果會列出無效的環境參考，以及在驗證所包含的任何參考環境中皆無法找到的參考環境變數。  
  
  
