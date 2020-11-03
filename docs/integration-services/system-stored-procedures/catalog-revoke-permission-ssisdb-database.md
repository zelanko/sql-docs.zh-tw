---
description: catalog.revoke_permission (SSISDB 資料庫)
title: catalog.revoke_permission (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- revoke_permission stored procedure [Integration Services]
- catalog.revoke_permission stored procedure [Integration Services]
ms.assetid: 850b9c26-5c7c-47b9-a61c-5cf9bb5948cf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5386c10a85d548a59e68b33009d5ed46e95d85d0
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243638"
---
# <a name="catalogrevoke_permission-ssisdb-database"></a>catalog.revoke_permission (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  撤銷 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的安全性實體物件權限。  
  
## <a name="syntax"></a>語法  
  
```sql
catalog.revoke_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>引數  
 [ @object_type = ] *object_type*  
 安全性實體物件的類型。 安全性實體物件類型包含資料夾 (`1`)、專案 (`2`)、環境 (`3`) 和作業 (`4`)。 *object_type* 是 **smallint** _。_  
  
 [ @object_id = ] *object_id*  
 安全性實體物件的唯一識別碼 (ID)。 *object_id* 是 **bigint** 。  
  
 [ @principal_id = ] *principal_id*  
 要撤銷其權限之主體的識別碼。 *principal_id* 是 **int** 。  
  
 [ @permission_type = ] *permission_type*  
 權限的類型。 *permission_type* 是 **smallint** 。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功)  
  
 1 (object_class 無效)  
  
 2 (object_id 不存在)  
  
 3 (主體不存在)  
  
 4 (權限無效)  
  
 5 (其他錯誤)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 ASSIGN_PERMISSIONS 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員** 伺服器角色的成員資格  
  
## <a name="remarks"></a>備註  
 如果指定 permission_type，則預存程序會移除已明確指派給物件主體的權限。 即使沒有這種類型的執行個體，程序還是會傳回成功的程式碼值 (`0`)。 如果省略 permission_type，則預存程序會移除物件主體的所有權限。  
  
> [!NOTE]  
>  如果主體是具有指定權限之角色的成員，則主體依然會具有物件的指定權限。  
  
 這個預存程序可讓您撤銷下表所述的權限類型：  
  
|permission_type 值|權限名稱|權限描述|適用的物件類型|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|允許主體讀取會被視為物件一部分 (例如屬性) 的資訊。 它不允許主體列舉或讀取物件內所包含之其他主體的內容。|資料夾、專案、環境、作業|  
|`2`|MODIFY|允許主體修改會被視為物件一部分 (例如屬性) 的資訊。 它不允許主體修改物件內所包含之其他主體的內容。|資料夾、專案、環境、作業|  
|`3`|執行 CREATE 陳述式之前，請先執行|允許主體執行專案中所有的封裝。|Project|  
|`4`|MANAGE_PERMISSIONS|允許主體將權限指派至物件。|資料夾、專案、環境、作業|  
|`100`|CREATE_OBJECTS|允許主體在資料夾中建立物件。|資料夾|  
|`101`|READ_OBJECTS|允許主體讀取資料夾中的所有物件。|資料夾|  
|`102`|MODIFY_OBJECTS|允許主體修改資料夾中的所有物件。|資料夾|  
|`103`|EXECUTE_OBJECTS|允許主體執行來自資料夾中所有專案的所有封裝。|資料夾|  
|`104`|MANAGE_OBJECT_PERMISSIONS|允許主體管理資料夾中所有物件的權限。|資料夾|  
  
  
