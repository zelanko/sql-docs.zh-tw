---
title: catalog.executable_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 3dda28d6-10d8-4294-9b5e-a6048c07faf9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 79ef41fb52aa431325578195111ee9e4f451d9cf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85673004"
---
# <a name="catalogexecutable_statistics"></a>catalog.executable_statistics 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對每個執行的可執行檔 (包括可執行檔的每個反覆運算)，顯示一個資料列。  
  
 可執行檔是您加入至封裝之控制流程的工作或容器。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|Statistics_id|BIGINT|資料的唯一識別碼。|  
|Execution_id|BIGINT|執行之執行個體的唯一識別碼。<br /><br /> catalog.executions 檢視提供有關執行的詳細資訊。 如需詳細資訊，請參閱 [catalog.executions &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)。|  
|Executable_id|BIGINT|封裝元件的唯一識別碼。<br /><br /> catalog.executables 檢視提供有關可執行檔的詳細資訊。 如需詳細資訊，請參閱 [catalog.executables](../../integration-services/system-views/catalog-executables.md)。|  
|Execution_path|nvarchar(max)|元件封裝 (包括元件的每個反覆運算) 的完整執行路徑。|  
|Start_time|datetimeoffset(7)|可執行檔進入執行前階段的時間。|  
|End_time|datetimeoffset(7)|可執行檔進入執行後階段的時間。|  
|Execution_duration|int|可執行檔花在執行的時間長度。 值會以毫秒來表示。|  
|Execution_result|SMALLINT|以下是可能的值：<br /><br /> 0 (成功)<br /><br /> 1 (失敗)<br /><br /> 2 (完成)<br /><br /> 3 (已取消)|  
|Execution_value|sql_variant|執行所傳回的值。 這是使用者定義值。|  
  
## <a name="permissions"></a>權限  
 此檢視需要下列其中一個權限：  
  
-   執行之執行個體的 READ 權限。  
  
-   **ssis_admin** 資料庫角色的成員資格。  
  
-   **sysadmin** 伺服器角色的成員資格。  
  
  
