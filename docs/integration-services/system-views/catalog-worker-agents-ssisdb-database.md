---
title: catalog.worker_agents (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4efc9ce081b9e319ca74247f43695dd80dcc59de
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="catalogworkeragents-ssisdb-database"></a>catalog.worker_agents (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 背景工作角色的資訊。

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|Scale Out Worker 的背景工作代理程式識別碼。|
|IsEnabled|**bit**|是否已啟用 Scale Out 背景工作角色。|
|DisplayName|**nvarchar(256)**|Scale Out 背景工作角色的顯示名稱。|
|描述|**nvarchar(256)**|Scale Out 背景工作角色的描述。|
|MachineName|**nvarchar(256)**|Scale Out 背景工作角色的電腦名稱。|
|Tags|**nvarchar(max)**|Scale Out 背景工作角色的標籤。|
|UserAccount|**nvarchar(256)**|執行 Scale Out 背景工作角色服務的使用者帳戶。|
|LastOnlineTime|**datetimeoffset(7)**|Scale Out 背景工作角色上一次上線的時間。|

## <a name="remarks"></a>Remarks
此檢視會顯示每個 Scale Out 背景工作角色連線到使用 SSISDB 目錄之 Scale Out 主機的資料列。

## <a name="permissions"></a>Permissions
這個檢視需要下列其中一個權限：

- **ssis_admin** 資料庫角色的成員資格

- **ssis_cluster_executor** 資料庫角色的成員資格

- **系統管理員**伺服器角色的成員資格
