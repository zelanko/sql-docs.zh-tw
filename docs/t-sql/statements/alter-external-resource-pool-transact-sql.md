---
title: "ALTER 外部資源集區 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs: TSQL
helpviewer_keywords: ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
caps.latest.revision: "10"
author: jeannt
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb4073a8114e953dc9df87614a63e074ab8c9683
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTER 外部資源集區 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]和[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

變更資源管理員的外部集區，指定可由外部處理序的資源。 

+ 如[!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]中[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]，外部集區控管`rterm.exe`， `BxlServer.exe`，及其所衍生的其他處理序。

+ 如[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]外部集區會在 SQL Server 2017，管理 R 處理序所列的先前版本中，以及`python.exe`， `BxlServer.exe`，及其所衍生的其他處理序。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>語法

```sql
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
指定發生 CPU 競爭時，可接收外部資源集區中的所有要求的最大平均 CPU 頻寬。 *值*是預設值為 100 的整數。 允許的範圍*值*是從 1 到 100 之間。


同質 {CPU = AUTO |( \<CPU_range_spec >) |NUMANODE = (\<NUMA_node_range_spec >)}  
將外部資源集區連接至特定的 Cpu。 預設值是 AUTO。

CPU 親和性 = **(** \<CPU_range_spec > **)**對應的外部資源集區[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]給定 CPU_IDs 所識別的 Cpu。 當您使用 AFFINITY NUMANODE = **(** \<NUMA_node_range_spec > **)**，外部資源集區會相似於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]對應給定 NUMA 至實體 Cpu節點或節點範圍。


MAX_MEMORY_PERCENT =*值*  
指定可以在這個外部資源集區的要求所使用的總伺服器記憶體。 *值*是預設值為 100 的整數。 允許的範圍*值*是從 1 到 100 之間。


MAX_PROCESSES =*值*  
指定允許的外部資源集區的處理序數目上限。 指定 0 設定無限的臨界值之後繫結只能由電腦資源集區。 預設值是 0。

## <a name="remarks"></a>備註

[!INCLUDE[ssDE](../../includes/ssde-md.md)]實作資源集區，當您執行[ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md)陳述式。

一般資源集區的詳細資訊，請參閱[Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)， [sys.resource_governor_external_resource_pools &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)，和[sys.dm_resource_governor_external_resource_pool_affinity &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).  

如需特定資訊可讓您使用的外部資源集區來管理機器學習工作，請參閱[資源管理針對 SQL Server 中的機器學習](../../advanced-analytics/r/resource-governance-for-r-services.md)...
## <a name="permissions"></a>Permissions

需要 `CONTROL SERVER` 權限。

## <a name="examples"></a>範例

下列陳述式變更外部集區，50%到 25%的電腦上的可用記憶體的最大記憶體限制 CPU 使用量。
  
```sql
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

[SQL Server 中的機器學習資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)

[外部指令碼已啟用伺服器組態選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

[卸除的外部資源集區 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)

[ALTER RESOURCE POOL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)

[建立工作負載群組 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-workload-group-transact-sql.md)

[資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

[ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
