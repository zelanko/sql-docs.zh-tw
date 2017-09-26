---
title: "catalog.restore_project （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 23074fc664591411666315036e3493e1b7b26134
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrestoreproject-ssisdb-database"></a>catalog.restore_project (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案還原到舊版。  
  
## <a name="syntax"></a>語法  
  
```tsql  
restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name =] *folder_name*  
 包含專案之資料夾的名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project v =] *project_name*  
 專案的名稱。 *Project_name*是**nvarchar （128)**。  
  
 [ @object_version_lsn =] *object_version_lsn*  
 專案的版本。 *Object_version_lsn*是**bigint**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 專案的詳細資料會當做傳回**varbinary （max)**過程之結果集如果*project_name*找到。  
  
 **沒有結果集**傳回如果專案無法還原指定的資料夾。  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 和 MODIFY 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   專案版本不存在或不符合專案名稱  
  
-   專案不存在  
  
-   使用者未具備適當的權限  
  
## <a name="remarks"></a>備註  
 還原專案時，會為所有參數會指定預設值，而且所有環境參考都會維持不變。 要保留在目錄中的專案版本的最大數目取決目錄屬性**MAX_VERSIONS_PER_PROJECT**，如下所示[catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)檢視。  
  
> [!WARNING]  
>  還原專案之後，環境參考可能不再有效。  
  
  
