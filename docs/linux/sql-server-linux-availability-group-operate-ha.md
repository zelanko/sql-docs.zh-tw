---
title: 操作可用性群組在 Linux 上的 SQL Server
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: c1dfdeead4f8eb82dc95882d719ef42f16017bdc
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834246"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>一律對 Linux 上的可用性群組

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>可用性群組升級

您的可用性群組升級之前，請檢閱的模式和最佳作法[可用性群組複本執行個體升級](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)。

下列各節說明如何在 Linux 上執行輪流升級 SQL Server 執行個體，使用可用性群組。 

### <a name="upgrade-steps-on-linux"></a>在 Linux 上的升級步驟

在 Linux 中的 SQL Server 執行個體上可用性群組複本時，可用性群組的叢集類型是`EXTERNAL`或`NONE`。 可用性群組 besides 是 Windows Server 容錯移轉叢集 (WSFC) 叢集管理員管理`EXTERNAL`。 使用 Corosync pacemaker 是外部叢集管理員 的範例。 可用性群組不使用叢集管理員有叢集類型`NONE`此處所述的升級步驟是針對可用性群組的叢集類型`EXTERNAL`或`NONE`。

您將升級執行個體的順序取決於其角色是否次要資料庫，以及它們裝載同步或非同步複本。 升級第一次裝載非同步的次要複本的 SQL Server 執行個體。 然後將裝載同步的次要複本的執行個體的升級。 

   >[!NOTE]
   >如果可用性群組只有非同步複本，以避免遺失任何資料變更為同步的一個複本，並等候它完成同步。 然後將此複本的升級。
   
在開始之前，請將每個資料庫備份。

1. 在裝載次要複本進行升級的目標節點上停止資源。
   
   執行升級命令之前，請停止資源，因此叢集不會監視它，且不會不必要地將它容錯。 下列範例會將位置條件約束會在節點上的的資源，以停止。 更新`ag_cluster-master`的資源名稱和`nodeName1`裝載複本升級為目標的節點。

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. 升級 SQL Server 上的次要複本。

   下列範例會升級`mssql-server`和`mssql-server-ha`封裝。

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. 移除位置條件約束。

   執行升級命令之前，請停止資源，因此叢集不會監視它，且不會不必要地將它容錯。 下列範例會將位置條件約束會在節點上的的資源，以停止。 更新`ag_cluster-master`的資源名稱和`nodeName1`裝載複本升級為目標的節點。

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   最佳做法，請確定 啟動任何資源 (使用`pcs status`命令) 和次要複本已連接和同步處理升級後的狀態。

1. 升級所有次要複本之後，手動容錯移轉至其中一個同步次要複本。

   具有的可用性群組`EXTERNAL`叢集類型，請使用叢集管理工具，容錯移轉; 可用性群組搭配`NONE`叢集類型應該使用 TRANSACT-SQL 來容錯移轉。 
   下列範例會容錯移轉叢集管理工具的可用性群組。 取代`<targetReplicaName>`會變成主要複本的同步次要複本的名稱：

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >下列步驟只適用於不需要叢集管理員的可用性群組。

   如果可用性群組叢集類型`NONE`、 手動容錯移轉。 依序完成下列步驟：

      a. 下列命令會將主要複本設定為次要。 取代`AG1`您的可用性群組的名稱。 在裝載主要複本的 SQL Server 執行個體上執行 TRANSACT-SQL 命令。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      b. 下列命令會將同步的次要複本設定為主要。 在 SQL Server-主控同步的次要複本的執行個體的目標執行個體上執行下列 TRANSACT-SQL 命令。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. 容錯移轉之後，將 SQL Server 升級舊的主要複本上，重複上述程序。

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

1. 對於可用性群組與外部叢集管理員-其中的叢集類型是外部，清除所造成的手動容錯移轉的位置限制式。 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. 繼續新升級的次要複本-先前的主要複本的資料移動為止。 更高版本的執行個體的 SQL Server 會將記錄區塊傳送至可用性群組中的較低版本執行個體時，就需要此步驟。 新的次要複本 （先前的主要複本） 上執行下列命令。

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

在升級之後的所有伺服器，您可以容錯回復。 如有必要，容錯移轉回原始的主要。 

## <a name="drop-an-availability-group"></a>卸除可用性群組

若要刪除可用性群組，請執行[DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md)。 如果叢集類型是`EXTERNAL`或`NONE`每個主控複本的 SQL Server 執行個體上執行命令。 例如，若要卸除可用性群組命名為`group_name`執行下列命令：

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>後續步驟

[設定 SQL Server 可用性群組叢集資源的 Red Hat Enterprise Linux 叢集](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 可用性群組叢集資源設定 SUSE Linux Enterprise Server 叢集](sql-server-linux-availability-group-cluster-sles.md)

[設定 SQL Server 可用性群組叢集資源的 Ubuntu 叢集](sql-server-linux-availability-group-cluster-ubuntu.md)
