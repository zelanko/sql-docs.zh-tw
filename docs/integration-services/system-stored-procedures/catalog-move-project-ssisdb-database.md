---
title: catalog.move_project (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: ef3b0325-d8e9-472b-bf11-7d3efa6312ff
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 44bc62ba806eae723a931f01e799980a22989926
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404840"
---
# <a name="catalogmoveproject---ssisdb-database"></a>catalog.move_project - SSISDB 資料庫
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  將專案從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的某個資料夾移動到另一個資料夾。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.move_project [ @source_folder = ] source_folder  
    , [ @project_name = ] project_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>引數  
 [ @source_folder = ] *source_folder*  
 在移動之前，專案所在之來源資料夾的名稱。 *source_folder* 是 **nvarchar(128)**。  
  
 [ @project_name = ] *project_name*  
 要移動之專案的名稱。 *project_name* 是 **nvarchar(128)**。  
  
 [ @destination_folder = ] *destination_folder*  
 在移動之後，專案所在之目的地資料夾的名稱。 *destination_folder* 是 **nvarchar(128)**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   您想要移動之專案的 READ 和 MODIFY 權限，以及目的地資料夾的 CREATE_OBJECTS 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會造成預存程序引發錯誤的某些條件：  
  
-   專案不存在  
  
-   來源資料夾不存在  
  
-   目的地資料夾不存在或目的地資料夾已包含具有相同名稱的專案  
  
-   使用者未具備適當的權限  
  
## <a name="remarks"></a>Remarks  
 當專案從來源資料夾移動到目的地資料夾時，來源資料夾中的專案和對應環境參考將遭到刪除。 目的地資料夾中會建立相同的專案和環境參考。 移動之後，相對環境參考將解析成不同的資料夾。 移動之後，絕對參考會解析成相同的資料夾。  
  
> [!NOTE]  
>  專案可以具有相對或絕對的環境參考。 相對參考會依名稱參考環境，而這些參考會要求環境位於與專案相同的資料夾中。 絕對參考會依名稱和資料夾參考環境，而這些參考會參考位於與專案資料夾不同之資料夾中的環境。  
  
  
