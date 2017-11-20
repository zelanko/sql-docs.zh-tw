---
title: "catalog.execution_data_statistics |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: fa1d87489ff6d0a10d95bf160ded3d038ca39d81
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="catalogexecutiondatastatistics"></a>catalog.execution_data_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  每當資料流程元件傳送資料至特定封裝執行的下游元件，此檢視就會顯示一個資料列。 此檢視中的資訊可用來計算元件的資料輸送量。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|資料的唯一識別碼 (ID)。|  
|execution_id|**bigint**|執行執行個體的唯一識別碼 (ID)。|  
|package_name|**nvarchar （260)**|在執行期間第一個啟動之封裝的名稱。|  
|task_name|**nvarchar(4000)**|資料流程工作的名稱。|  
|dataflow_path_id_string|**nvarchar(4000)**|資料流程路徑的識別字串。|  
|dataflow_path_name|**nvarchar(4000)**|資料流程路徑的名稱。|  
|source_component_name|**nvarchar(4000)**|已傳送資料的資料流程元件名稱。|  
|destination_component_name|**nvarchar(4000)**|已接收資料的資料流程元件名稱。|  
|rows_sent|**bigint**|從來源元件傳送的資料列數目。|  
|created_time|**datatimeoffset(7)**|取得值的時間。|  
|execution_path|**nvarchar(max)**|元件的執行路徑。|  
  
## <a name="remarks"></a>備註  
  
-   當元件有多個輸出時，就會針對每個輸出各加入一個資料列。  
  
-   依預設，當執行開始時，並不會記錄所傳送之資料列數目的詳細資訊。  
  
-   若要檢視特定的封裝執行此資料，設定記錄層級為**Verbose**。 如需詳細資訊，請參閱 [在 SSIS 伺服器上啟用封裝執行的記錄功能](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)。  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   執行的執行個體之 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  

