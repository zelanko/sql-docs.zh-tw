---
title: catalog.enable_worker_agent (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c6e5266b-c32d-49ff-aa69-f09664009fb4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a72e4f786809c5e977f2bb005bf9780e3c9ee192
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290694"
---
# <a name="catalogenableworkeragent-ssisdb-database"></a>catalog.enable_worker_agent (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

啟用處理此 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄之 Scale Out Master 的 Scale Out Worker。

## <a name="syntax"></a>語法

```sql
catalog.enable_worker_agent [@WorkerAgentId =] WorkerAgentId
```
## <a name="arguments"></a>引數
[@WorkerAgentId =] *WorkerAgentId*：Scale Out Worker 的背景工作代理程式識別碼。 *WorkerAgentId* 是 **uniqueidentifier**。

## <a name="example"></a>範例
這個範例會在 MachineA 上啟用相應放大背景工作。

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  

## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格 

## <a name="errors-and-warnings"></a>錯誤和警告
如果背景工作代理程式識別碼無效，則預存程序會傳回錯誤。
