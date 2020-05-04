---
title: catalog.create_environment_reference (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 48069bea-31cb-4a0e-9849-a07edc94088f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7b78f54633150fa507ca9df4a4c866cc4226e66
ms.sourcegitcommit: db1b6153f0bc2d221ba1ce15543ecc83e1045453
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/30/2020
ms.locfileid: "82588214"
---
# <a name="catalogcreate_environment_reference-ssisdb-database"></a>catalog.create_environment_reference (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案建立環境參考。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_environment_reference [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @environment_name = ] environment_name  
     , [ @reference_type = ] reference_type  
  [  , [ @environment_folder_name = ] environment_folder_name ]  
  [  , [ @reference_id = ] reference_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name = ] *folder_name*  
 參考環境之專案的資料夾名稱。 *folder_name* 是 **nvarchar(128)** 。  
  
 [ @project_name = ] *project_name*  
 參考環境的專案名稱。 *project_name* 是 **nvarchar(128)** 。  
  
 [ @environment_name = ] *environment_name*  
 正在參考的環境名稱。 *environment_name* 是 **nvarchar(128)** 。  
  
 [ @reference_type = ] *reference_type*  
 指出環境會位於與專案相同的資料夾 (相對參考) 中，或是在不同的資料夾 (絕對參考) 中。 使用值 `R` 表示相對參考。 使用值 `A` 表示絕對參考。 *reference_type* 是 **char(1)** 。  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 正在參考之環境的所在資料夾名稱。 對於絕對參考來說，這個值是必要值。 *environment_folder_name* 是 **nvarchar(128)** 。  
  
 [ @reference_id = ] *reference_id*  
 傳回新參考的唯一識別碼。 這是選擇性參數。 *reference_id* 是 **bigint**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 和 MODIFY 權限，以及環境的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   資料夾名稱無效  
  
-   專案名稱無效  
  
-   使用者未具備適當的權限  
  
-   已使用 *reference_location* 參數中的 `A` 字元指定了絕對參考，但是並未使用 *environment_folder_name* 參數指定資料夾名稱。  
  
## <a name="remarks"></a>備註  
 專案可以具有相對或絕對的環境參考。 相對參考會依名稱參考環境，並且需要位於與專案相同的資料夾中。 絕對參考會依名稱和資料夾參考環境，且可以參考位於與專案不同資料夾中的環境。 專案可以參考多個環境。  
  
  
