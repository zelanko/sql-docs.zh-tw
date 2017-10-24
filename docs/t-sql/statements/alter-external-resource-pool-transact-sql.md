---
title: "ALTER 外部資源集區 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d85123a34de6dea6b76c1dd4ad8dc6af3117764d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTER 外部資源集區 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  變更資源管理員外部集區已經定義外部處理序的資源。 針對 R 服務外部集區管理`rterm.exe`， `BxlServer.exe`，及其所衍生的其他處理序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
  
```  
ALTER EXTERNAL RESOURCE POOL { pool_name | "default" }  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] AFFINITY CPU =    
            {  
                AUTO   
              | ( <cpu_range_spec> )   
              | NUMANODE = (( <NUMA_node_id> )   
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
  
## <a name="arguments"></a>引數  
 { *pool_name* |"default"}  
 為現有使用者定義的外部資源集區或時，會建立預設外部資源集區的名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝。  
"default"必須加上引號 ("") 或方括號 ([]) 搭配使用時`ALTER EXTERNAL RESOURCE POOL`以避免衝突`DEFAULT`，這是系統保留字。  
  
 MAX_CPU_PERCENT =*值*  
 指定發生 CPU 競爭時，將會收到外部資源集區中的所有要求的最大平均 CPU 頻寬。 *值*是預設值為 100 的整數。 允許的範圍*值*是從 1 到 100 之間。  
  
同質 {CPU = AUTO |( \<CPU_range_spec >) |NUMANODE = (\<NUMA_node_range_spec >)} 將外部資源集區附加至特定的 Cpu。 預設值是 AUTO。  
  
CPU 親和性 = **(** \<CPU_range_spec > **)**對應的外部資源集區[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]給定 CPU_IDs 所識別的 Cpu。
  
當您使用 AFFINITY NUMANODE = **(** \<NUMA_node_range_spec > **)**，外部資源集區會相似於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]對應給定 NUMA 至實體 Cpu節點或節點範圍。
  
 MAX_MEMORY_PERCENT =*值*  
 指定可以在這個外部資源集區的要求所使用的總伺服器記憶體。 *值*是預設值為 100 的整數。 允許的範圍*值*是從 1 到 100 之間。  
  
 MAX_PROCESSES =*值*  
 指定允許的外部資源集區的處理序數目上限。 指定 0 設定無限的臨界值，只是將繫結的集區的電腦資源。 預設值是 0。  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]實作資源集區，當您執行[ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md)陳述式。  
  
 如需有關資源集區的詳細資訊，請參閱[Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)， [sys.resource_governor_external_resource_pools &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)，和[sys.dm_resource_governor_external_resource_pool_affinity &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要 `CONTROL SERVER` 權限。  
  
## <a name="examples"></a>範例  
 下列陳述式變更外部集區，50%到 25%的電腦上的可用記憶體的最大記憶體限制 CPU 使用量。  
  
```  
ALTER EXTERNAL RESOURCE POOL ep_1  
WITH (  
    MAX_CPU_PERCENT = 50  
    , AFFINITY CPU = AUTO  
    , MAX_MEMORY_PERCENT = 25  
);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [啟用外部指令碼伺服器組態選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [SQL Server R services 已知的問題](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

