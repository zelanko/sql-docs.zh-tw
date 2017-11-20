---
title: "catalog.set_environment_property （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a345675b-d32e-4624-96cf-ec656730b114
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8eedfe6919a69759cc6de3645b3e1f965dcdd0c6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetenvironmentproperty-ssisdb-database"></a>catalog.set_environment_property (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的環境屬性。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_environment_property [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name =] *folder_name*  
 包含環境之資料夾的名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [ @environment_name =] *environment_name*  
 環境的名稱。 *Environment_name*是**nvarchar （128)**。  
  
 [ @property_name =] *property_name*  
 環境屬性的名稱。 *Property_name*是**nvarchar （128)**。  
  
 [ @property_value =] *property_value*  
 環境屬性的值。 *Property_value*是**nvarchar （1024)**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   環境的 READ 和 MODIFY 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   資料夾名稱無效  
  
-   屬性名稱無效  
  
-   環境名稱無效  
  
## <a name="remarks"></a>備註  
 在這個版本中，只可以設定 `Description` 屬性。 `Description` 屬性的屬性值不能超過 4000 個字元。  
  
  

