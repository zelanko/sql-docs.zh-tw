---
title: catalog.operations (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- operations view [Integration Services]
- catalog.operations view [Integration Services]
ms.assetid: 9455c5b1-60ff-45fc-8599-cc3abbd6daf5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 68e848fac38e304514341973fb2e413085e8020c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85671771"
---
# <a name="catalogoperations-ssisdb-database"></a>catalog.operations (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的所有作業的詳細資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|operation_id|**bigint**|作業的唯一識別碼 (ID)。|  
|operation_type|**smallint**|作業的類型。|  
|created_time|**datetimeoffset**|建立作業的日期和時間。|  
|object_type|**smallint**|受作業影響之物件的類型。 物件可以是資料夾 (`10`)、專案 (`20`)、封裝 (`30`)、環境 (`40`) 或執行執行個體 (`50`)。|  
|object_id|**bigint**|受作業影響之物件的識別碼。|  
|object_name|**nvarchar(260)**|物件的名稱。|  
|status|**int**|作業狀態。 可能的值為已建立 (`1`)、執行中 (`2`)、已取消 (`3`)、失敗 (`4`)、暫止 (`5`)、意外結束 (`6`)、成功 (`7`)、停止 (`8`) 和已完成 (`9`)。|  
|start_time|**datetimeoffset**|作業啟動的時間。|  
|end_time|**datetimeoffsset**|作業結束的時間。|  
|caller_sid|**varbinary(85)**|使用者的安全性識別碼 (SID) (如果使用 Windows 驗證登入)。|  
|caller_name|**nvarchar(128)**|執行作業的帳戶名稱。|  
|process_id|**int**|外部處理序的處理序識別碼 (如果適用)。|  
|stopped_by_sid|**varbinary(85)**|停止作業之使用者的 SID。|  
|stopped_by_name|**nvarchar(128)**|停止作業之使用者的名稱。|  
|server_name|**nvarchar(128)**|指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 Windows 伺服器和執行個體資訊。|  
|machine_name|**nvarchar(128)**|執行伺服器執行個體的電腦名稱。|  
  
## <a name="remarks"></a>備註  
 這個檢視會針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的每個作業顯示一行資料列。 它允許系統管理員列舉伺服器上已執行的所有邏輯作業 (例如部署專案或執行封裝)。  
  
 這個檢視會顯示下列作業類型，如同 **operation_type** 資料行中所列：  
  
|**operation_type** 值|**operation_type** 描述|**object_id** 描述|**object_name** 描述|  
|-------------------------------|-------------------------------------|--------------------------------|----------------------------------|  
|`1`|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 初始化|**NULL**|**NULL**|  
|`2`|保留週期<br /><br /> (SQL Agent 作業)|**NULL**|**NULL**|  
|`3`|MaxProjectVersion<br /><br /> (SQL Agent 作業)|**NULL**|**NULL**|  
|`101`|**deploy_project**<br /><br /> (預存程序)|專案識別碼|專案名稱|  
|`106`|**restore_project**<br /><br /> (預存程序)|專案識別碼|專案名稱|  
|`200`|**create_execution** 和 **start_execution**<br /><br /> (預存程序)|專案識別碼|**NULL**|  
|`202`|**stop_operation**<br /><br /> (預存程序)|專案識別碼|**NULL**|  
|`300`|**validate_project**<br /><br /> (預存程序)|專案識別碼|專案名稱|  
|`301`|**validate_package**<br /><br /> (預存程序)|專案識別碼|套件名稱|  
|`1000`|**configure_catalog**<br /><br /> (預存程序)|**NULL**|**NULL**||  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   作業的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
