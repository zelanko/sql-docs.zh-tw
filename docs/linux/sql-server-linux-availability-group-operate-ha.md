---
title: 在 Linux 上的 SQL Server 操作可用性群組
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 24a9d3d9ee0fd65b08e30f40a0597eadf47c6b76
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67916044"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>在 Linux 上操作 Always On 可用性群組

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>升級可用性群組

升級可用性群組之前，請檢閱[升級可用性群組複本執行個體](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)中的模式和做法。

下列各節說明如何對 Linux 上具有可用性群組的 SQL Server 執行個體執行輪流升級。 

### <a name="upgrade-steps-on-linux"></a>Linux 上的升級步驟

當可用性群組複本位於 Linux 中的 SQL Server 執行個體上時，可用性群組的叢集類型為 `EXTERNAL` 或 `NONE`。 除了 Windows Server 容錯移轉叢集 (WSFC) 以外，由叢集管理員所管理的可用性群組為 `EXTERNAL`。 Pacemaker 與 Corosync 即為外部叢集管理員的範例。 沒有叢集管理員的可用性群組具有叢集類型 `NONE`。此處所述的升級步驟僅適用於叢集類型 `EXTERNAL` 或 `NONE` 的可用性群組。

升級執行個體的順序取決於其角色是否為次要，以及其裝載的是同步或非同步複本。 裝載非同步次要複本的 SQL Server 執行個體會先升級。 再升級裝載同步次要複本的執行個體。 

   >[!NOTE]
   >如果可用性群組只有非同步複本，為了避免任何資料遺失，請將一個複本變更為同步，並等候直到同步完成為止。 然後升級此複本。
   
開始之前，請備份每個資料庫。

1. 停止裝載升級目標次要複本之節點上的資源。
   
   執行升級命令之前，請停止資源，以便叢集不受監視及不必要地予以容錯移轉。 下列範例會在節點上新增位置限制式，這會導致資源停止。 將 `ag_cluster-master` 更新為資源名稱，並將 `nodeName1` 更新為裝載要升級之目標複本的節點。

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. 升級次要複本上的 SQL Server。

   下列範例會升級 `mssql-server` 和 `mssql-server-ha` 套件。

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. 移除位置限制式。

   執行升級命令之前，請停止資源，以便叢集不受監視及不必要地予以容錯移轉。 下列範例會在節點上新增位置限制式，這會導致資源停止。 將 `ag_cluster-master` 更新為資源名稱，並將 `nodeName1` 更新為裝載要升級之目標複本的節點。

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   最佳做法是在升級後，確定資源已啟動 (使用 `pcs status` 命令)，且次要複本處於已連接和同步的狀態。

1. 升級所有次要複本之後，請以手動方式容錯移轉到其中一個同步次要複本。

   針對具有 `EXTERNAL` 叢集類型的可用性群組，請使用叢集管理工具進行容錯移轉；具有 `NONE` 叢集類型的可用性群組應該使用 Transact-SQL 進行容錯移轉。 
   下列範例使用叢集管理工具，容錯移轉可用性群組。 將 `<targetReplicaName>` 取代為要成為主要複本的同步次要複本名稱：

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >下列步驟僅適用於沒有叢集管理員的可用性群組。

   如果可用性群組叢集類型為 `NONE`，請以手動方式進行容錯移轉。 依序完成下列步驟：

      A. 下列命令會將主要複本設定為次要複本。 將 `AG1` 取代為您的可用性群組名稱。 在裝載主要複本的 SQL Server 執行個體上，執行 Transact-SQL 命令。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      B. 下列命令會將同步次要複本設定為主要複本。 在裝載同步次要複本的目標 SQL Server 執行個體上，執行下列 Transact-SQL 命令。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. 容錯移轉之後，請重複上述程序，升級舊主要複本上的 SQL Server。

   下列範例會升級 `mssql-server` 和 `mssql-server-ha` 套件。

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

1. 針對具有外部叢集管理員 (其中叢集類型為 EXTERNAL) 的可用性群組，請清除手動容錯移轉所造成的位置限制式。 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. 繼續為新升級的次要複本 (先前的主要複本) 移動資料。 當 SQL Server 較高版本的執行個體將記錄區塊轉送到可用性群組中較低版本的執行個體時，即需執行此步驟。 在新的次要複本 (先前的主要複本) 上，執行下列命令。

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

升級所有伺服器之後，即可進行容錯回復。 如有需要，請容錯回復到原始的主要複本。 

## <a name="drop-an-availability-group"></a>置放可用性群組

若要刪除可用性群組，請執行 [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md)。 如果叢集類型為 `EXTERNAL` 或 `NONE`，請在每個裝載複本的 SQL Server 執行個體上執行命令。 例如，若要置放名為 `group_name` 的可用性群組，請執行下列命令：

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>後續步驟

[設定 Red Hat Enterprise Linux 叢集的 SQL Server 可用性群組叢集資源](sql-server-linux-availability-group-cluster-rhel.md)

[設定 SUSE Linux Enterprise Server 叢集的 SQL Server 可用性群組叢集資源](sql-server-linux-availability-group-cluster-sles.md)

[設定 Ubuntu 叢集的 SQL Server 可用性群組叢集資源](sql-server-linux-availability-group-cluster-ubuntu.md)
