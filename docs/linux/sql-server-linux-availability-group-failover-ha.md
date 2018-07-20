---
title: 管理可用性群組容錯移轉-在 Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e993478f3ae593c2829a9e2cf39d46527a909a77
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086090"
---
# <a name="always-on-availability-group-failover-on-linux"></a>在 Linux 上的 always On 可用性群組容錯移轉

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在可用性群組 (AG) 的內容中，主要角色和次要可用性複本的角色是在稱為容錯移轉的程序中通常可以互換。 容錯移轉共有三種形式，包括自動容錯移轉 (不會遺失資料)、規劃的手動容錯移轉 (不會遺失資料)，以及強制手動容錯移轉 (可能會遺失資料)，這種形式通常稱為「強制容錯移轉」。 自動及經過規劃的手動容錯移轉會保留您所有的資料。 AG 容錯移轉的可用性複本層級。 也就是 AG 容錯移轉到其中一個次要複本 （目前的容錯移轉目標）。 

如需容錯移轉的背景資訊，請參閱[容錯移轉和容錯移轉模式](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)。

## <a name="failover"></a>手動容錯移轉

您可以使用叢集管理工具來管理由外部叢集管理員 AG 容錯移轉。 比方說，如果方案使用 Pacemaker 管理 Linux 叢集，使用`pcs`RHEL 或 Ubuntu 上執行手動容錯移轉。 在 SLES 上使用`crm`。 

