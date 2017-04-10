---
title: "如何︰ 建立資源集區 | Microsoft Docs"
ms.custom: ""
ms.date: "10/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# 如何︰ 建立資源集區
  本主題說明如何建立專為管理 R 中的工作負載的資源集區 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 假設您已安裝 R 服務 （資料庫），並且想要重新設定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援更多更細緻 r 所使用的資源管理的執行個體  
  
 如需管理伺服器資源的詳細資訊，請參閱 [資源管理員](../../relational-databases/resource-governor/resource-governor.md) 和 [資源管理員相關動態管理檢視 & #40。TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。  
  
 **步驟**  
  
1.  檢閱現有的資源集區的狀態  
  
2.  修改伺服器資源集區  
  
3.  建立新的資源集區外部的處理程序  
  
4.  建立分類函數，以找出 R 要求  
  
5.  確認新的外部資源集區擷取 R 作業  
  
##  <a name="bkmk_ReviewStatus"></a> 檢閱現有的資源集區的狀態  
  
1.  首先，請檢查伺服器的預設集區配置的資源。  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **結果**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|預設|0|100|0|100|100|0|0|  

2.  請查看資源配置給預設 **外部** 資源集區。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **結果**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|預設|100|20|0|2|  
 
3.  在這些伺服器預設值，R 執行階段可能會有資源不足，無法完成大部分的工作。 若要變更這種情況，您必須修改伺服器資源使用狀況，如下所示︰  
  
    -   減少可用的最大的電腦記憶體 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
    -   增加可供外部處理序的最大的電腦記憶體  
  
## 修改伺服器資源使用狀況  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ，執行下列陳述式來限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體使用量對 **60%** '最大伺服器記憶體] 設定中的值。  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  同樣地，執行下列陳述式的記憶體使用限制由外部處理序 **40%** 的總電腦資源。  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  若要強制執行這些變更，您必須重新設定並重新啟動資源管理員，如下所示︰  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  這些是以開頭; 只是建議的設定您應該評估對其他伺服器處理序的 R 需求，以判斷您的環境和工作負載的正確平衡。  
  
## 建立使用者定義的外部資源集區  
  
1.  設定資源管理員的任何變更會強制執行整個伺服器，而且會影響伺服器上，使用預設集區的工作負載，以及使用外部集區的工作負載。  
  
     因此，若要提供更細微的控制的工作負載應該具有優先順序，您可以建立新的使用者定義的外部資源集區。 您也應該定義分類函數，並將它指派給外部的資源集區。  
  
     首先，建立新的 *使用者定義的外部資源集區*。 在下列範例中，名為集區 **ds_ep**。  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     請注意新 **外部** 關鍵字。  
  
2.  建立名為工作負載群組 `ds_wg` 管理工作階段要求。 針對 SQL 查詢中，您將使用預設集區。查詢會使用所有的外部處理序 `ds_ep` 集區。  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     要求會指派給預設群組中，只要要求無法分類，或如果沒有任何其他分類失敗。  
  
     如需詳細資訊，請參閱 [資源管理員工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md) 和 [建立工作負載群組 & #40。TRANSACT-SQL &#41;](../../t-sql/statements/create-workload-group-transact-sql.md)。  
  
## 建立分類函數的 R  
  
1.  分類函數會檢查傳入的工作，並判斷工作是否可以使用目前的資源集區中執行的其中一個。 不符合準則的分類函數的工作會指派至伺服器的預設資源集區。  
  
     開始指定分類函數應該使用的資源管理員來判斷資源集區。 您可以指定 null 做為預留位置的分類函數。  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     如需詳細資訊，請參閱 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)。  
  
2.  在分類函數中的每個資源集區，您可以定義陳述式或應該指派給資源集區的連入要求的型別。  
  
     例如，下列函數會傳回指派給使用者定義的外部資源集區，傳送要求的應用程式是否 「 Microsoft R 主機 ' 或 'RStudio;' 的結構描述名稱否則會傳回預設資源集區。  
  
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
  
3.  建立函式後，重新設定新的分類函數指派至您稍早定義的外部資源群組的資源群組。  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## 確認新的資源集區和親和性  
  
1.  若要確認已進行變更，請檢查所有執行個體的資源集區相關聯的工作負載群組的每個伺服器記憶體和 CPU 的設定︰ 預設集區 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器、 外部處理序的預設資源集區和外部處理序的使用者定義集區。  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **結果**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|內部|中|25|0|0|0|0|1|2|  
    |2|預設|中|25|0|0|0|0|2|2|  
    |256|ds_wg|中|25|0|0|0|0|2|256|  
  
2.  您可以使用新的目錄檢視中， [sys.resource_governor_external_resource_pools & #40。TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), ，來檢視所有外部的資源集區。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **結果**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|預設|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     如需詳細資訊，請參閱 [資源管理員目錄檢視 & #40。TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)。  
  
3.  下列陳述式會傳回外部的資源集區會相似化為電腦資源的相關資訊。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     在此情況下，因為集區已建立的自動相似性，就會不顯示任何資訊。 如需詳細資訊，請參閱 [sys.dm_resource_governor_resource_pool_affinity & #40。TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)。  
  
## 請參閱＜  
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)   
 [R 服務的資源管理](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  