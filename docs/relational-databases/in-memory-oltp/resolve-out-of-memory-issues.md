---
title: 解決記憶體不足問題 | Microsoft 文件
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e29658950a9a058214fea4cf9e7bdcfda9daa808
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="resolve-out-of-memory-issues"></a>解決記憶體不足問題
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 所使用的記憶體比 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]更多，而且使用方式也不同。 您所安裝並配置給 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 的記憶體數量可能會變得不足以支應成長的需求。 若是如此，您可能會用完記憶體。 本主題將說明如何從 OOM 情況中復原。 如需可協助您避免多種 OOM 情況的指引，請參閱 [監視與疑難排解記憶體使用量](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md) 。  
  
## <a name="covered-in-this-topic"></a>本主題所涵蓋的內容  
  
|主題|概觀|  
|-----------|--------------|  
|[解決由於 OOM 所造成的資料庫還原失敗](#bkmk_resolveRecoveryFailures)|若您收到錯誤訊息：「資料庫 '*\<資料庫名稱>*' 的還原作業因為資源集區 '*\<資源集區名稱>*' 中的記憶體不足而失敗」，該怎麼辦。|  
|[解決低記憶體或 OOM 狀況對於工作負載的影響](#bkmk_recoverFromOOM)|如果您發現低記憶體問題對於效能造成負面影響，該怎麼辦。|  
|[解決有足夠的記憶體可用但卻記憶體不足所造成的頁面配置失敗](#bkmk_PageAllocFailure)|若您收到錯誤訊息：「不允許資料庫 '*\<資料庫名稱>*' 的頁面配置，因為資源集區 '*\<資源集區名稱>*' 中的記憶體不足」，該怎麼辦。 …” 前提是可用的記憶體足夠供執行作業。|
|[在 VM 環境中使用記憶體內部 OLTP 的最佳做法](#bkmk_VMs)|在虛擬環境中使用記憶體內部 OLTP 的注意事項。|
  
##  <a name="bkmk_resolveRecoveryFailures"></a> 解決由於 OOM 所造成的資料庫還原失敗  
 當您嘗試還原資料庫時，可能會收到錯誤訊息：「資料庫 '*\<資料庫名稱>*' 的還原作業因為資源集區 '*\<資源集區名稱>*' 中的記憶體不足而失敗」。這表示伺服器沒有足夠的可用記憶體來還原資料庫。 
   
您還原資料庫的目標伺服器針對資料庫備份的記憶體最佳化資料表必須有足夠的可用記憶體，否則資料庫將不會恢復連線，並會標記為可疑。  
  
如果伺服器確實有足夠的實體記憶體，但您仍發現此錯誤，可能是其他處理序使用太多記憶體，或組態問題導致沒有足夠的記憶體可供還原使用。 針對這類問題，請採取下列措施將更多記憶體提供給還原作業： 
  
-   暫時關閉執行中的應用程式。   
    透過關閉一個或多個執行中的應用程式或停止目前不需要的服務，就可以將這些應用程式或服務所使用的記憶體提供給還原作業。 您可以在成功還原之後重新啟動這些應用程式。  
  
-   提高 MAX_MEMORY_PERCENT 的值。   
    如果資料庫已 [繫結至資源集區](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)(這是最佳做法)，還原作業可用的記憶體是由 MAX_MEMORY_PERCENT 所管理。 如果此值太低，還原就會失敗。 這個程式碼片段會將資源集區 PoolHk 的 MAX_MEMORY_PERCENT 變更為已安裝記憶體的 70%。  
  
    > [!IMPORTANT]  
    > 如果伺服器是在 VM 上執行，而且不是專用的，請將 MIN_MEMORY_PERCENT 設成與 MAX_MEMORY_PERCENT 相同的值。   
    > 如需詳細資訊，請參閱[在 VM 環境中使用記憶體內部 OLTP 的最佳做法](#bkmk_VMs)主題。  
  
    ```sql  
    -- disable resource governor  
    ALTER RESOURCE GOVERNOR DISABLE  
  
    -- change the value of MAX_MEMORY_PERCENT  
    ALTER RESOURCE POOL PoolHk  
    WITH  
         ( MAX_MEMORY_PERCENT = 70 )  
    GO  
  
    -- reconfigure the Resource Governor  
    --    RECONFIGURE enables resource governor  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
  
    ```  
  
     如需 MAX_MEMORY_PERCENT 之最大值的資訊，請參閱主題章節： [可用於記憶體最佳化資料表和索引的記憶體百分比](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)。  
  
-   增加 **最大伺服器記憶體**。  
    如需設定**最大伺服器記憶體**的資訊，請參閱[伺服器記憶體伺服器設定選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。  
  
##  <a name="bkmk_recoverFromOOM"></a> 解決低記憶體或 OOM 狀況對於工作負載的影響  
 避免發生低記憶體或 OOM (記憶體不足) 的情況才是最上策。 良好的規劃和監視有助於避免 OOM 情況。 不過，最佳的規劃永遠無法預測實際發生的狀況，而最後可能會導致低記憶體或 OOM。 有兩個步驟可以從 OOM 中復原：  
  
1.  [開啟 DAC (專用管理員連接)](#bkmk_openDAC)  
  
2.  [採取更正動作](#bkmk_takeCorrectiveAction)  
  
###  <a name="bkmk_openDAC"></a> 開啟 DAC (專用管理員連接)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供專用管理員連接 (DAC)。 即使伺服器對其他用戶端連接沒有回應，系統管理員也可以使用 DAC 來存取 SQL Server Database Engine 的執行中執行個體，以針對伺服器上的問題進行疑難排解。 您可以透過 `sqlcmd` 公用程式與 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來存取 DAC。  
  
 如需透過 SSMS 或 `sqlcmd` 使用 DAC 的指導，請參閱[資料庫管理員的診斷連線](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。  
  
###  <a name="bkmk_takeCorrectiveAction"></a> 採取更正動作  
 若要解決 OOM 狀況，您必須透過降低使用量，釋出現有的記憶體，或是將更多記憶體提供給記憶體中的資料表。  
  
#### <a name="free-up-existing-memory"></a>釋出現有的記憶體  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>刪除非必要的記憶體最佳化資料表資料列並等候記憶體回收  
 您可以從記憶體最佳化資料表中移除非必要的資料列。 記憶體回收行程會將這些資料列所使用的記憶體傳回給可用的記憶體。 記憶體中 OLTP 引擎會積極地回收資料列佔用的記憶體。 不過，長時間執行的交易可能會防止記憶體回收。 例如，假設您的交易會執行 5 分鐘，則任何在交易作用期間由於更新/刪除作業而建立的資料列版本，都無法進行記憶體回收。  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>將一個或多個資料列移至磁碟資料表  
 下列 TechNet 文件提供了有關將記憶體最佳化資料表的資料列移至磁碟資料表的指引。  
  
-   [應用程式層級資料分割](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
  
-   [分割記憶體最佳化資料表的應用程式模式](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
#### <a name="increase-available-memory"></a>增加可用的記憶體  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>提高資源集區的 MAX_MEMORY_PERCENT 值  
 如果您尚未針對記憶體中的資料表建立具名資源集區，就應該先建立集區，並且將 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料庫繫結至該集區。 如需如何建立 [資料庫並繫結至資源集區的指引，請參閱](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) 將包含記憶體最佳化資料表的資料庫繫結至資源集區 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 主題。  
  
 如果您的 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料庫已繫結至資源集區，您應該能夠提高集區可存取的記憶體百分比。 如需變更資源集區之 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 值的指引，請參閱 [變更現有集區上的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) 子主題。  
  
 提高 MAX_MEMORY_PERCENT 的值。   
這個程式碼片段會將資源集區 PoolHk 的 MAX_MEMORY_PERCENT 變更為已安裝記憶體的 70%。  
  
> [!IMPORTANT]  
>  如果伺服器是在 VM 上執行，而且不是專用的，請將 MIN_MEMORY_PERCENT 與 MAX_MEMORY_PERCENT 設為相同值。   
> 如需詳細資訊，請參閱[在 VM 環境中使用記憶體內部 OLTP 的最佳做法](#bkmk_VMs)主題。  
  
```sql  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor to enabled it
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
 如需 MAX_MEMORY_PERCENT 之最大值的資訊，請參閱主題章節： [可用於記憶體最佳化資料表和索引的記憶體百分比](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)。  
  
##### <a name="install-additional-memory"></a>安裝額外記憶體  
 最佳的終極解決方案還是安裝額外的實體記憶體 (如果可行)。 如果您這樣做，請記住，因為 [不太可能需要更多記憶體，所以您或許能夠一併提高 MAX_MEMORY_PERCENT 的值 (請參閱](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)變更現有集區上的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 子主題)，以便將大部分新安裝的記憶體提供給資源集區。  
  
> [!IMPORTANT]  
>  如果伺服器是在 VM 上執行，而且不是專用的，請將 MIN_MEMORY_PERCENT 與 MAX_MEMORY_PERCENT 設為相同值。   
> 如需詳細資訊，請參閱[在 VM 環境中使用記憶體內部 OLTP 的最佳做法](#bkmk_VMs)主題。  
  
##  <a name="bkmk_PageAllocFailure"></a> 解決有足夠的記憶體可用但卻記憶體不足所造成的頁面配置失敗  
 若在可用的實體記憶體足以配置分頁時，於錯誤記錄檔中收到錯誤訊息 `Disallowing page allocations for database '*\<databaseName>*' due to insufficient memory in the resource pool '*\<resourcePoolName>*'. See 'http://go.microsoft.com/fwlink/?LinkId=330673' for more information.`，可能是因為停用 Resource Governor 所致。 若資源管理員已停用，MEMORYBROKER_FOR_RESERVE 會誘發不實的記憶體壓力。  
  
 為了解決此問題，您必須啟用資源管理員。  
  
 如需使用物件總管、資源管理員屬性或 Transact-SQL 來啟用資源管理員之限制事項的資訊和指引，請參閱 [啟用資源管理員](../../relational-databases/resource-governor/enable-resource-governor.md) 。  
 
## <a name="bkmk_VMs"></a> 在 VM 環境中使用記憶體內部 OLTP 的最佳做法
伺服器虛擬化技術可協助您降低 IT 資本和作業成本，並透過改善的應用程式佈建、維護、可用性和備份/復原程序，達到更高的 IT 效率。 隨著最近的技術進步，可以更輕易地運用虛擬化技術，將複雜的資料庫工作負載合併。 本主題涵蓋在虛擬化環境中使用 SQL Server 記憶體內部 OLTP 的最佳做法。

### <a name="memory-pre-allocation"></a>記憶體預先配置
對虛擬化環境中的記憶體而言，更好的效能與增強的支援是基本考量。 您必須能夠依據虛擬機器的需求 (尖峰和非尖峰負載)，快速配置記憶體給虛擬機器，同時也要確保不會浪費記憶體。 有關如何在主機上執行的虛擬機器之間配置和管理記憶體，Hyper-V 動態記憶體功能可以加強這方面的靈活度。

將具有記憶體最佳化資料表的資料庫進行虛擬化時，需要修改虛擬化及管理 SQL Server 的一些最佳做法。 如果沒有記憶體最佳化資料表，則其中兩個最佳作法如下：
-  如果您使用最小伺服器記憶體，最好只要指派所需的記憶體數量，這樣才能保留足夠的記憶體給其他處理序 (進而避免分頁)。
-  不要設定太高的記憶體預先配置值。 否則，其他程序可能會在需要時，無法得到足夠的記憶體，而導致記憶體分頁。

如果您為具有記憶體最佳化資料表的資料庫遵循上述作法，即使您有足夠的記憶體來還原資料庫，在嘗試還原和復原資料庫時，還是會導致資料庫陷入「復原暫止」狀態。 原因如下，在啟動時，記憶體內部 OLTP 將資料帶入記憶體的積極程度，遠勝於動態記憶體配置將記憶體配置給資料庫。

### <a name="resolution"></a>解決方案
若要緩和這個問題，請預先配置足夠的記憶體給資料庫，以復原或重新啟動資料庫，而不是提供最小值，依賴動態記憶體在需要時提供額外的記憶體。
  
## <a name="see-also"></a>另請參閱  
 [為記憶體中的 OLTP 管理記憶體](http://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)   
 [監視與疑難排解記憶體使用量](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)   
 [將包含記憶體最佳化資料表的資料庫繫結至資源集區](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [記憶體管理架構指南](../../relational-databases/memory-management-architecture-guide.md)  
 [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md) 
  
