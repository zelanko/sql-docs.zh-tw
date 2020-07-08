---
title: catalog.extended_operation_info (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: db299b45-557d-4c62-8e14-355cdb051f63
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7beb83a2170624391dccb01f299c8710cf336644
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85672057"
---
# <a name="catalogextended_operation_info-ssisdb-database"></a>catalog.extended_operation_info (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有作業顯示擴充資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|info_id|**bigint**|擴充資訊的唯一識別碼 (ID)。|  
|operation_id|**bigint**|與擴充資訊對應之作業的唯一識別碼。|  
|object_name|**nvarchar(260)**|物件的名稱。|  
|object_type|**smallint**|受作業影響之物件的類型。 物件可以是資料夾 (`10`)、專案 (`20`)、封裝 (`30`)、環境 (`40`) 或執行執行個體 (`50`)。|  
|reference_id|**bigint**|作業中所使用之參考的唯一識別碼。|  
|status|**int**|作業狀態。 可能的值為已建立 (`1`)、執行中 (`2`)、已取消 (`3`)、失敗 (`4`)、暫止 (`5`)、意外結束 (`6`)、成功 (`7`)、停止 (`8`) 和已完成 (`9`)。|  
|start_time|**datetimeoffset(7)**|作業啟動的日期和時間。|  
|end_time|**datetimeoffset(7)**|作業結束的日期和時間。|  
  
## <a name="remarks"></a>備註  
 單一作業可以具有多個擴充資訊資料列。  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   作業的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
