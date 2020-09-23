---
title: 建立資源集區
description: 了解如何建立及使用資源集區來管理 SQL Server 機器學習服務中的 Python 與 R 工作負載。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08f2c66fec80ce27e3e7a9ffca7a00194ff3b81b
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283759"
---
# <a name="create-a-resource-pool-for-sql-server-machine-learning-services"></a>建立 SQL Server 機器學習服務的資源集區
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

了解如何建立及使用資源集區來管理 SQL Server 機器學習服務中的 Python 與 R 工作負載。 

此程序包括多個步驟：

1. 檢閱現有資源集區的狀態。 請務必了解哪些服務使用現有的資源。
2. 修改伺服器資源集區。
3. 為外部處理序建立新的資源集區。
4. 建立分類函數函式以識別外部指令碼要求。
5. 確認新的外部資源集區正在從指定的用戶端或帳戶擷取 R 與 Python 作業。

<a name="bkmk_ReviewStatus"></a>

##  <a name="review-the-status-of-existing-resource-pools"></a>檢閱現有資源集區的狀態
  
1.  使用如下陳述式檢查指派給伺服器預設集區的資源。
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **範例結果**

    |pool_id|NAME|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|預設|0|100|0|100|100|0|0|

2.  檢查指派給預設「外部」資源集區的資源。
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **範例結果**

    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|預設|100|20|0|2|
 
3.  在這些伺服器預設設定下，外部執行階段可能會沒有足夠的資源來完成大多數工作。 若要改善資源，您必須依下列方式修改伺服器資源使用量：
  
    -   調降資料庫引擎可使用的電腦記憶體上限。
  
    -   調高外部處理序可使用的電腦記憶體上限。

## <a name="modify-server-resource-usage"></a>修改伺服器資源量

1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，執行下列陳述式以將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體使用量限制為 [最大伺服器記憶體] 設定值的 **60%** 。

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2. 執行下列陳述式以將外部處理序的記憶體使用量限制為總電腦資源的 **40%** 。
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  若要強制執行這些變更，您必須依下列方式重新設定並重新啟動 Resource Governor：
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  這些只是建議的起始設定；您應該對照其他伺服器處理序評估機器學習工作，以判斷您環境與工作負載的正確平衡點。

## <a name="create-a-user-defined-external-resource-pool"></a>建立使用者定義的外部資源集區
  
1.  對 Resource Governor 設定的所有變更都會在整個伺服器上強制執行。 這些變更會影響使用伺服器預設集區的工作負載，也會影響使用外部集區的工作負載。
  
     為了能夠以更精細的方式控制哪些工作負載應該優先，您可以建立一個新的使用者定義外部資源集區。 請定義一個分類函式，並將其指派給外部資源集區。 **EXTERNAL** 關鍵字是新的。
  
     建立新的*使用者定義的外部資源集區*。 在接下來的範例中，該集區是命名為 **ds_ep**。
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  建立一個名為 `ds_wg` 的工作負載群組以用於管理工作階段要求。 針對 SQL 查詢，您將會使用預設集區；針對所有外部處理序查詢，則會使用 `ds_ep` 集區。
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     每當無法將要求分類，或是如果發生任何其他分類失敗時，都會將要求指派給預設群組。

 
如需詳細資訊，請參閱 [Resource Governor 工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)和 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)。
  
## <a name="create-a-classification-function-for-machine-learning"></a>建立機器學習的分類函式
  
分類函式會檢查傳入工作。 它會判斷該工作是否是可使用目前的資源集區來執行的工作。 針對不符合分類函數準則的工作，系統會將其指派回給伺服器的預設資源集區。
  
1. 請從指定 Resource Governor 應該使用分類函式來判斷資源集區開始著手。 您可以指派 **Null** 作為分類函式的預留位置。
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     如需詳細資訊，請參閱 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)。
  
2.  在每個資源集區的分類函式中，您必須定義應指派給資源集區的陳述式或內送要求類型。
  
     例如，如果傳送要求的應用程式是 'Microsoft R Host'、'RStudio' 或 'Mashup'，下列函數就會傳回指派給使用者定義外部資源集區之結構描述的名稱；否則會傳回預設資源集區。
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio', 'Mashup') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  建立函數之後，重新設定資源群組，以將新的分類函數指派給您稍早定義的外部資源集區。
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>確認新的資源集區和親和性

檢查每個工作負載群組的伺服器記憶體設定和 CPU。 請檢閱下列項目，確認已進行執行個體資源變更：

+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器的預設集區
+ 外部處理序的預設資源集區
+ 外部處理序的使用者定義集區

1. 執行下列陳述式來檢視所有工作負載群組：

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **範例結果**

    |group_id|NAME|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|internal|中|25|0|0|0|0|1|2|
    |2|default|中|25|0|0|0|0|2|2|
    |256|ds_wg|中|25|0|0|0|0|2|256|
  
2.  使用新的目錄檢視 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 來檢視所有外部資源集區。
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **範例結果**
    
    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|default|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     如需詳細資訊，請參閱 [Resource Governor 目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)。
  
3.  執行下列陳述式以傳回與外部資源集區產生親和性之電腦資源的相關資訊 (若適用)：
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     由於建立集區時將親和性指定為 AUTO，因此不會顯示任何資訊。 如需詳細資訊，請參閱 [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)。

## <a name="next-steps"></a>後續步驟

如需有關管理伺服器資源的詳細資訊，請參閱：

+ [資源管理員](../../relational-databases/resource-governor/resource-governor.md) 
+ [Resource Governor 相關動態管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

如需機器學習的資源治理概觀，請參閱：

+ [使用 SQL Server 機器學習服務中的 Resource Governor 管理 Python 與 R 工作負載](resource-governor.md)
