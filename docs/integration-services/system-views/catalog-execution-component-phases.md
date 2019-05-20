---
title: catalog.execution_component_phases | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 07a9a163-4787-40f7-b371-ac5c6cb4b095
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 718605c140bcf6e44cd78c9b07b8b649e0f593bf
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65714794"
---
# <a name="catalogexecutioncomponentphases"></a>catalog.execution_component_phases 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示資料流程元件在每個執行階段所花費的時間。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|phase_stats_id|**bigint**|階段的唯一識別碼 (ID)。|  
|execution_id|**bigint**|執行執行個體的唯一識別碼 (ID)。|  
|package_name|**nvarchar(260)**|在執行期間第一個啟動之封裝的名稱。|  
|task_name|**nvarchar(4000)**|資料流程工作的名稱。|  
|subcomponent_name|**nvarchar(4000)**|資料流程元件的名稱。|  
|階段|**nvarchar(128)**|執行階段的名稱。|  
|start_time|**datetimeoffset(7)**|階段開始的時間。|  
|end_time|**datetimeoffset(7)**|階段結束的時間。|  
|execution_path|**nvarchar(max)**|資料流程工作的執行路徑。|  
  
## <a name="remarks"></a>Remarks  
 此檢視針對資料流程元件的每個執行階段，各顯示一個資料列，例如：Validate、Pre-Execute、Post-Execute、PrimeOutput 和 ProcessInput。 每個資料列都會顯示特定執行階段的開始和結束的時間。  
  
## <a name="example"></a>範例  
 下列範例會使用 catalog.execution_component_phases 檢視來尋找特定套件在所有階段執行所花費的全部時間 (**active_time**)，以及套件的總經過時間 (**total_time**)。  
  
> [!WARNING]  
>  catalog.execution_component_phases 檢視會在封裝執行作業的記錄層次設定為 [效能] 或 [詳細資訊] 時，提供這項資訊。 如需詳細資訊，請參閱 [在 SSIS 伺服器上啟用封裝執行的記錄功能](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)。  
  
```sql
use SSISDB  
select package_name, task_name, subcomponent_name, execution_path,  
    SUM(DATEDIFF(ms,start_time,end_time)) as active_time,  
    DATEDIFF(ms,min(start_time), max(end_time)) as total_time  
from catalog.execution_component_phases  
where execution_id = 1841  
group by package_name, task_name, subcomponent_name, execution_path  
order by package_name, task_name, subcomponent_name, execution_path  
```  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   執行的執行個體之 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
