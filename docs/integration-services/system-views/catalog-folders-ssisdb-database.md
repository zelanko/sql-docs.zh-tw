---
title: catalog.folders (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14930bfd90b242f30a8b3f265f6ed3b367bd07f9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296532"
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的資料夾。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|id|**bigint**|資料夾的唯一識別碼。|  
|NAME|**sysname(nvarchar(128)**|資料夾的名稱，這在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中是唯一的。|  
|description|**nvarchar(1024)**|資料夾的描述。|  
|created_by_sid|**varbinary(85)**|建立資料夾之使用者的安全性識別碼 (SID)。|  
|created_by_name|**nvarchar(128)**|建立資料夾的使用者名稱。|  
|created_time|**datetimeoffset(7)**|建立資料夾的日期和時間。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示目錄中每個資料夾的資料列。  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   資料夾的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
