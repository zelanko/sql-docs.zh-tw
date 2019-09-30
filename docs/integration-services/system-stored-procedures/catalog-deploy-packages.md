---
title: catalog.deploy_packages | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0a1828925494ca2e1e8f593e3f133a21cd10a9ee
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296778"
---
# <a name="catalogdeploy_packages"></a>catalog.deploy_packages 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  將一或多個套件部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的資料夾，或更新先前已部署的現有套件。  
  
## <a name="syntax"></a>語法  
  
```sql  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name = ] *folder_name*  
 資料夾的名稱。 *folder_name* 是 **nvarchar(128)** 。  
  
 [ @project_name = ] *project_name*  
 資料夾中的專案名稱。 *project_name* 是 **nvarchar(128)** 。  
  
 [ @packages_table = ] *packages_table*  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件 (.dtsx) 檔案的二進位內容。 *packages_table* 是 **[catalog].[Package_Table_Type]**  
  
 [ @operation_id = ] *operation_id*  
 傳回部署作業的唯一識別碼。 *operation_id* 是 **bigint**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   要更新套件之專案的 CREATE_OBJECTS 權限或套件的 MODIFY 權限。  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會造成預存程序引發錯誤的某些條件：  
  
-   參數參考到不存在的物件、參數會嘗試建立物件已經存在的物件，或參數因為其他原因而無效。  
  
-   使用者未具備足夠的權限  
  
  
