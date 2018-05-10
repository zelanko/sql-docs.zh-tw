---
title: catalog.executable_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 3dda28d6-10d8-4294-9b5e-a6048c07faf9
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f952429dfe0003b0b3ccc7c75565cd30702aa55
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="catalogexecutablestatistics"></a>catalog.executable_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
|Execution_duration|ssNoversion|可執行檔花在執行的時間長度。 值會以毫秒來表示。|  
|Execution_result|SMALLINT|以下是可能的值：<br /><br /> 0 (成功)<br /><br /> 1 (失敗)<br /><br /> 2 (完成)<br /><br /> 3 (已取消)|  
|Execution_value|sql_variant|執行所傳回的值。 這是使用者定義值。|  
  
## <a name="permissions"></a>Permissions  
 此檢視需要下列其中一個權限：  
  
-   執行之執行個體的 READ 權限。  
  
-   **ssis_admin** 資料庫角色的成員資格。  
  
-   **sysadmin** 伺服器角色的成員資格。  
  
  
