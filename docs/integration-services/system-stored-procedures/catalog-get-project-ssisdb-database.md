---
title: catalog.get_project (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f263c9e4-a7db-4888-a458-70ae99b1f729
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 79756562767943d89efd199007941cf9bf29b702
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65716172"
---
# <a name="cataloggetproject-ssisdb-database"></a>catalog.get_project (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  擷取已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器之專案的二進位資料流。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.get_project [ @folder_name = ] folder_name , [ @project_name = ] project_name   
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name = ] *folder_name*  
 包含專案之資料夾的名稱。 *folder_name* 是 **nvarchar(128)** 。  
  
 [ @project_name = ] *project_name*  
 專案的名稱。 *project_name* 是 **nvarchar(128)** 。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 專案的二進位資料流會當作 **varbinary(MAX)** 傳回。 如果找不到資料夾或專案，則會不傳回任何結果。  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會造成 get_project 預存程序引發錯誤的某些條件：  
  
-   專案不存在  
  
-   資料夾不存在  
  
-   使用者未具備適當的權限  
  
  
