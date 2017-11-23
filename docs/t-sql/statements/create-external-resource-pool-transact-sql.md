---
title: "建立外部資源集區 (TRANSACT-SQL) |Microsoft 文件"
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
f1_keywords:
- CREATE EXTERNAL RESOURCE POOL
- CREATE EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE POOL
- EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE
- EXTERNAL_RESOURCE_TSQL
dev_langs: TSQL
helpviewer_keywords: CREATE EXTERNAL RESOURCE POOL statement
ms.assetid: 8cc798ad-c395-461c-b7ff-8c561c098808
caps.latest.revision: "12"
author: jeannt
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb3da0f663ab67238c0eb133f66f465a62dcc970
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="create-external-resource-pool-transact-sql"></a>建立外部資源集區 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]和[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

建立外部集區，用來定義外部處理序的資源。 資源集區代表的 Database Engine 執行個體的實體資源 （記憶體和 Cpu） 的子集。 資源管理員可讓資料庫管理員在資源集區間散發伺服器資源，最多可達 64 個集區。

+ 如[!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]中[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]，外部集區控管`rterm.exe`， `BxlServer.exe`，及其所衍生的其他處理序。

+ 如[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]中[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]，外部集區會管理 SQL Server 2016 中，針對列出的 R 處理序以及`python.exe`， `BxlServer.exe`，及其所衍生的其他處理序。

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
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
是使用者定義的外部資源集區名稱。 *pool_name*是英數字元可以是最多 128 個字元，必須是唯一的執行個體內[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，且必須符合的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  

MAX_CPU_PERCENT =*值*  
指定發生 CPU 競爭時，可接收外部資源集區中的所有要求的最大平均 CPU 頻寬。 *值*是預設值為 100 的整數。 允許的範圍*值*是從 1 到 100 之間。

同質 {CPU = AUTO |( \<CPU_range_spec >) |NUMANODE = (\<NUMA_node_range_spec >)} 將外部資源集區附加至特定的 Cpu。 預設值是 AUTO。

CPU 親和性 = **(** \<CPU_range_spec > **)**對應的外部資源集區[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]給定 CPU_IDs 所識別的 Cpu。

當您使用 AFFINITY NUMANODE = **(** \<NUMA_node_range_spec > **)**，外部資源集區會相似於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]對應給定 NUMA 至實體 Cpu節點或節點範圍。 

MAX_MEMORY_PERCENT =*值*  
指定可以在這個外部資源集區的要求所使用的總伺服器記憶體。 *值*是預設值為 100 的整數。 允許的範圍*值*是從 1 到 100 之間。

MAX_PROCESSES =*值*  
指定允許的外部資源集區的處理序數目上限。 指定 0 設定無限的臨界值之後繫結只能由電腦資源集區。 預設值是 0。

## <a name="remarks"></a>備註

[!INCLUDE[ssDE](../../includes/ssde-md.md)]實作資源集區，當您執行[ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md)陳述式。

 一般資源集區的詳細資訊，請參閱[Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)， [sys.resource_governor_external_resource_pools &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)，和[sys.dm_resource_governor_external_resource_pool_affinity &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).

單指管理機器學習所使用的外部資源集區的資訊，請參閱[資源管理針對 SQL Server 中的機器學習](../../advanced-analytics/r/resource-governance-for-r-services.md)。 

## <a name="permissions"></a>Permissions

需要 `CONTROL SERVER` 權限。

## <a name="examples"></a>範例

下列陳述式定義外部集區，75%到 30%的電腦上的可用記憶體的最大記憶體限制 CPU 使用量。

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

 [啟用外部指令碼伺服器組態選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [ALTER 外部資源集區 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
