---
title: "catalog.add_execution_worker (SSISDB 資料庫) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d5ecc54863b47ef55269a068353cbc25bbd5d008
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="catalogaddexecutionworker-ssisdb-database"></a>catalog.add_execution_worker (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker 新增 Scale Out 中的執行個體。

## <a name="syntax"></a>語法

```sql
catalog.add_execution_worker [@execution_id = ] execution_id, [@workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>引數
[ @execution_id = ] *execution_id*  
 執行之執行個體的唯一識別碼。 *execution_id* 是 **bigint**。  
 
[@workeragent_id = ] *workeragent_id*  
Scale Out Worker 的背景工作代理程式識別碼。 *workeragent_id* 是 **uniqueidentifier**。

## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  

## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   執行的執行個體之 READ 和 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **sysadmin** 伺服器角色的成員資格  
 
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
 
- 使用者未具備適當的權限。

- 執行識別碼無效。

- 背景工作代理程式識別碼無效。

- 執行不是在 Scale Out 中。

## <a name="see-also"></a>另請參閱
[在 Scale Out 中執行套件](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)。

