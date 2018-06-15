---
title: 管理可用性群組容錯移轉的 SQL Server on Linux |Microsoft 文件
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: ddbe5f25cf3153b3354425fd426798e7061bdf36
ms.sourcegitcommit: 99e355b71ff2554782f6bc8e0da86e6d9e3e0bef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34799808"
---
# <a name="always-on-availability-group-failover-on-linux"></a>在 Linux 上的 alwayson 可用性群組容錯移轉

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在可用性群組 (AG) 的內容中，主要角色和次要可用性複本的角色是通常稱為 「 容錯移轉的程序交換。 容錯移轉共有三種形式，包括自動容錯移轉 (不會遺失資料)、規劃的手動容錯移轉 (不會遺失資料)，以及強制手動容錯移轉 (可能會遺失資料)，這種形式通常稱為「強制容錯移轉」。 自動及經過規劃的手動容錯移轉會保留您所有的資料。 AG 容錯移轉的可用性複本層級。 也就是說，AG 容錯移轉至其中一個次要複本 （目前的容錯移轉目標）。 

如需容錯移轉的背景資訊，請參閱[容錯移轉和容錯移轉模式](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)。

## <a name="failover"></a>手動容錯移轉

使用容錯移轉 AG 外部叢集 manager 所管理的叢集管理工具。 例如，如果方案使用 Pacemaker 來管理 Linux 叢集，請使用`pcs`RHEL 或 Ubuntu 上執行手動容錯移轉。 SLES 上使用`crm`。 

