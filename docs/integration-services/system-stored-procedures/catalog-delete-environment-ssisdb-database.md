---
description: catalog.delete_environment (SSISDB 資料庫)
title: catalog.delete_environment (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: d44b765f-9523-4e6a-bb17-37846d5e5334
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ea6093e6c4f3359d1178879295448531009ff090
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456888"
---
# <a name="catalogdelete_environment-ssisdb-database"></a>catalog.delete_environment (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的資料夾刪除環境。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.delete_environment [ @folder_name = ] folder_name , [ @environment_name = ] environment_name  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name = ] *folder_name*  
 包含環境之資料夾的名稱。 *folder_name* 是 **nvarchar(128)** 。  
  
 [ @environment_name = ] *environment_name*  
 要刪除之環境的名稱。 *environment_name* 是 **nvarchar(128)** 。  
  
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
  
-   指定的環境不存在。  
  
-   使用者未具備適當的權限  
  
  
