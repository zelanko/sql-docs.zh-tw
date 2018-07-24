---
title: CREATE EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL RESOURCE POOL
- CREATE EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE POOL
- EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE
- EXTERNAL_RESOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL RESOURCE POOL statement
ms.assetid: 8cc798ad-c395-461c-b7ff-8c561c098808
author: HeidiSteen
ms.author: heidist
manager: cgronlund
ms.openlocfilehash: 7e4ae3239332c004ad6ceda624b641b7bf7603be
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37999290"
---
# <a name="create-external-resource-pool-transact-sql"></a>CREATE EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**適用對象**：[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 和 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

建立外部集區，以用來定義外部處理序的資源。 資源集區代表資料庫引擎執行個體的實體資源 (記憶體和 CPU) 子集。 資源管理員可讓資料庫管理員在資源集區間散發伺服器資源，最多可達 64 個集區。

+ 若是 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 中的 [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]，外部集區會掌管 `rterm.exe`、`BxlServer.exe` 及其衍生的其他處理序。

+ 若是 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] 中的 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]，外部集區可管理針對 SQL Server 2016 所列出的 R 處理序，以及 `python.exe`、`BxlServer.exe` 及其所衍生的其他處理序。

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
  
```  
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] AFFINITY CPU =    
            {  
                AUTO   
              | ( <cpu_range_spec> )   
              | NUMANODE = ( <NUMA_node_id> )   
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

*pool_name*  
這是外部資源集區的使用者定義名稱。 *pool_name* 是英數字元，最多可有 128 個字元，而且在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體內必須是唯一的，並須符合[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。  

MAX_CPU_PERCENT =*value*  
在出現 CPU 競爭時，指定外部資源集區中所有要求可接收的最大平均 CPU 頻寬。 *value* 是整數，預設值為 100。 允許的 *value* 範圍從 1 至 100。

AFFINITY {CPU = AUTO | ( \<CPU_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)} 將外部資源集區附加至特定的 CPU。 預設值是 AUTO。

AFFINITY CPU = **(** \<CPU_range_spec> **)** 會將外部資源集區對應到指定 CPU_IDs 所識別的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU。

當您使用 AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)** 時，外部資源集區會與對應到指定 NUMA 節點或節點範圍的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實體 CPU 同質化。 

MAX_MEMORY_PERCENT =*value*  
指定在此外部資源集區中，可供要求使用的伺服器記憶體總量。 *value* 是整數，預設值為 100。 允許的 *value* 範圍為 1 至 100。

MAX_PROCESSES =*value*  
指定允許外部資源集區使用的處理序數目上限。 指定 0 來為集區設定無限的閾值，這在之後只有電腦資源繫結會對其建立繫結。 預設值是 0。

## <a name="remarks"></a>Remarks

當您執行 [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) 陳述式時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 將實作資源集區。

 如需資源集區的一般資訊，請參閱[資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)、[sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 及 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)。

如需如何管理用於機器學習之外部資源集區的特定資訊，請參閱 [SQL Server 中的機器學習資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)。 

## <a name="permissions"></a>[權限]

需要 `CONTROL SERVER` 權限。

## <a name="examples"></a>範例

下列陳述式可定義外部集區，將 CPU 使用量限制為 75%，且記憶體上限為電腦中可用記憶體的 30%。

```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
  
## <a name="see-also"></a>另請參閱

 [啟用外部指令碼伺服器設定選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
