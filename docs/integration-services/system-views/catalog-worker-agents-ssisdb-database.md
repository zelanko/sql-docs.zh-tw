---
title: "catalog.worker_agents （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d56af0ab150255c53746898a638a32112938755c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="catalogworkeragents-ssisdb-database"></a>catalog.worker_agents （SSISDB 資料庫）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

顯示的資訊[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]標尺出背景工作。

|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|背景工作代理程式識別碼的標尺出背景工作。|
|IsEnabled|**bit**|是否已啟用延展出背景工作。|
|DisplayName|**nvarchar(256)**|標尺出背景工作的顯示名稱。|
|Description|**nvarchar(256)**|標尺出背景工作的描述。|
|MachineName|**nvarchar(256)**|標尺出背景工作電腦名稱。|
|Tags|**nvarchar(max)**|標尺出工作者的標記。|
|UserAccount|**nvarchar(256)**|使用者執行服務的帳戶向出背景工作。|
|LastOnlineTime|**datetimeoffset(7)**|標尺出工作者正在線上上一次。|

## <a name="remarks"></a>備註
此檢視會顯示一個資料列的每個標尺出背景工作連接到使用 SSISDB 目錄出主要刻度。

## <a name="permissions"></a>Permissions
這個檢視需要下列其中一個權限：

- 成員資格**ssis_admin**資料庫角色

- 成員資格**ssis_cluster_executor**資料庫角色

- 成員資格**sysadmin**伺服器角色

