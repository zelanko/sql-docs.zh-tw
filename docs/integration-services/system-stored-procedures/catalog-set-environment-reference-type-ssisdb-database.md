---
title: catalog.set_environment_reference_type (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b79e3a06-22c0-40e5-8933-1b3414db3329
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d50cef16424f5524429c6b4285af0ae8568391be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038703"
---
# <a name="catalogsetenvironmentreferencetype-ssisdb-database"></a>catalog.set_environment_reference_type (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案，設定與現有環境參考相關聯之參考類型和環境名稱。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_environment_reference_location [ @reference_id = reference_id  
    , [ @reference_type = ] reference_type  
 [  , [ @environment_folder_name = ] environment_folder_name ]  
```  
  
## <a name="arguments"></a>引數  
 [ @reference_id = ] *reference_id*  
 要更新之環境參考的唯一識別碼。 *reference_id* 是 **bigint**。  
  
 [ @reference_type = ] *reference_type*  
 指出環境會位於與專案相同的資料夾 (相對參考) 中，或是在不同的資料夾 (絕對參考) 中。 使用值 `R` 表示相對參考。 使用值 `A` 表示絕對參考。 *reference_type* 是 **char(1)** 。  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 環境所在的資料夾。 對於絕對參考來說，這個值是必要值。 *environment_folder_name* 是 **nvarchar(128)** 。  
  
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
  
-   資料夾名稱、環境名稱或參考識別碼無效  
  
-   使用者未具備適當的權限  
  
-   已使用 *reference_location* 參數中的 `A` 字元指定了絕對參考，但是並未使用 *environment_folder_name* 參數指定資料夾名稱。  
  
## <a name="remarks"></a>Remarks  
 專案可以具有相對或絕對的環境參考。 相對參考會依名稱參考環境，並且需要位於與專案相同的資料夾中。 絕對參考會依名稱和資料夾參考環境，且可以參考位於與專案不同資料夾中的環境。 專案可以參考多個環境。  
  
> [!IMPORTANT]  
>  如果指定了相對參照，就不會使用 *environment_folder_name* 參數值，且環境資料夾名稱會自動設為 **NULL**。 如果指定了絕對參照，就必須在 *environment_folder_name* 參數中提供環境資料夾名稱。  
  
  
