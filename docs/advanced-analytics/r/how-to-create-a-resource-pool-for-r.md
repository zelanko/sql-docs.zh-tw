---
title: "操作說明：建立 R 的資源集區 | Microsoft Docs"
ms.custom: 
ms.date: 10/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: be3afb3a1ff5175fbb3d0735cde59bd19bb47f6c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="how-to-create-a-resource-pool-for-r"></a>操作說明：建立 R 的資源集區
  本主題說明如何特別針對管理 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的 R 工作負載建立資源集區。 此處假設您已經安裝 R Services (資料庫內)，而想要重新設定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體，以支援對 R 所使用的資源進行更精細的管理。  
  
 如需有關管理伺服器資源的詳細資訊，請參閱 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) 和 [Resource Governor 相關的動態管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。  
  
 **步驟**  
  
1.  檢閱現有資源集區的狀態  
  
2.  修改伺服器資源集區  
  
3.  為外部處理序建立新的資源集區  
  
4.  建立分類函數以識別 R 要求  
  
5.  確認新的外部資源集區正在擷取 R 作業  
  
##  <a name="bkmk_ReviewStatus"></a> 檢閱現有資源集區的狀態  
  
1.  首先，檢查配置給伺服器預設集區的資源。  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **結果**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|預設|0|100|0|100|100|0|0|  

2.  檢查配置給預設「外部」資源集區的資源。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **結果**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|預設|100|20|0|2|  
 
3.  在這些伺服器預設設定下，R 執行階段可能會沒有足夠的資源來完成大多數工作。 若要變更此情況，您必須依下列方式修改伺服器資源使用量：  
  
    -   調降 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可使用的電腦記憶體上限  
  
    -   調升外部處理序可使用的電腦記憶體上限  
  
## <a name="modify-server-resource-usage"></a>修改伺服器資源量  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，執行下列陳述式以將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體使用量限制為 [最大伺服器記憶體] 設定值的 **60%**。  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  同樣地，執行下列陳述式以將外部處理序的記憶體使用量限制為總電腦資源的 **40%**。  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  若要強制執行這些變更，您必須依下列方式重新設定並重新啟動 Resource Governor：  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  這些只是建議的起始設定；您應該對照其他伺服器處理序來評估 R 需求，以判斷您環境與工作負載的正確平衡點。  
  
## <a name="create-a-user-defined-external-resource-pool"></a>建立使用者定義的外部資源集區  
  
1.  對 Resource Governor 設定所做的任何變更都會在整個伺服器強制執行，並且除了影響使用外部集區的工作負載之外，也會影響使用伺服器預設集區的工作負載。  
  
     因此，為了能夠以更精細的方式控制哪些工作負載應該優先，您可以建立一個新的使用者定義外部資源集區。 您還應該定義一個分類函數，並將它指派給外部資源集區。  
  
     請從建立一個新的「使用者定義的外部資源集區」開始著手。 在接下來的範例中，該集區是命名為 **ds_ep**。  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     請注意新的 **EXTERNAL** 關鍵字。  
  
2.  建立一個名為 `ds_wg` 的工作負載群組以用於管理工作階段要求。 針對 SQL 查詢，您將會使用預設集區；針對所有外部處理序查詢，則會使用 `ds_ep` 集區。  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     每當無法將要求分類，或是如果發生任何其他分類失敗時，都會將要求指派給預設群組。  
  
     如需詳細資訊，請參閱 [Resource Governor 工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)和 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)。  
  
## <a name="create-a-classification-function-for-r"></a>建立 R 的分類函數  
  
1.  分類函數會檢查內送的工作，並判斷該工作是否是可使用目前的資源集區來執行的工作。 針對不符合分類函數準則的工作，系統會將其指派回給伺服器的預設資源集區。  
  
     請從指定 Resource Governor 應該使用分類函數來判斷資源集區開始著手。 您可以指派 Null 作為分類函數的預留位置。  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     如需詳細資訊，請參閱 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)。  
  
2.  在每個資源集區的分類函數中，您需定義應指派給資源集區的陳述式或內送要求的類型。  
  
     例如，如果傳送要求的應用程式是 'Microsoft R Host' 或 'RStudio'，下列函數就會傳回指派給使用者定義外部資源集區之結構描述的名稱；否則會傳回預設資源集區。  
  
    ```  
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
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## <a name="verify-new-resource-pools-and-affinity"></a>確認新的資源集區和親和性  
  
1.  若要確認是否已進行變更，請針對與所有執行個體資源集區關聯的每個工作負載群組，檢查伺服器記憶體和 CPU 的設定：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器的預設集區、外部處理序的預設資源集區，以及外部處理序的使用者定義集區。  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **結果**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|內部|中|25|0|0|0|0|1|2|  
    |2|預設|中|25|0|0|0|0|2|2|  
    |256|ds_wg|中|25|0|0|0|0|2|256|  
  
2.  您可以使用新的目錄檢視 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 來檢視所有外部資源集區。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **結果**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|預設|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     如需詳細資訊，請參閱 [Resource Governor 目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)。  
  
3.  下列陳述式會傳回與外部資源集區產生親和性之電腦資源的相關資訊。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     在此案例中，由於建立集區時已將親和性指定為 AUTO，因此不會顯示任何資訊。 如需詳細資訊，請參閱 [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)   
 [R Services 的資源管理](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  

