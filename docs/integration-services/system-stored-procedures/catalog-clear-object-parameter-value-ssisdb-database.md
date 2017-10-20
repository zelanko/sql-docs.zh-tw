---
title: "catalog.clear_object_parameter_value （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: dcbbb714-a051-4805-9e2b-2c2fb647c890
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5d0d89081a31341a8d813d9985940c0e3ce0160a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogclearobjectparametervalue-ssisdb-database"></a>catalog.clear_object_parameter_value (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  清除現有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案或封裝儲存在伺服器上的參數值。  
  
## <a name="syntax"></a>語法  
  
```sql  
clear_object_parameter [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @object_type = ] object_type   
    , [ @object_name = ] object_name   
    , [ @parameter_ name = ] parameter_name  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name =] *folder_name*  
 包含專案之資料夾的名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =] *project_name*  
 專案的名稱。 *Project_name*是**nvarchar （128)**。  
  
 [ @object_type =] *object_type*  
 物件的類型。 有效的值包括 `20` (專案) 和 `30` (封裝)。 *Object_type*是**smallInt**。  
  
 [@ 物件 b =]*物件 b*  
 封裝名稱。 *物件 b*是**nvarchar （260)**。  
  
 [@parameter_名稱 =] *parameter_name*  
 參數的名稱。 *Parameter_ 名稱*是**nvarchar （128)**。  
  
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
 下列清單描述可能會導致 clear_object_parameter 預存程序引發錯誤的某些條件：  
  
-   指定了無效的物件類型，或在專案中找不到物件名稱。  
  
-   專案不存在、無法存取專案或專案名稱無效。  
  
-   指定的參數名稱無效。  
  
-   使用者未具備適當的權限。  
  
  
