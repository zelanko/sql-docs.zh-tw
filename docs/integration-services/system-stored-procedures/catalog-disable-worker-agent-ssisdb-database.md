---
title: "catalog.disable_worker_agent （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: aab83dd2f179c8e6b90ad9ff7a212597a51038de
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>catalog.disable_worker_agent （SSISDB 資料庫）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

停用的標尺出 Master，與此工作的標尺出工作者[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]類別目錄。

## <a name="syntax"></a>語法

```tsql
disable_worker_agent [@WorkerAgentId = ] WorkerAgentId
```
## <a name="arguments"></a>引數
[ @WorkerAgentId =] *WorkerAgentId*標尺出背景工作的背景工作代理程式識別碼。 *WorkerAgentId*是**uniqueidentifier**。

## <a name="example"></a>範例
這個範例會停用上 MachineA 出工作者小數位數。
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[disable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  

## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色 

## <a name="errors-and-warnings"></a>錯誤和警告
如果不是有效的背景工作代理程式識別碼，預存程序會傳回錯誤。

