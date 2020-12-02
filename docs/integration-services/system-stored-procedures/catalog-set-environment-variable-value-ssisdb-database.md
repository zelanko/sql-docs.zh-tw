---
description: catalog.set_environment_variable_value (SSISDB 資料庫)
title: catalog.set_environment_variable_value (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 1d493dad-9d9c-4f0a-87e2-20a2d4a35f99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 35d7408a5ad925673f68ce9c66c90768f7fe2f06
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129677"
---
# <a name="catalogset_environment_variable_value-ssisdb-database"></a>catalog.set_environment_variable_value (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中環境變數的值。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_environment_variable_value [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable _name  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name = ] *folder_name*  
 包含環境之資料夾的名稱。 *folder_name* 是 **nvarchar(128)** 。  
  
 [ @environment_name = ] *environment_name*  
 環境的名稱。 *environment_name* 是 **nvarchar(128)** 。  
  
 [ @variable _name = ] *variable _name*  
 環境變數的名稱。 *variable _name* 是 **nvarchar(128)**。  
  
 [ @value = ] *value*  
 環境變數的值。 *value* 是 **sql_variant**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   環境的 READ 和 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員** 伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   資料夾名稱無效  
  
-   環境名稱無效  
  
-   環境變數名稱無效  
  
-   使用者未具備適當的權限  
  
  