> [!IMPORTANT]
> 在一般操作下，就不會容錯使用 TRANSACT-SQL 或 SQL Server 管理工具，例如 SSMS 或 PowerShell。 當`CLUSTER_TYPE = EXTERNAL`，只可接受的值為`FAILOVER_MODE`是`EXTERNAL`。 這些設定，外部叢集管理員執行所有的手動或自動容錯移轉動作。 若要強制容錯移轉可能遺失資料的指示，請參閱[強制容錯移轉](#forceFailover)。

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">手動容錯移轉步驟

若要容錯移轉，將會變成主要複本的次要複本必須同步。 如果次要複本是非同步，[變更可用性模式](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)。

手動容錯移轉以兩個步驟。

   首先，[手動容錯移轉移動 AG 資源](#manualMove)從叢集節點擁有的資源至新的節點。

   AG 資源容錯移轉叢集，並將位置限制式加入。 這個條件約束會設定要在新的節點上執行的資源。 移除此條件約束，才能成功進行容錯移轉在未來。

   第二個，[移除位置限制式](#removeLocConstraint)。

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">步驟 1。 手動容錯移轉將可用性群組資源

手動容錯移轉名為的 AG 資源*ag_cluster*至名為的叢集節點*nodeName2*，執行您的散發的適當命令：

- **RHEL/Ubuntu 範例**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 範例**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>手動容錯移轉的資源之後，您需要移除位置限制式，會自動加入。

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> 步驟 2。 移除位置條件約束

在手動容錯移轉，`pcs`命令`move`或`crm`命令`migrate`將放置在新的目標節點上資源的位置限制式加入。 若要查看新的條件約束，請在手動移動資源後執行下列命令：

- **RHEL/Ubuntu 範例**

   ```bash
   sudo pcs constraint list --full
   ```

- **SLES 範例**

   ```bash
   crm config show
   ```

取得建立的手動容錯移轉由於條件約束的範例。 
 `Enabled on: Node1 (score:INFINITY) (role: Master) (id:cli-prefer-ag_cluster-master)`

- **RHEL/Ubuntu 範例**

   在下列命令中，`cli-prefer-ag_cluster-master` 是需要移除的條件約束識別碼。 `sudo pcs constraint list --full` 會傳回此識別碼。 
   
   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
   
- **SLES 範例**

   下列命令`cli-prefer-ms-ag_cluster`是條件約束的識別碼。 `crm config show` 會傳回此識別碼。 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>自動容錯移轉不會加入位置條件約束，因此不需要清除。 

如需詳細資訊：
- [Red Hat：管理叢集資源 (英文)](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [Pacemaker-手動移動資源](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-pcs/html/Clusters_from_Scratch/_move_resources_manually.html)
 [SLES 系統管理指南-資源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 
## <a name="forceFailover"></a> 強制容錯移轉 

強制容錯移轉僅限用於災害復原。 在此情況下，您無法容錯移轉叢集管理工具因為主要資料中心已關閉。 如果您強制容錯移轉至非同步的次要複本，有些資料可能會遺失。 如果您必須立即還原服務 AG，並且願意承擔遺失資料的風險，只強制容錯移轉。

如果您無法使用叢集管理工具與叢集-例如，互動，如果叢集沒有回應，因為發生災害事件中主要資料中心，您可能必須強制容錯移轉，以略過外部叢集管理員。 此程序不會建議每天的作業，因為它風險資料遺失。 當叢集管理工具無法執行容錯移轉動作，請使用它。 在功能上，此程序是類似於[執行強制手動容錯移轉](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)上 Windows 中的 AG。
 
這個程序所強制容錯移轉是特定 SQL Server on Linux。

1. 請確認，AG 資源不由管理叢集了。 

      - 設定為未受管理的模式的資源目標叢集節點上。 此命令會發出訊號資源代理程式停止資源監視及管理。 例如： 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - 如果將資源模式設定未受管理的模式嘗試失敗，請刪除資源。 例如：

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >當您刪除資源時，它也會刪除所有相關聯的條件約束。 

1. 在裝載次要複本的 SQL server 執行個體，設定工作階段內容變數`external_cluster`。

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. 容錯移轉利用 TRANSACT-SQL AG。 在下列範例中，取代`<MyAg>`您 AG 名稱。 連接到裝載目標次要複本的 SQL Server 執行個體，並執行下列命令：

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  強制容錯移轉之後，狀況良好的狀態之前重新啟動的叢集資源監視和管理或重新建立 AG 資源將 AG。 檢閱[強制容錯移轉後的重要工作](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp)。

1.  請重新啟動叢集資源監視與管理：

   若要重新啟動的叢集資源監視和管理，請執行下列命令：

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   如果您刪除叢集資源，請將它重新建立。 若要重新建立叢集資源，請遵循指示[建立可用性群組資源](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。

>[!Important]
>請勿使用上述步驟的災害復原演練，因為有資料遺失的風險。 改為變更同步的非同步複本，而指示[正常的手動容錯移轉](#manualFailover)。

## <a name="database-level-monitoring-and-failover-trigger"></a>資料庫層級監視和容錯移轉觸發程序

如`CLUSTER_TYPE=EXTERNAL`，容錯移轉觸發程序語意不相同相較於 WSFC。 在 WSFC 中的 SQL Server 執行個體上 AG 時，轉換出`ONLINE`狀態的資料庫會導致 AG 健全狀況報告錯誤。 在回應時，叢集管理員 會觸發容錯移轉動作。 在 Linux 上的 SQL Server 執行個體無法與叢集通訊。 監視資料庫健全狀況*外部中*。 如果使用者已選擇在資料庫層級的容錯移轉的監視和容錯移轉 (藉由設定選項`DB_FAILOVER=ON`建立 AG 時)，叢集會檢查資料庫狀態是否為`ONLINE`每次執行監視的動作。 在叢集中的查詢中的狀態`sys.databases`。 不同於任何狀態`ONLINE`，自動 （如果符合自動容錯移轉條件），它將會觸發容錯移轉。 實際的容錯移轉時間取決於監視的動作，以及正在更新 sys.databases 中的資料庫狀態的頻率。

自動容錯移轉需要至少一個同步複本。

## <a name="next-steps"></a>後續的步驟

[設定 SQL Server 可用性群組的叢集資源的 Red Hat Enterprise Linux 叢集](sql-server-linux-availability-group-cluster-rhel.md)

[設定 SQL Server 可用性群組的叢集資源的 SUSE Linux Enterprise Server 叢集](sql-server-linux-availability-group-cluster-sles.md)

[Ubuntu Server 可用性群組的叢集資源的叢集設定](sql-server-linux-availability-group-cluster-ubuntu.md)
