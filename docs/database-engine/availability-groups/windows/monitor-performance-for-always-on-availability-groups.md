---
title: 監視 Always On 可用性群組的效能 (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dfd2b639-8fd4-4cb9-b134-768a3898f9e6
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6ad77dc80e9c54dffba133e06428dca24f2f704b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="monitor-performance-for-always-on-availability-groups"></a>監視 Always On 可用性群組的效能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Always On 可用性群組的效能層面，對於維護關鍵任務資料庫的服務等級協定 (SLA) 來說非常重要。 了解可用性群組如何將記錄傳送至次要複本，可協助您 預估可用性實作的復原時間目標 (RTO) 與復原點目標 (RPO)，以及針對效能不佳的可用性群組或複本來識別其中的瓶頸。 本文章會說明同步處理程序，示範如何計算一些關鍵計量，並提供某些常見效能疑難排解案例的連結。  
  
 其中涵蓋下列主題：  
  
-   [資料同步處理程序](#BKMK_DATA_SYNC_PROCESS)  
  
-   [流程控制閘道](#BKMK_FLOW_CONTROL_GATES)  
  
-   [預估容錯移轉時間 (RTO)](#BKMK_RTO)  
  
-   [預估潛在資料遺失 (RPO)](#BKMK_RPO)  
  
-   [監視 RTO 和 RPO](#BKMK_Monitoring_for_RTO_and_RPO)  
  
-   [效能疑難排解案例](#BKMK_SCENARIOS)  
  
-   [實用的擴充事件](#BKMK_XEVENTS)  
  
##  <a name="BKMK_DATA_SYNC_PROCESS"></a> 資料同步處理程序  
 若要預估完整同步處理的時間並找出瓶頸，您需要了解同步處理程序。 效能瓶頸可能會在程序中的任何位置，而找出瓶頸可以協助您挖掘更深入的底層問題。 下圖和下表說明資料同步處理程序：  
  
 ![可用性群組資料同步處理](media/always-onag-datasynchronization.gif "可用性群組資料同步處理")  
  
|||||  
|-|-|-|-|  
|**序列**|**步驟描述**|**註解**|**實用的計量**|  
|@shouldalert|記錄檔產生|記錄檔資料會排清至磁碟。 此記錄檔必須複寫到次要複本。 記錄檔記錄會進入傳送佇列。|[SQL Server:Database > Log bytes flushed\sec](~/relational-databases/performance-monitor/sql-server-databases-object.md)|  
|2|擷取|這會擷取每個資料庫的記錄檔並傳送至對應的夥伴佇列 (每個資料庫複本組一個)。 只要已連接可用性複本且資料移動未因任何原因暫停，此擷取程序就會持續執行，且資料庫複本組會顯示為「同步處理中」或「已同步處理」兩者之一。 如果擷取程序掃描訊息並將它加入佇列的速度不夠快，則會建立記錄檔傳送佇列。|[SQL Server:Availability Replica > Bytes Sent to Replica\sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md)，這是針對該可用性複本排入佇列的所有資料庫訊息總和彙總。<br /><br /> 主要複本上為 [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB) 和 [log_bytes_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB/秒)。|  
|3|Send|這會清除每個資料庫複本佇列中的訊息佇列，並跨線路傳送到個別的次要複本。|[SQL Server:Availability Replica > Bytes sent to transport\sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md) 和 [SQL Server:Availability Replica > Message Acknowledgement Time](~/relational-databases/performance-monitor/sql-server-availability-replica.md) (毫秒)|  
|4|接收並快取|每個次要複本會接收並快取訊息。|效能計數器 [SQL Server:Availability Replica > Log Bytes Received/sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|5|強行寫入|這會排清次要複本上的記錄檔，以進行強行寫入。 記錄檔排清之後，會將認可傳回到主要複本。<br /><br /> 一旦強行寫入記錄檔，可以避免資料遺失。|效能計數器 [SQL Server:Database > Log Bytes Flushed/sec](~/relational-databases/performance-monitor/sql-server-databases-object.md)<br /><br /> 等候類型 [HADR_LOGCAPTURE_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
|6|取消復原|在次要複本上重做排清的分頁。 頁面等候重做時會保留在重做佇列中。|[SQL Server:Database Replica > Redone Bytes/sec](~/relational-databases/performance-monitor/sql-server-database-replica.md)<br /><br /> [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB) 和 [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)。<br /><br /> 等候類型 [REDO_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
  
##  <a name="BKMK_FLOW_CONTROL_GATES"></a> 流程控制閘道  
 可用性群組是以主要複本上的流程控制閘道設計，以避免所有可用性複本上過多的資源耗用，例如網路和記憶體資源。 這些流程控制閘道不會影響可用性複本的同步處理健康情況狀態，但它們可能會影響您的可用性資料庫 (包括 RPO) 的整體效能。  
  
 在主要複本上擷取記錄檔後，記錄檔會受限於兩個層級的流程控制，如下表所示。  
  
|||||  
|-|-|-|-|  
|**Level**|**閘道數目**|**訊息數目**|**實用的計量**|  
|傳輸|每個可用性複本 1 個|8192|擴充事件 **database_transport_flow_control_action**|  
|[資料庫]|每個可用性資料庫 1 個|11200 (x64)<br /><br /> 1600 (x86)|[DBMIRROR_SEND](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)<br /><br /> 擴充事件 **hadron_database_flow_control_action**|  
  
 一旦達到其中一個閘道的訊息閾值，記錄檔訊息便不會再傳送至特定複本，或是針對特定資料庫傳送。 一旦收到傳送訊息的訊息收條，就可以傳送訊息，讓傳送訊息數目低於閾值。  
  
 除了流程控制閘道以外，還有另外一個防止傳送記錄檔訊息的因素。 複本的同步處理可確保訊息會以記錄序號 (LSN) 的順序傳送並套用。 在傳送記錄檔訊息之前，也會針對最低認可 LSN 編號檢查其 LSN，以確定它小於其中一個閾值 (根據訊息類型而定)。 如果兩個 LSN 編號之間的間距大於閾值，則不會傳送訊息。 一旦間距再次低於閾值，則會傳送訊息。  
  
 兩個實用的效能計數器 [SQL Server:Availability Replica > Flow control/sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md) 和 [SQL Server:Availability Replica > Flow Control Time (毫秒/秒)](~/relational-databases/performance-monitor/sql-server-availability-replica.md)，會為您顯示上一秒內已啟動多少次流程控制，以及花費多少時間等候流程控制。 較高的流程控制等候時間會轉譯為較高的 RPO。 針對可能造成較高流程控制等候時間的問題，如需問題類型的詳細資訊，請參閱[疑難排解：可用性群組超過 RPO](troubleshoot-availability-group-exceeded-rpo.md).  
  
##  <a name="BKMK_RTO"></a> 預估容錯移轉時間 (RTO)  
 您 SLA 中的 RTO 會取決於您的 Always On 實作在任何給定時間的容錯移轉時間，可以用下列公式表示：  
  
 ![可用性群組 RTO 計算](media/always-on-rto.gif "可用性群組 RTO 計算")  
  
> [!IMPORTANT]  
>  如果可用性群組包含多個可用性資料庫，則包含最高 Tfailover 的可用性資料庫會變成 RTO 合規性的限制值。  
  
 失敗偵測時間 Tdetection 是系統用來偵測失敗的時間。 此時間取決於叢集層級設定，而不是個別可用性複本。 根據已設定的自動容錯移轉條件，則可能會觸發容錯移轉作為關鍵 SQL Server 內部錯誤的立即回應，例如孤立執行緒同步鎖定。 在此情況下，偵測可以和 [sp_server_diagnostics &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 錯誤報告傳送至 WSFC 叢集同樣快速 (預設間隔為健康情況檢查逾時的 1/3)。 容錯移轉也可因為逾時而觸發，例如叢集健康情況檢查逾時已過期 (預設為 30 秒) 或資源 DLL 和 SQL Server 執行個體之間的租用已過期 (預設為 20 秒)。 在此情況下，偵測時間與逾時間隔長度相同。 如需詳細資訊，請參閱[可用性群組自動容錯移轉的彈性容錯移轉原則 &#40;SQL Server&#41;](https://msdn.microsoft.com/library/hh710061(SQL.120).aspx)。  
  
 次要複本為了準備好進行容錯移轉而必須做的一件事，就是讓重做趕上記錄檔的結尾。 重做時間 Tredo 是使用下列公式計算的：  
  
 ![可用性群組重做時間計算](media/always-on-redo.gif "可用性群組重做時間計算")  
  
 其中 *redo_queue* 是 [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 中的值，而 *redo_rate* 是 [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 中的值。  
  
 容錯移轉負擔時間 Toverhead 包含系統用來容錯移轉 WSFC 叢集，並讓資料庫上線的時間。 此時間通常簡短且一致。  
  
##  <a name="BKMK_RPO"></a> 預估潛在資料遺失 (RPO)  
 您 SLA 中的 RPO 取決於您的 Always On 實作在任何給定時間的潛在資料遺失。 這個可能的資料遺失可以用下列公式來表示：  
  
 ![可用性群組 RPO 計算](media/always-on-rpo.gif "可用性群組 RPO 計算")  
  
 其中 *log_send_queue* 是 [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 的值，而*記錄檔產生速率*是 [SQL Server:Database > Log Bytes Flushed/sec](~/relational-databases/performance-monitor/sql-server-databases-object.md) 的值。  
  
> [!WARNING]  
>  如果可用性群組包含多個可用性資料庫，則包含最高 Tdata_loss 的可用性資料庫會變成 RPO 合規性的限制值。  
  
 記錄檔傳送佇列表示可能會從從重大失敗遺失的所有資料。 使用記錄檔產生速率而非記錄檔傳送速率，第一眼看起來不尋常 (請參閱 [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md))。 不過，請記住，使用記錄檔傳送速率僅能提供您同步處理的時間，而 RPO 會根據資料產生的速度 (而非同步處理資料的速度) 來測量資料遺失。  
  
 預估 Tdata_loss 更簡單的方式是使用 [last_commit_time](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)。 在主要複本上的 DMV 會針對所有複本回報此值。 您可以計算主要複本的值和次要複本的值之間的差異，以預估次要複本上的記錄檔趕上主要複本的速度。 如先前所述，這個計算不會根據記錄檔產生的速度告訴您潛在的資料遺失，但應為近似值。  
  
##  <a name="BKMK_Monitoring_for_RTO_and_RPO"></a> 監視 RTO and RPO  
 本節示範如何監視 RTO 和 RPO 計量的可用性群組。 此示範類似 [Always On 健康情況模型，第 2 部分：擴充健康情況模型](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)中提供的 GUI 教學課程。  
  
 [預估容錯移轉時間 (RTO)](#BKMK_RTO) 和[預估潛在資料遺失 (RPO)](#BKMK_RPO) 中容錯移轉時間和潛在資料遺失的元素，會提供為原則管理 Facet **資料庫複本狀態**中便利的效能計量 (請參閱[檢閱 SQL Server 物件的原則式管理 Facet](~/relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md))。 您可以依排程監視這兩個計量，並在計量分別超過您的 RTO 和 RPO 時收到警示。  
  
 示範指令碼會建立依照其個別排程執行的兩個系統原則，具有下列特性：  
  
-   當預估的容錯移轉時間超過 10 分鐘 (每 5 分鐘進行評估) 時會失敗的 RTO 原則  
  
-   當預估的資料遺失超過 1 小時 (每 30 分鐘進行評估) 時會失敗的 RPO 原則  
  
-   這兩個原則在所有可用性複本上具有相同的設定  
  
-   原則會在所有的伺服器上評估，但僅限於本機可用性複本為主要複本的可用性群組上。 如果本機可用性複本不是主要複本，則不會評估原則。  
  
-   當您在主要複本上檢視原則失敗時，它會顯示在 Always On 儀表板中。  

若要建立原則，請在參與可用性群組的所有伺服器執行個體上依照下列指示執行：  

1.  [啟動 SQL Server Agent 服務](~/ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md) (如果尚未啟動)。  
  
2.  在 SQL Server Management Studio 中，在 [工具] 功能表中，按一下 [選項]。  
  
3.  在 [SQL Server Always On] 索引標籤中，選取 [啟用使用者定義 Always On 原則] 並按一下 [確定]。  
  
     此設定可讓您在 Always On 儀表板中顯示已正確設定的自訂原則。  
  
4.  使用下列規格建立[以原則為基礎的管理條件](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md)：  
  
    -   **名稱**：`RTO`  
  
    -   **Facet**：**資料庫複本狀態**  
  
    -   **欄位**：`Add(@EstimatedRecoveryTime, 60)`  
  
    -   **運算子**：**<=**  
  
    -   **值**：`600`  
  
     當潛在容錯移轉時間超過 10 分鐘 (包括失敗偵測和容錯移轉的 60 秒額外負荷)，此條件會失敗。  
  
5.  使用下列規格建立第二個[以原則為基礎的管理條件](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md)：  
  
    -   **名稱**：`RPO`  
  
    -   **Facet**：**資料庫複本狀態**  
  
    -   **欄位**：`@EstimatedDataLoss`  
  
    -   **運算子**：**<=**  
  
    -   **值**：`3600`  
  
     當潛在資料遺失超過 1 小時時，此條件會失敗。  
  
6.  使用下列規格建立第三個[以原則為基礎的管理條件](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md)：  
  
    -   **名稱**：`IsPrimaryReplica`  
  
    -   **Facet**：**可用性群組**  
  
    -   **欄位**：`@LocalReplicaRole`  
  
    -   **運算子**：**=**  
  
    -   **值**：`Primary`  
  
     此條件會檢查給定可用性群組的本機可用性複本是否為主要複本。  
  
7.  使用下列規格建立[以原則為基礎的管理原則](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md)：  
  
    -   [一般] 頁面：  
  
        -   **名稱**：`CustomSecondaryDatabaseRTO`  
  
        -   **檢查條件**：`RTO`  
  
        -   **針對目標**：**IsPrimaryReplica AvailabilityGroup** 中的**每個 DatabaseReplicaState**  
  
             此設定可確保原則僅於本機可用性複本為主要複本的可用性群組上評估。  
  
        -   **評估模式**：**按排程時間**  
  
        -   **排程**：**CollectorSchedule_Every_5min**  
  
        -   **已啟用**：**選取**  
  
    -   [描述] 頁面：  
  
        -   **類別**：**可用性資料庫警告**  
  
             此設定可讓原則評估結果在 Always On 儀表板中顯示。  
  
        -   **描述**：**目前的複本擁有已超過 10 分鐘的 RTO，假設 1 分鐘的額外負荷進行探索及容錯移轉。您應該立即調查個別的伺服器執行個體上的效能問題。**  
  
        -   **要顯示的文字**：**已超過 RTO！**  
  
8.  使用下列規格建立第二個[以原則為基礎的管理原則](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md)：  
  
    -   [一般] 頁面：  
  
        -   **名稱**：`CustomAvailabilityDatabaseRPO`  
  
        -   **檢查條件**：`RPO`  
  
        -   **針對目標**：**IsPrimaryReplica AvailabilityGroup** 中的**每個 DatabaseReplicaState**  
  
        -   **評估模式**：**按排程時間**  
  
        -   **排程**：**CollectorSchedule_Every_30min**  
  
        -   **已啟用**：**選取**  
  
    -   [描述] 頁面：  
  
        -   **類別**：**可用性資料庫警告**  
  
        -   **描述**：**可用性資料庫已超過您的 1 小時 RPO。您應該立即調查可用性複本上的效能問題。**  
  
        -   **要顯示的文字**：**已超過 RPO！**  
  
 當您完成時，會分別針對每個原則評估排程建立兩個新的 SQL Server Agent 作業。 這些作業的名稱開頭應該為 **syspolicy_check_schedule**。  
  
 您可以檢視作業記錄以檢查評估結果。 評估失敗也會記錄在事件識別碼為 34052 的 Windows 應用程式記錄檔中 (位於 [事件檢視器])。 您也可以設定 SQL Server Agent 在原則失敗時傳送警示。 如需詳細資訊，請參閱[設定警示，在原則失敗時通知原則系統管理員](~/relational-databases/policy-based-management/configure-alerts-to-notify-policy-administrators-of-policy-failures.md)。  
  
##  <a name="BKMK_SCENARIOS"></a> 效能疑難排解案例  
 下表列出常見的效能相關疑難排解案例。  
  
|狀況|描述|  
|--------------|-----------------|  
|[偵錯：可用性群組超過 RTO](troubleshoot-availability-group-exceeded-rto.md)|在自動容錯移轉或規劃的手動容錯移轉之後若未遺失資料，容錯移轉時間會超過您的 RTO。 或者，當您評估同步認可次要複本 (例如自動容錯移轉夥伴) 的容錯移轉時間時，發現它超過您的 RTO。|  
|[偵錯：可用性群組超過 RPO](troubleshoot-availability-group-exceeded-rpo.md)|在您執行強制手動容錯移轉之後，遺失的資料超過您的 RPO。 或者，當您計算非同步認可次要複本的潛在資料遺失時，發現它超過您的 RPO。|  
|[疑難排解：對主要複本的變更未反映在次要複本上](troubleshoot-primary-changes-not-reflected-on-secondary.md)|用戶端應用程式在主要複本上成功完成更新，但是查詢次要複本卻顯示未反映變更。|  
  
##  <a name="BKMK_XEVENTS"></a> 實用的擴充事件  
 當針對**同步處理中**狀態的複本進行疑難排解時，下列擴充事件很有用。  
  
|事件名稱|類別目錄|通路|可用性複本|  
|----------------|--------------|-------------|--------------------------|  
|redo_caught_up|交易|偵錯|次要|  
|redo_worker_entry|交易|偵錯|次要|  
|hadr_transport_dump_message|`alwayson`|偵錯|Primary|  
|hadr_worker_pool_task|`alwayson`|偵錯|Primary|  
|hadr_dump_primary_progress|`alwayson`|偵錯|Primary|  
|hadr_dump_log_progress|`alwayson`|偵錯|Primary|  
|hadr_undo_of_redo_log_scan|`alwayson`|分析|次要|  
  
  