> [!IMPORTANT]
> 在一般操作下，就不會容錯使用 SSMS 或 PowerShell 等的 TRANSACT-SQL 或 SQL Server 管理工具。 當`CLUSTER_TYPE = EXTERNAL`，如 jedinou platnou hodnotu`FAILOVER_MODE`是`EXTERNAL`。 使用這些設定，所有的手動或自動容錯移轉動作會由外部叢集管理員執行。 若要強制可能遺失資料的容錯移轉的指示，請參閱[強制容錯移轉](#forceFailover)。

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">手動容錯移轉步驟

若要容錯移轉，將會成為主要複本的次要複本必須同步。 如果次要複本是非同步的[變更的可用性模式](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)。

手動容錯移轉以兩個步驟。

   首先，[依移動 AG 資源手動容錯移轉](#manualMove)從叢集節點擁有的資源至新的節點。

   叢集容錯移轉 AG 資源，並加入位置條件約束。 這個條件約束會設定要在新的節點上執行的資源。 若要成功進行容錯移轉在未來移除此條件約束。

   第二個，[移除位置條件約束](#removeLocConstraint)。

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">步驟 1。 依移動可用性群組資源手動容錯移轉

若要手動容錯移轉名為的 AG 資源*ag_cluster*到名為的叢集節點*nodeName2*，執行適當的命令，為您的散發：

- **RHEL/Ubuntu 範例**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 範例**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>手動容錯移轉資源之後，您需要移除位置條件約束會自動新增。

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> 步驟 2。 移除位置條件約束

手動容錯移轉期間，`pcs`命令`move`或是`crm`命令`migrate`加入新的目標節點上放置資源的位置條件約束。 若要查看新的條件約束，請在手動移動資源後執行下列命令：

- **RHEL/Ubuntu 範例**

   ```bash
   sudo pcs constraint list --full
   ```

- **SLES 範例**

   ```bash
   crm config show
   ```

取得建立由於手動容錯移轉的條件約束的範例。 
 `Enabled on: Node1 (score:INFINITY) (role: Master) (id:cli-prefer-ag_cluster-master)`

- **RHEL/Ubuntu 範例**

   在下列命令中，`cli-prefer-ag_cluster-master` 是需要移除的條件約束識別碼。 `sudo pcs constraint list --full` 會傳回此識別碼。 
   
   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
   
- **SLES 範例**

   在下列命令中`cli-prefer-ms-ag_cluster`是條件約束的識別碼。 `crm config show` 會傳回此識別碼。 
   
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

強制容錯移轉僅限用於災害復原。 在此情況下，您無法容錯移轉叢集管理工具因為主要資料中心已關閉。 如果您強制容錯移轉至非同步的次要複本，有些資料可能會遺失。 如果您必須立即還原服務至 AG，願意承擔遺失資料的風險，只強制容錯移轉。

如果叢集沒有回應，因為在主要資料中心發生災難事件時，您無法使用叢集管理工具與叢集-例如，互動，您可能必須強制容錯移轉，以略過外部叢集管理員。 此程序不會建議規則的作業，因為它有資料遺失的風險。 當叢集管理工具無法執行容錯移轉動作，請使用它。 在功能上，此程序大致[執行強制手動容錯移轉](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)在 Windows 中的 AG。
 
強制容錯移轉進行此程序是在 Linux 上的 SQL Server 特有的。

1. 請確認，AG 資源不由管理叢集了。 

      - 在目標叢集節點上，為未受管理的模式設定的資源。 此命令發出訊號停止資源監視和管理的資源代理程式。 例如： 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - 如果嘗試將資源模式設定為未受管理的模式失敗，請刪除資源。 例如：

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >當您刪除資源時，它也會刪除所有相關聯的條件約束。 

1. 在裝載次要複本的 SQL server 執行個體，將 工作階段內容變數`external_cluster`。

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. 將 AG 容錯移轉使用 Transact SQL。 在下列範例中，取代`<MyAg>`您 AG 的名稱。 連接到裝載目標次要複本的 SQL Server 執行個體，然後執行下列命令：

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  強制容錯移轉之後，將 AG 帶到狀況良好的狀態，然後再重新啟動的叢集資源監視和管理，或重新建立 AG 資源。 檢閱[強制容錯移轉後的重要工作](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp)。

1.  請重新啟動叢集資源監視與管理：

   若要重新啟動的叢集資源監視和管理，請執行下列命令：

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   如果您刪除叢集資源，請將它重新建立。 若要重新建立叢集資源，請遵循指示[建立可用性群組資源](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。

>[!Important]
>因為有資料遺失的風險，請勿針對災害復原演練，又使用上述的步驟。 變更為同步，非同步複本及其使用指示[標準的手動容錯移轉](#manualFailover)。

## <a name="database-level-monitoring-and-failover-trigger"></a>資料庫層級監視和容錯移轉觸發程序

針對`CLUSTER_TYPE=EXTERNAL`，容錯移轉觸發程序語意會不同於 WSFC。 WSFC 中的 SQL Server 的執行個體的 AG 時，轉換共`ONLINE`資料庫造成來報告錯誤的 AG 健全狀況狀態。 在回應中，「 叢集管理員會觸發容錯移轉動作。 在 Linux 上，SQL Server 執行個體無法與叢集通訊。 在完成資料庫健全狀況監視*外到內*。 如果使用者選擇在資料庫層級的容錯移轉的監視和容錯移轉 (藉由設定選項`DB_FAILOVER=ON`建立 AG 時)，叢集會檢查資料庫狀態是否`ONLINE`每次執行監視的動作。 叢集查詢中的狀態`sys.databases`。 不同於任何狀態`ONLINE`，自動 （如果符合自動容錯移轉條件），就會觸發容錯移轉。 實際的容錯移轉時間取決於監視的動作，以及在 sys.databases 中更新的資料庫狀態的頻率。

自動容錯移轉需要至少一個同步複本。

## <a name="next-steps"></a>後續步驟

[設定 SQL Server 可用性群組叢集資源的 Red Hat Enterprise Linux 叢集](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 可用性群組叢集資源設定 SUSE Linux Enterprise Server 叢集](sql-server-linux-availability-group-cluster-sles.md)

[設定 SQL Server 可用性群組叢集資源的 Ubuntu 叢集](sql-server-linux-availability-group-cluster-ubuntu.md)
