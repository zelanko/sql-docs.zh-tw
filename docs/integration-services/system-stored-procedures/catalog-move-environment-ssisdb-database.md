---
description: catalog.move_environment (SSISDB 資料庫)
title: catalog.move_environment (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b3fb5242-3c4c-4a87-b3e5-beb22fbab053
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2c8fd91f3b37aa410ca3aa86d2825c27a78e1217
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430090"
---
# <a name="catalogmove_environment-ssisdb-database"></a>catalog.move_environment (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將環境從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的某個資料夾移動到另一個資料夾。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.move_environment [ @source_folder = ] source_folder  
    , [ @environment_name = ] environment_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>引數  
 [ @source_folder = ] *source_folder*  
 在移動之前，環境所在之來源資料夾的名稱。 *source_folder* 是 **nvarchar(128)** 。  
  
 [ @environment_name = ] *environment_name*  
 要移動之環境的名稱。 *environment_name* 是 **nvarchar(128)** 。  
  
 [ @destination_folder = ] *destination_folder*  
 在移動之後，環境所在之目的地資料夾的名稱。 *destination_folder* 是 **nvarchar(128)** 。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   環境的 READ 和 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   環境不存在於來源資料夾中  
  
-   目的地資料夾已有名稱相同的環境  
  
-   使用者未具備適當的權限  
  
## <a name="remarks"></a>備註  
 來自專案的環境參考不會在移動期間隨著環境移動。 環境參考必須隨之更新。 即使環境參考因為環境移動而中斷，這個預存程序仍然會成功。 環境參考必須在預存程序完成之後更新。  
  
> [!NOTE]  
>  專案可以具有相對或絕對的環境參考。 相對參考會依名稱參考環境，而這些參考會要求環境位於與專案相同的資料夾中。 絕對參考會依名稱和資料夾參考環境，而這些參考會參考位於與專案資料夾不同之資料夾中的環境。  
  
  
