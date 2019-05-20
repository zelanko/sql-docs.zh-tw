---
title: catalog.executions (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- executions view [Integration Services]
- catalog.executions view [Integration Services]
ms.assetid: 879f13b0-331d-4dee-a079-edfaca11ae5b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b2ff22b3a5dfde43e4202062cb40737fb7d4c02e
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65714848"
---
# <a name="catalogexecutions-ssisdb-database"></a>catalog.executions (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中封裝的執行執行個體。 以 [封裝執行工作] 執行的封裝會使用與父封裝的相同執行執行個體來執行。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|execution_id|**bigint**|執行執行個體的唯一識別碼 (ID)。|  
|folder_name|**sysname(nvarchar(128))**|包含專案之資料夾的名稱。|  
|project_name|**sysname(nvarchar(128))**|專案的名稱。|  
|package_name|**nvarchar(260)**|在執行期間第一個啟動之封裝的名稱。|  
|reference_id|**bigint**|由執行執行個體所參照的環境。|  
|reference_type|**char(1)**|指出環境會位於與專案相同的資料夾 (相對參考) 中，或是在不同的資料夾 (絕對參考) 中。 當值為 `R` 時，會使用相對參考找出環境的所在位置。 當值為 `A` 時，會使用絕對參考找出環境的所在位置。|  
|environment_folder_name|**nvarchar(128)**|包含環境之資料夾的名稱。|  
|environment_name|**nvarchar(128)**|在執行期間所參考之環境的名稱。|  
|project_lsn|**bigint**|與執行執行個體對應的專案版本。 無法保證這個數字是連續的。|  
|executed_as_sid|**varbinary(85)**|啟動執行執行個體之使用者的 SID。|  
|executed_as_name|**nvarchar(128)**|用來啟動執行執行個體之資料庫主體的名稱。|  
|use32bitruntime|**bit**|指出是否使用 32 位元執行階段，在 64 位元作業系統上執行封裝。 當值為 `1` 時，會使用 32 位元執行階段來執行。 當值為 `0` 時，會使用 64 位元執行階段來執行。|  
|object_type|**smallint**|物件的類型。 物件可以是專案 (`20`) 或封裝 (`30`)。|  
|object_id|**bigint**|受作業影響之物件的識別碼。|  
|status|**int**|作業的狀態。 可能的值為已建立 (`1`)、執行中 (`2`)、已取消 (`3`)、失敗 (`4`)、暫止 (`5`)、意外結束 (`6`)、成功 (`7`)、停止 (`8`) 和已完成 (`9`)。|  
|start_time|**datetimeoffset**|執行執行個體的啟動時間。|  
|end_time|**datetimeoffsset**|執行執行個體的結束時間。|  
|caller_sid|**varbinary(85)**|使用者的安全性識別碼 (SID) (如果使用 Windows 驗證登入)。|  
|caller_name|**nvarchar(128)**|執行作業的帳戶名稱。|  
|process_id|**int**|外部處理序的處理序識別碼 (如果適用)。|  
|stopped_by_sid|**varbinary(85)**|停止執行的執行個體之使用者安全性識別碼 (SID)。|  
|stopped_by_name|**nvarchar(128)**|停止執行之執行個體的使用者名稱。|  
|total_physical_memory_kb|**bigint**|當執行開始時，伺服器上的實體記憶體總數 (以 MB 表示)。|  
|available_physical_memory_kb|**bigint**|當執行開始時，伺服器上的可用實體記憶體數量 (以 MB 表示)。|  
|total_page_file_kb|**bigint**|當執行開始時，伺服器上的分頁記憶體總數 (以 MB 表示)。|  
|available_page_file_kb|**bigint**|當執行開始時，伺服器上的可用分頁記憶體數量 (以 MB 表示)。|  
|cpu_count|**int**|當執行開始時，伺服器上的邏輯 CPU 數量。|  
|server_name|**nvarchar(128)**|指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 Windows 伺服器和執行個體資訊。|  
|machine_name|**nvarchar(128)**|執行伺服器執行個體的電腦名稱。|  
|dump_id|**uniqueidentifier**|執行傾印的識別碼。|  
  
## <a name="remarks"></a>Remarks  
 這個檢視會顯示目錄中每個執行之執行個體的資料列。  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   執行的執行個體之 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
