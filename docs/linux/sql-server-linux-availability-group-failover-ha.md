---
title: "操作可用性群組的 SQL Server on Linux |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 07/20/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 07a50a59c320d7abb58c725c717393f8751b337d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="operate-ha-availability-group-for-sql-server-on-linux"></a>SQL Server on Linux 會操作 HA 可用性群組

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

## <a name="failover"></a>可用性群組容錯移轉

用於外部叢集 manager 所管理可用性群組容錯移轉叢集管理工具。 例如，如果方案使用 Pacemaker 來管理 Linux 叢集，請使用`pcs`RHEL 或 Ubuntu 上執行手動容錯移轉。 SLES 上使用`crm`。 

> [!IMPORTANT]
> 在一般操作下，就不會容錯使用 TRANSACT-SQL 或 SQL Server 管理工具，例如 SSMS 或 PowerShell。 當`CLUSTER_TYPE = EXTERNAL`，只可接受的值為`FAILOVER_MODE`是`EXTERNAL`。 這些設定，外部叢集管理員執行所有的手動或自動容錯移轉動作。 

### <a name="manual-failover-examples"></a>手動容錯移轉範例

手動容錯移轉之可用性群組的外部叢集管理工具。 在一般操作下，不會起始與 TRANSACT-SQL 的容錯移轉。 如果未回應的外部叢集管理工具，您可以強制可用性群組容錯移轉。 若要強制手動容錯移轉的指示，請參閱[手動移動時則無法回應叢集工具](#forceManual)。

完成手動容錯移轉，兩個步驟。 

1. 從叢集節點擁有的資源至新的節點移動可用性群組資源。

   叢集管理員 會將可用性群組資源移動，並將位置限制式。 這個條件約束會設定要在新的節點上執行的資源。 您必須移除此條件約束，才能移動是手動或自動容錯移轉在未來。

2. 移除位置限制式。

#### <a name="1-manually-fail-over"></a>1.手動容錯移轉

手動容錯移轉可用性群組資源名為*ag_cluster*至名為的叢集節點*nodeName2*，執行適當您散發的命令：

- **RHEL/Ubuntu 範例**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 範例**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```



>[!IMPORTANT]
>手動容錯移轉的資源之後，您需要移除在移動期間會自動加入的位置條件約束。

#### <a name="2-remove-the-location-constraint"></a>2.移除位置條件約束

在手動移動，`pcs`命令`move`或`crm`命令`migrate`將放置在新的目標節點上資源的位置限制式加入。 若要查看新的條件約束，請在手動移動資源後執行下列命令：

- **RHEL/Ubuntu 範例**

   ```bash
   sudo pcs constraint --full
   ```

- **SLES 範例**

   ```bash
   crm config show
   ```

您需要移除位置條件約束，如此往後的移動 (包括自動容錯移轉) 才會成功。 

若要移除條件約束，請執行下列命令。 

- **RHEL/Ubuntu 範例**

   在此範例中`ag_cluster-master`已移動的資源名稱。 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **SLES 範例**

   在此範例中`ag_cluster`已移動的資源名稱。 

   ```bash
   crm resource clear ag_cluster
   ```

或者，您可以執行下列命令以移除位置條件約束。  

- **RHEL/Ubuntu 範例**

   在下列命令中，`cli-prefer-ag_cluster-master` 是需要移除的條件約束識別碼。 `sudo pcs constraint --full` 會傳回此識別碼。 

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
 

### <a name="forceManual"></a>手動移動時則無法回應叢集工具 

在極端情況下，如果使用者無法互動與叢集使用叢集管理工具 （也就是叢集沒有回應，叢集管理工具有故障的行為），使用者可能必須以手動方式-容錯移轉略過外部叢集管理員。 這不建議在正常的作業，並應內叢集無法在執行容錯移轉動作使用叢集管理工具的情況下使用。

如果您無法容錯移轉叢集管理工具在可用性群組，請遵循下列步驟來容錯移轉從 SQL Server 工具：

1. 請確認，可用性群組資源不由管理叢集了。 

      - 嘗試將資源設定為未受管理的模式。 這表示資源代理程式停止資源監視和管理。 例如： 
      
      ```bash
      sudo pcs resource unmanage <**resourceName**>
      ```

      - 如果將資源模式設定未受管理的模式嘗試失敗，請刪除資源。 例如：

      ```bash
      sudo pcs resource delete <**resourceName**>
      ```

      >[!NOTE]
      >當您刪除資源，它也會刪除所有相關聯的條件約束。 

1. 手動設定工作階段內容變數`external_cluster`。

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. 容錯移轉之可用性群組的 TRANSACT-SQL。 在下面取代範例`<**MyAg**>`與可用性群組的名稱。 連接到裝載目標次要複本的 SQL Server 執行個體，並執行下列命令：

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <**MyAg**> FAILOVER;
   ```

1. 重新啟動叢集資源監視和管理。 執行下列命令：

   ```bash
   sudo pcs resource manage <**resourceName**>
   sudo pcs resource cleanup <**resourceName**>
   ```

## <a name="database-level-monitoring-and-failover-trigger"></a>資料庫層級監視和容錯移轉觸發程序

如`CLUSTER_TYPE=EXTERNAL`，容錯移轉觸發程序語意不相同相較於 WSFC。 在 WSFC 中的 SQL Server 執行個體上可用性群組時，轉換出`ONLINE`狀態的資料庫會造成可用性群組健全狀況，以報告錯誤。 這會指示叢集管理員，以觸發容錯移轉動作。 在 Linux 上的 SQL Server 執行個體無法與叢集通訊。 資料庫健全狀況監視是 「 外部位置 」。 如果使用者已選擇在資料庫層級的容錯移轉的監視和容錯移轉 (藉由設定選項`DB_FAILOVER=ON`建立可用性群組時)，叢集會檢查資料庫狀態是否為`ONLINE`每次當執行監視的動作。 在叢集中的查詢中的狀態`sys.databases`。 不同於任何狀態`ONLINE`，自動 （如果符合自動容錯移轉條件），它將會觸發容錯移轉。 實際的容錯移轉時間取決於監視的動作，以及正在更新 sys.databases 中的資料庫狀態的頻率。

## <a name="upgrade-availability-group"></a>可用性群組升級

您將可用性群組升級之前，請檢閱在的最佳作法[可用性群組複本執行個體升級](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)。

下列各節說明如何在 Linux 上執行輪流升級 SQL Server 執行個體，與可用性群組。 

### <a name="upgrade-steps-on-linux"></a>在 Linux 上的升級步驟

在 Linux 中的 SQL Server 執行個體上的可用性群組複本時，可用性群組的叢集類型是`EXTERNAL`或`NONE`。 除了 Windows Server 容錯移轉叢集 (WSFC) 是由叢集管理員的可用性群組`EXTERNAL`。 與 Corosync pacemaker 是外部叢集管理員的範例。 沒有叢集管理員與可用性群組有叢集類型`NONE`此處所述的升級步驟特有的可用性群組的叢集類型`EXTERNAL`或`NONE`。

1. 在開始之前，備份每個資料庫。
2. 升級 SQL Server 執行個體主控次要複本。

    a. 先升級非同步次要複本。

    b. 升級同步次要複本。

   >[!NOTE]
   >如果可用性群組只有非同步複本-若要避免遺失任何資料會將一個複本變更為同步，並等待同步處理。 接著升級此複本。
   
   b.1。 在裝載次要複本升級的目標節點上停止資源
   
   然後再執行 [升級] 命令，停止資源，因此叢集將不進行監視並不必要地容錯。 下列範例會將會在節點上的位置限制式上停止資源。 更新`ag_cluster-master`的資源名稱和`nodeName1`與裝載複本升級的目標節點。

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```
   b.2。 升級次要複本上的 SQL Server

   下列範例會升級`mssql-server`和`mssql-server-ha`封裝。

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   b.3。 移除位置條件約束

   然後再執行 [升級] 命令，停止資源，因此叢集將不進行監視並不必要地容錯。 下列範例會將會在節點上的位置限制式上停止資源。 更新`ag_cluster-master`的資源名稱和`nodeName1`與裝載複本升級的目標節點。

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   最佳做法，請確定沒有啟動資源 (使用`pcs status`命令) 和連接的次要複本，而且在升級後同步處理狀態。

1. 升級所有次要複本之後，手動容錯移轉到其中一個同步的次要複本。

   使用可用性群組的`EXTERNAL`叢集類型，用於叢集管理工具在容錯移轉; 可用性群組`NONE`叢集類型應該使用 TRANSACT-SQL 來容錯移轉。 
   下列範例會容錯移轉叢集管理工具的可用性群組。 取代`<targetReplicaName>`同步次要複本將成為主要的名稱：

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >下列步驟僅適用於不需要叢集管理員的可用性群組。  
   如果可用性群組叢集類型為`NONE`、 手動容錯移轉。 依序完成下列步驟：

      a. 下列命令會將主要複本設定為次要。 取代`AG1`與可用性群組的名稱。 裝載主要複本的 SQL Server 執行個體上執行的 TRANSACT-SQL 命令。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      b. 下列命令會將同步的次要複本設定為主要。 下列 TRANSACT-SQL 命令目標執行個體上執行的 SQL Server-裝載同步的次要複本的執行個體。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. 容錯移轉之後，SQL Server 升級舊的主要複本上重複相同步驟 b.1 b.3 上面所述的程序。

   下列範例會升級`mssql-server`和`mssql-server-ha`封裝。

   ```bash
   # add constraint for the resource to stop on the upgraded node
   # replace 'nodename2' with the name of the cluster node targeted for upgrade
   pcs constraint location ag_cluster-master avoids nodeName2
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   
   ```bash
   # upgrade mssql-server and mssql-server-ha packages
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

   ```bash
   # remove the constraint; make sure the resource is started and replica is connected and synchronized
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```

1. 外部的叢集與可用性群組的管理員-輸入叢集的地方是外部、 清除所造成的手動容錯移轉的位置限制式。 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. 繼續新升級的次要複本-先前的主要複本的資料移動。 更高版本的執行個體的 SQL Server 會將記錄檔區塊傳送至可用性群組中的較低版本執行個體時，這是必要的。 新的次要複本 （先前的主要複本） 上執行下列命令。

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

在升級之後的所有伺服器，您可以容錯回復的容錯移轉回到原始的主要-必要。 

## <a name="drop-an-availability-group"></a>卸除可用性群組

若要刪除可用性群組，請執行[DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md)。 如果叢集類型為`EXTERNAL`或`NONE`裝載複本的 SQL Server 的每個執行個體上執行命令。 例如，若要卸除可用性群組命名為`group_name`執行下列命令：

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>後續的步驟

[設定 SQL Server 可用性群組的叢集資源的 Red Hat Enterprise Linux 叢集](sql-server-linux-availability-group-cluster-rhel.md)

[設定 SQL Server 可用性群組的叢集資源的 SUSE Linux Enterprise Server 叢集](sql-server-linux-availability-group-cluster-sles.md)

[Ubuntu Server 可用性群組的叢集資源的叢集設定](sql-server-linux-availability-group-cluster-ubuntu.md)

