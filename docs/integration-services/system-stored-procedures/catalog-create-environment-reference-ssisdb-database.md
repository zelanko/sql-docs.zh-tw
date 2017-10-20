---
title: "catalog.create_environment_reference （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 48069bea-31cb-4a0e-9849-a07edc94088f
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 496136e8a0073ba93f003d8dfa539afb48d2c5dc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreateenvironmentreference-ssisdb-database"></a>catalog.create_environment_reference (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案建立環境參考。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_environment_reference [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @environment_name = ] environment_name  
     , [ @reference_location = ] reference_location  
  [  , [ @environment_folder_name = ] environment_folder_name ]  
  [  , [ @reference_id = ] reference_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name =] *folder_name*  
 參考環境之專案的資料夾名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =] *project_name*  
 參考環境的專案名稱。 *Project_name*是**nvarchar （128)**。  
  
 [ @environment_name =] *environment_name*  
 正在參考的環境名稱。 *Environment_name*是**nvarchar （128)**。  
  
 [ @reference_location =] *reference_location*  
 指出環境會位於與專案相同的資料夾 (相對參考) 中，或是在不同的資料夾 (絕對參考) 中。 使用值 `R` 表示相對參考。 使用值 `A` 表示絕對參考。 *Reference_location*是**char （1)**。  
  
 [ @environment_folder_name =] *n*  
 正在參考之環境的所在資料夾名稱。 對於絕對參考來說，這個值是必要值。 *n*是**nvarchar （128)**。  
  
 [ @reference_id =] *e _ i d*  
 傳回新參考的唯一識別碼。 這個參數是選擇性的。 *E _ i d*是**bigint**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 和 MODIFY 權限，以及環境的 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   資料夾名稱無效  
  
-   專案名稱無效  
  
-   使用者未具備適當的權限  
  
-   使用指定了絕對參考`A`字元在*reference_location*參數，但資料夾名稱未指定與*n*參數。  
  
## <a name="remarks"></a>備註  
 專案可以具有相對或絕對的環境參考。 相對參考會依名稱參考環境，並且需要位於與專案相同的資料夾中。 絕對參考會依名稱和資料夾參考環境，且可以參考位於與專案不同資料夾中的環境。 專案可以參考多個環境。  
  
  
