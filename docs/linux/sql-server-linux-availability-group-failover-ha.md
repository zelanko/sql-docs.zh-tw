---
title: 管理可用性群組容錯移轉 - Linux 上的 SQL Server
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: a13f9f3da00889323f3d971ffd801f1fa7d09890
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027226"
---
# <a name="always-on-availability-group-failover-on-linux"></a>Linux 上的 Always On 可用性群組容錯移轉

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在可用性群組 (AG) 的內容中，可用性複本主要角色和次要角色在稱為容錯移轉的程序中通常可以互換。 容錯移轉共有三種形式，包括自動容錯移轉 (不會遺失資料)、規劃的手動容錯移轉 (不會遺失資料)，以及強制手動容錯移轉 (可能會遺失資料)，這種形式通常稱為「強制容錯移轉」  。 自動及經過規劃的手動容錯移轉會保留所有資料。 AG 會在可用性複本層級容錯移轉。 亦即 AG 會容錯移轉至其中一個次要複本 (目前的容錯移轉目標)。 

如需容錯移轉的背景資訊，請參閱[容錯移轉與容錯移轉模式](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)。

## <a name="failover"></a>手動容錯移轉

使用叢集管理工具來容錯移轉外部叢集管理員所管理的 AG。 例如，如果解決方案使用 Pacemaker 來管理 Linux 叢集，則請使用 `pcs` 在 RHEL 或 Ubuntu 上執行手動容錯移轉。 在 SLES 中，請使用 `crm`。 

