---
title: catalog.worker_agents (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2678853d13436811b53b40473a04191625535db
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295138"
---
# <a name="catalogworker_agents-ssisdb-database"></a>catalog.worker_agents (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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

## <a name="remarks"></a>備註
此檢視會顯示每個 Scale Out 背景工作角色連線到使用 SSISDB 目錄之 Scale Out 主機的資料列。

## <a name="permissions"></a>權限
這個檢視需要下列其中一個權限：

- **ssis_admin** 資料庫角色的成員資格

- **ssis_cluster_executor** 資料庫角色的成員資格

- **系統管理員**伺服器角色的成員資格
