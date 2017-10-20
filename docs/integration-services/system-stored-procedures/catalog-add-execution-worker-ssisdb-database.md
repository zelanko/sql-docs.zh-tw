---
title: "catalog.add_execution_worker （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8ce83f2678a1f3dcae6539f33beb33070b8e771b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="catalogaddexecutionworker-ssisdb-database"></a>catalog.add_execution_worker （SSISDB 資料庫）
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

新增[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]標尺出背景工作中向外執行的執行個體。

## <a name="syntax"></a>語法

```sql
add_execution_worker [@execution_id = ] execution_id, [@workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>引數
[ @execution_id =] *execution_id*  
 執行之執行個體的唯一識別碼。 *Execution_id*是**bigint**。  
 
[@workeragent_id =] *workeragent_id*  
標尺出背景工作的背景工作代理程式識別碼。 *Workeragent_id*是**uniqueIdentifier**。

## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  

## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   執行的執行個體之 READ 和 MODIFY 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
 
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
 
- 使用者未具備適當的權限。

- 執行識別碼無效。

- 背景工作代理程式識別碼無效。

- 執行不是向外。

## <a name="see-also"></a>另請參閱
[在向外執行的封裝](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)。


