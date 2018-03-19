---
title: ALTER EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: jeannt
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb4073a8114e953dc9df87614a63e074ab8c9683
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTER EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 和 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

變更 Resource Governor 外部集區，其指定外部處理序可以使用的資源。 

+ 若是 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 中的 [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]，外部集區會掌管 `rterm.exe`、`BxlServer.exe` 及其衍生的其他處理序。

+ 若是 SQL Server 2017 中的 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]，外部集區會掌管為先前版本列出的 R 處理序，以及 `python.exe`、`BxlServer.exe` 及其衍生的其他處理序。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

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

{ *pool_name* | "default" }  
這是現有的使用者定義外部資源集區名稱，或是安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時建立的預設外部資源集區名稱。
搭配 `ALTER EXTERNAL RESOURCE POOL` 使用時，"default" 必須加上引號 ("") 或方括號 ([]) 才能避免與系統保留字 `DEFAULT` 產生衝突。


MAX_CPU_PERCENT =*value*  
在出現 CPU 競爭時，指定外部資源集區中所有要求可接收的最大平均 CPU 頻寬。 *value* 是預設值為 100 的整數。 允許的 *value* 範圍為 1 至 100。


AFFINITY {CPU = AUTO | ( \<CPU_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)}  
將外部資源集區附加到指定的 CPU。 預設值是 AUTO。

AFFINITY CPU = **(** \<CPU_range_spec> **)** 會將外部資源集區對應到指定 CPU_IDs 所識別的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU。 當您使用 AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)** 時，外部資源集區會與對應到指定 NUMA 節點或節點範圍的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實體 CPU 同質化。


MAX_MEMORY_PERCENT =*value*  
指定在此外部資源集區中，可供要求使用的伺服器記憶體總量。 *value* 是預設值為 100 的整數。 允許的 *value* 範圍為 1 至 100。


MAX_PROCESSES =*value*  
指定允許外部資源集區使用的處理序數目上限。 指定 0 來為集區設定無限的閾值，這在之後只有電腦資源繫結會對其建立繫結。 預設值是 0。

## <a name="remarks"></a>Remarks

當您執行 [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) 陳述式時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 將實作資源集區。

如需資源集區的一般資訊，請參閱 [Resource Governor 資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)、[sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)及 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)。  

如需使用外部資源集區來管理機器學習工作的特定資訊，請參閱 [SQL Server 中的機器學習資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)...
## <a name="permissions"></a>Permissions

需要 `CONTROL SERVER` 權限。

## <a name="examples"></a>範例

下列陳述式會變更外部集區，其限制 CPU 使用量為 50%，電腦中可用記憶體的最大記憶體為 25%。
  
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

[DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)

[ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)

[CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)

[資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

[ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
