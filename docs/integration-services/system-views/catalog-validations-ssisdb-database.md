---
title: catalog.validations (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: dbafe110-b480-48f3-b45f-31d71ca68f62
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4409c736d53617d87c6d2a36f1f50b4eab4ee2b3
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403880"
---
# <a name="catalogvalidations-ssisdb-database"></a>catalog.validations (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有專案和封裝驗證顯示詳細資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|validation_id|**bigint**|驗證的唯一識別碼 (ID)。|  
|environment_scope|**Char(1)**|指出由驗證考量的環境參考。 當值為 `A` 時，驗證中會包含與專案相關的所有環境參考。 當值為 `S` 時，只會包含單一環境參考。 當值為 `D` 時，不會包含任何環境參考，而且每個參數必須為常值預設值，才能通過驗證。|  
|validate_type|**Char(1)**|執行的類型驗證。 可能的驗證類型為相依性驗證 (`D`) 或完整驗證 (`F`)。 封裝驗證永遠會是完整驗證。|  
|folder_name|**nvarchar(128)**|包含對應專案之資料夾的名稱。|  
|project_name|**nvarchar(128)**|專案的名稱。|  
|project_lsn|**bigint**|做為驗證依據之專案的版本。|  
|use32bitruntime|**bit**|指出是否使用 32 位元執行階段，在 64 位元作業系統上執行封裝。 當值為 `1` 時，會使用 32 位元執行階段來執行。 當值為 `0` 時，會使用 64 位元執行階段來執行。|  
|reference_id|**bigint**|專案參考環境時所使用之專案環境參考的唯一識別碼。|  
|operation_type|**smallint**|作業的類型。 在這個檢視中顯示的作業包括專案驗證 (`300`) 和封裝驗證 (`301`)。|  
|object_name|**nvarhcar(260)**|物件的名稱。|  
|object_type|**smallint**|物件的類型。 物件可以是專案 (`20`) 或封裝 (`30`)。|  
|object_id|**bigint**|受作業影響之物件的識別碼。|  
|start_time|**datetimeoffset(7)**|作業啟動的時間。|  
|end_time|**datetimeoffsset(7)**|作業結束的時間。|  
|status|**int**|作業的狀態。 可能的值為已建立 (`1`)、執行中 (`2`)、已取消 (`3`)、失敗 (`4`)、暫止 (`5`)、意外結束 (`6`)、成功 (`7`)、停止 (`8`) 和已完成 (`9`)。|  
|caller_sid|**varbinary(85)**|使用者的安全性識別碼 (SID) (如果使用 Windows 驗證登入)。|  
|caller_name|**nvarchar(128)**|執行作業的帳戶名稱。|  
|process_id|**int**|外部處理序的處理序識別碼 (如果適用)。|  
|stopped_by_sid|**varbinary(85)**|停止作業之使用者的 SID。|  
|stopped_by_name|**nvarchar(128)**|停止作業之使用者的名稱。|  
|server_name|**nvarchar(128)**|指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 Windows 伺服器和執行個體資訊。|  
|machine_name|**nvarchar(128)**|執行伺服器執行個體的電腦名稱。|  
|dump_id|**uniqueidentifier**|執行傾印的識別碼。|  
  
## <a name="remarks"></a>Remarks  
 這個檢視會針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的每個驗證顯示一行資料列。  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   對應作業的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
