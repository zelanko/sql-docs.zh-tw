---
title: "catalog.create_folder （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 43d128f9dcc4cea632c810a13d21eb5e1ddb61df
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreatefolder-ssisdb-database"></a>catalog.create_folder (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中建立資料夾。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_folder [@folder_name =] folder_name, [@folder_id =] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>引數  
 [@folder_name =] *folder_name*  
 新資料夾的名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [@folder_name =] *folder_id*  
 資料夾的唯一識別碼 (ID)。 *Folder_id*是**bigint**。  
  
## <a name="return-code-value"></a>傳回碼值  
 傳回資料夾識別項。  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
如果具有相同名稱的資料夾已經存在，預存程序會傳回錯誤。  
  
  

