---
title: "catalog.deploy_packages |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1839430dd7fb83ab16c4de46011819e3ce28e835
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeploypackages"></a>catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  將一或多個套件部署中的資料夾[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]目錄或更新先前已部署的現有套件。  
  
## <a name="syntax"></a>語法  
  
```  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name =] *folder_name*  
 資料夾的名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =] *project_name*  
 資料夾中的專案名稱。 *Project_name*是**nvarchar （128)**。  
  
 [ @packages_table =] *packages_table*  
 二進位內容之[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]封裝 (.dtsx) 檔案。 *Packages_table*是**[catalog]。 [Package_Table_Type]**  
  
 [ @operation_id =] *operation_id*  
 傳回部署作業的唯一識別碼。 *Operation_id*是**bigint**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   專案或修改封裝的權限來更新封裝的 CREATE_OBJECTS 權限。  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會造成預存程序引發錯誤的某些條件：  
  
-   參數參考到不存在的物件、 參數會嘗試建立的物件已經存在，或以其他方法的參數無效。  
  
-   使用者未具備足夠的權限  
  
  
