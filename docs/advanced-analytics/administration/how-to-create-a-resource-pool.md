---
title: 如何建立 R 和 Python 的資源集區
description: 在 SQL Server 2016 或 SQL Server 2017 database engine 實例上, 定義 R 或 Python 進程的 SQL Server 資源集區。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5b58c2a42334352d64aa2cea61a75585f29996c3
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344066"
---
# <a name="how-to-create-a-resource-pool-for-machine-learning-in-sql-server"></a>如何在 SQL Server 中建立機器學習服務的資源集區
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何建立和使用資源集區, 專門用來管理 SQL Server 中的 R 和 Python 機器學習服務工作負載。 它假設您已安裝並啟用機器學習功能, 並想要重新設定實例, 以支援更精細的管理外部進程 (例如 R 或 Python) 所使用的資源。

此套裝程式含多個步驟:

1.  檢查任何現有資源集區的狀態。 請務必瞭解哪些服務使用現有的資源。
2.  修改伺服器資源集區。
3.  為外部進程建立新的資源集區。
4.  建立分類功能以識別外部腳本要求。
5.  確認新的外部資源集區正在從指定的用戶端或帳戶中, 捕獲 R 或 Python 作業。

##  <a name="bkmk_ReviewStatus"></a> 檢閱現有資源集區的狀態
  
1.  使用如下的語句來檢查配置給伺服器之預設集區的資源。
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **範例結果**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|預設|0|100|0|100|100|0|0|

2.  檢查配置給預設「外部」  資源集區的資源。
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **範例結果**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|預設|100|20|0|2|
 
3.  在這些伺服器預設設定下, 外部執行時間可能會有足夠的資源來完成大部分的工作。 若要變更此情況，您必須依下列方式修改伺服器資源使用量：
  
    -   減少資料庫引擎可以使用的電腦記憶體上限。
  
    -   增加外部進程可使用的電腦記憶體上限。

## <a name="modify-server-resource-usage"></a>修改伺服器資源量

1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，執行下列陳述式以將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體使用量限制為 [最大伺服器記憶體] 設定值的 **60%** 。

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2.  同樣地，執行下列陳述式以將外部處理序的記憶體使用量限制為總電腦資源的 **40%** 。
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  若要強制執行這些變更，您必須依下列方式重新設定並重新啟動 Resource Governor：
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  這些只是建議的設定, 以開始使用;您應該在其他伺服器進程中評估機器學習工作, 以判斷您的環境和工作負載的正確平衡。

## <a name="create-a-user-defined-external-resource-pool"></a>建立使用者定義的外部資源集區
  
1.  對 Resource Governor 設定所做的任何變更都會在整個伺服器強制執行，並且除了影響使用外部集區的工作負載之外，也會影響使用伺服器預設集區的工作負載。
  
     因此，為了能夠以更精細的方式控制哪些工作負載應該優先，您可以建立一個新的使用者定義外部資源集區。 您還應該定義一個分類函數，並將它指派給外部資源集區。 **EXTERNAL**關鍵字是 new。
  
     請從建立一個新的「使用者定義的外部資源集區」  開始著手。 在接下來的範例中，該集區是命名為 **ds_ep**。
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  建立一個名為 `ds_wg` 的工作負載群組以用於管理工作階段要求。 針對 SQL 查詢，您將會使用預設集區；針對所有外部處理序查詢，則會使用 `ds_ep` 集區。
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     每當無法將要求分類，或是如果發生任何其他分類失敗時，都會將要求指派給預設群組。
  
     如需詳細資訊，請參閱 [Resource Governor 工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)和 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)。
  
## <a name="create-a-classification-function-for-machine-learning"></a>建立機器學習服務的分類函式
  
分類函數會檢查內送的工作，並判斷該工作是否是可使用目前的資源集區來執行的工作。 針對不符合分類函數準則的工作，系統會將其指派回給伺服器的預設資源集區。
  
1. 一開始先指定應該使用分類函數來判斷資源集區 Resource Governor。 您可以指派**null**做為分類函數的預留位置。
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     如需詳細資訊，請參閱 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)。
  
2.  在每個資源集區的分類函數中, 定義應指派給資源集區的語句類型或傳入要求。
  
     例如，如果傳送要求的應用程式是 'Microsoft R Host' 或 'RStudio'，下列函數就會傳回指派給使用者定義外部資源集區之結構描述的名稱；否則會傳回預設資源集區。
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  建立函數之後，重新設定資源群組，以將新的分類函數指派給您稍早定義的外部資源集區。
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR WITH reconfigure;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>確認新的資源集區和親和性

若要確認是否已進行變更, 您應該檢查與這些實例資源集區相關聯的每個工作負載群組的伺服器記憶體和 CPU 設定:

+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]伺服器的預設集區
+ 外部進程的預設資源集區
+ 外部進程的使用者定義集區

1. 執行下列語句來查看所有工作負載群組:

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **範例結果**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|內部|中|25|0|0|0|0|1|2|
    |2|預設|中|25|0|0|0|0|2|2|
    |256|ds_wg|中|25|0|0|0|0|2|256|
  
2.  使用新的目錄檢視[resource_governor_external_resource_pools &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)來查看所有外部資源集區。
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **範例結果**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|預設|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     如需詳細資訊，請參閱 [Resource Governor 目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)。
  
3.  執行下列語句, 以傳回相似化為至外部資源集區之電腦資源的相關資訊 (若適用):
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     在此案例中，由於建立集區時已將親和性指定為 AUTO，因此不會顯示任何資訊。 如需詳細資訊，請參閱 [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)。

## <a name="see-also"></a>另請參閱

如需管理伺服器資源的詳細資訊, 請參閱:

+  [資源管理員](../../relational-databases/resource-governor/resource-governor.md) 
+ [Resource Governor 相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

如需機器學習服務的資源管理總覽, 請參閱:

+  [Machine Learning 服務的資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)
