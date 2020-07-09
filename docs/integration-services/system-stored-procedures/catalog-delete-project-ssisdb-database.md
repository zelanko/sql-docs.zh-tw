---
title: catalog.delete_project (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f3431445-8dd2-443b-813e-b99db893977e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 36485d7731d1d575eb3cff75ca19c60b13969452
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749592"
---
# <a name="catalogdelete_project-ssisdb-database"></a>catalog.delete_project (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的資料夾刪除現有專案。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.delete_project [ @folder_name = ] folder_name , [ @project_name = ] project_name  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name = ] *folder_name*  
 包含專案之資料夾的名稱。 *folder_name* 是 **nvarchar(128)** 。  
  
 [ @project_name = ] *project_name*  
 要刪除之專案的名稱。 *project_name* 是 **nvarchar(128)** 。  
  
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
 下列清單將描述可能會造成 delete_project 預存程序引發錯誤的某些條件：  
  
-   專案不存在  
  
-   資料夾不存在  
  
-   使用者未具備適當的權限  
  
## <a name="remarks"></a>備註  
 與專案對應的所有物件和環境參考都會隨著專案刪除。 但是，專案版本和相關的作業記錄會予以保留，直到執行下一次的作業清除工作。  
  
  