> [!IMPORTANT]
> 在正常作業下，請勿使用 Transact-SQL 或 SQL Server 管理工具 (例如 SSMS 或 PowerShell) 進行容錯移轉。 當 `CLUSTER_TYPE = EXTERNAL` 時，`FAILOVER_MODE` 的唯一可接受值為 `EXTERNAL`。 使用這些設定，所有手動或自動容錯移轉動作都會由外部叢集管理員執行。 如需可能遺失資料的強制容錯移轉指示，請參閱[強制容錯移轉](#forceFailover)。

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">手動容錯移轉步驟

若要進行容錯移轉，將成為主要複本的次要複本必須是同步的。 如果次要複本為非同步，請[變更可用性模式](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)。

以兩個步驟進行手動容錯移轉。

   首先，將 AG 資源從擁有資源的叢集節點移至新節點，以進行[手動容錯移轉](#manualMove)。

   叢集會為 AG 資源進行容錯移轉並新增位置條件約束。 此條件約束會將資源設定為在新的節點上執行。 請移除此條件約束，以便在未來成功進行容錯移轉。

   其次，[移除位置條件約束](#removeLocConstraint)。

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove"> 步驟 1. 移動可用性群組資源來手動容錯移轉

若要手動將名為 *ag_cluster* 的 AG 資源容錯移轉至名為 *nodeName2* 的叢集節點，請針對您的發行版本執行適用命令：

- **RHEL/Ubuntu 範例**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 範例**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>在您手動為資源進行容錯移轉後，您需要移除自動新增的位置條件約束。

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> 步驟 2. 移除位置條件約束

在手動容錯移轉期間，`pcs` 命令 `move` 或 `crm` 命令 `migrate` 會針對要放置在新目標節點上的資源新增位置條件約束。 若要查看新的條件約束，請在手動移動資源後執行下列命令：

- **RHEL/Ubuntu 範例**

   ```bash
   sudo pcs constraint list --full
   ```

- **SLES 範例**

   ```bash
   crm config show
   ```

因手動容錯移轉而建立的條件約束範例。 
 `Enabled on: Node1 (score:INFINITY) (role: Master) (id:cli-prefer-ag_cluster-master)`

- **RHEL/Ubuntu 範例**

   在下列命令中，`cli-prefer-ag_cluster-master` 是需要移除的條件約束識別碼。 `sudo pcs constraint list --full` 會傳回此識別碼。 
   
   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
   
- **SLES 範例**

   在下列命令中，`cli-prefer-ms-ag_cluster` 是條件約束的識別碼。 `crm config show` 會傳回此識別碼。 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>自動容錯移轉不會加入位置條件約束，因此不需要清除。 

如需詳細資訊：
- [Red Hat：管理叢集資源 (英文)](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [acemaker - Move Resources Manually](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/_manually_moving_resources_around_the_cluster.html) (Pacemaker - 手動移動資源)
 [SLES Administration Guide - Resources](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) (SLES 管理指南 - 資源) 
 
## <a name="forceFailover"></a> 強制容錯移轉 

強制容錯移轉主要用於災害復原。 在此情況下，因為主要資料中心已關閉，所以您無法使用叢集管理工具進行容錯移轉。 如果您強制容錯移轉至非同步的次要複本，有些資料可能會遺失。 只有在您必須立即還原 AG 的服務且願意承擔遺失資料的風險時，才強制執行容錯移轉。

如果您無法使用叢集管理工具與叢集進行互動 (例如，如果叢集由於主要資料中心發生嚴重損壞事件而沒有回應)，您可能必須強制容錯移轉以略過外部叢集管理員。 不建議將此程序用於一般作業，因為它會有造成資料遺失的風險。 當叢集管理工具無法執行容錯移轉動作時，請使用此程序。 在功能上，此程序類似於在 Windows 的 AG 上[執行強制手動容錯移轉](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)。
 
此強制容錯移轉處理序特定於 Linux 上的 SQL Server。

1. 確認 AG 資源不再由叢集所管理。 

      - 在目標叢集節點上將資源設定為非受控模式。 此命令會指示資源代理程式停止資源監視和管理。 例如： 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - 如果嘗試將資源模式設定為非受控模式失敗，請刪除該資源。 例如：

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >當您刪除資源時，它也會刪除所有相關聯的條件約束。 

1. 在裝載次要複本的 SQL Server 執行個體上設定工作階段內容變數 `external_cluster`。

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. 使用 Transact-SQL 為 AG 進行容錯移轉。 在下列範例中，以您的 AG 名稱取代 `<MyAg>`。 連線到裝載目標次要複本的 SQL Server 執行個體，並執行下列命令：

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  在強制容錯移轉之後，請先讓 AG 恢復健康狀態，再重新啟動叢集資源監視和管理，或重建 AG 資源。 請檢閱[強制容錯移轉後的重要工作](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp)。

1.  重新啟動叢集資源監視和管理：

   若要重新啟動叢集資源監視和管理，請執行下列命令：

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   如果您刪除了叢集資源，請予以重新建立。 若要重新建立叢集資源，請遵循[建立可用性群組資源](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)中的指示。

>[!Important]
>請不要將上述步驟用於災害復原演練，因為其可能會有造成資料遺失的風險。 而是將非同步複本變更為同步，並遵循[一般手動容錯移轉](#manualFailover)的指示。

## <a name="database-level-monitoring-and-failover-trigger"></a>資料庫層級監視和容錯移轉觸發程序

針對 `CLUSTER_TYPE=EXTERNAL`，相較於 WSFC，容錯移轉觸發程序的語意會不同。 當 AG 位於 WSFC 的 SQL Server 執行個體上時，從資料庫的 `ONLINE` 狀態轉換會導致 AG 健康狀態回報錯誤。 為了回應，叢集管理員會觸發容錯移轉動作。 在 Linux 上，SQL Server 執行個體無法與叢集通訊。 監視資料庫健康狀態的作業是「由外而內」  進行。 如果使用者選擇進行資料庫層級的容錯移轉監視和容錯移轉 (透過在建立 AG 時設定 `DB_FAILOVER=ON` 選項)，叢集會在每次執行監視動作時，檢查資料庫狀態是否為 `ONLINE`。 叢集會查詢 `sys.databases` 中的狀態。 針對不同於 `ONLINE` 的狀態，它會自動觸發容錯移轉 (如果符合自動容錯移轉條件的話)。 容錯移轉實際時間取決於監視動作的頻率，以及 sys.databases 中所更新的資料庫狀態。

自動容錯移轉需要至少一個同步複本。

## <a name="next-steps"></a>後續步驟

[設定 SQL Server 可用性群組叢集資源的 Red Hat Enterprise Linux 叢集](sql-server-linux-availability-group-cluster-rhel.md)

[設定 SQL Server 可用性群組叢集資源的 SUSE Linux Enterprise Server 叢集](sql-server-linux-availability-group-cluster-sles.md)

[設定 SQL Server 可用性群組叢集資源的 Ubuntu 叢集](sql-server-linux-availability-group-cluster-ubuntu.md)
