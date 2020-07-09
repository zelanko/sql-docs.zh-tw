---
title: catalog.delete_folder (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b9c08992-500c-447e-bc19-1eb13c9b0293
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4e9986843ce2196cd4450bac806631a862147ef4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749599"
---
# <a name="catalogdelete_folder-ssisdb-database"></a>catalog.delete_folder (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄刪除資料夾。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.delete_folder [ @folder_name = ] folder_name  
```  
  
## <a name="arguments"></a>引數  
 [ @folder_name = ] *folder_name*  
 要刪除之資料夾的名稱。 *folder_name* 是 **nvarchar(128)** 。  
  
## <a name="return-code-value"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 傳回訊息以確認資料夾的刪除。  
  
  
