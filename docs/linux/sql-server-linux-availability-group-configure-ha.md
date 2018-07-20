---
title: 設定 SQL Server Always On 可用性群組在 Linux 上的高可用性 |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 801009112dffaa83bd1c938194a27934e4bbbdaa
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082710"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>設定 SQL Server Always On 可用性群組在 Linux 上的高可用性

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何在 Linux 上建立 SQL Server Alwayson 上可用性群組 (AG) 的高可用性。 有兩種設定類型的 Ag。 A*高可用性*組態會使用 「 叢集管理員來提供商務持續性。 此設定也可以包含讀取級別複本。 本文件說明如何建立高可用性的 AG。

您也可以建立的 AG，而不需要叢集管理員*讀取級別*。 讀取級別的 AG 只會提供效能相應放大的唯讀複本。它不提供高可用性。 若要建立的讀取級別 AG，請參閱[在 Linux 上設定 SQL Server 可用性群組的讀取級別](sql-server-linux-availability-group-configure-rs.md)。

保證高可用性和資料保護的組態需要兩個或三個同步認可複本。 具有三個同步複本，AG 可以自動復原，即使沒有一部伺服器。 如需詳細資訊，請參閱 <<c0> [ 可用性群組組態的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。 

所有伺服器必須都是實體或虛擬的而且虛擬伺服器必須都位於相同的虛擬化平台。 這項需求是因為柵欄代理程式都是特定的平台。 請參閱[客體叢集的原則](https://access.redhat.com/articles/29440#guest_policies)。

## <a name="roadmap"></a>藍圖

在高可用性的 Linux 伺服器上建立 AG 的步驟是從 Windows Server 容錯移轉叢集上的步驟不同。 下列清單說明的概要步驟： 

1. [在三個叢集伺服器上設定 SQL Server](sql-server-linux-setup.md)。

   >[!IMPORTANT]
   >在 AG 中的所有三個伺服器必須位於相同的平台-實體或虛擬的因為 Linux 高可用性使用隔離代理程式來找出伺服器上的資源。 隔離代理程式是針對每個平台。

2. 建立 AG。 此步驟涵蓋此目前的文件中。 

3. 設定叢集資源管理員，例如 Pacemaker。
   
   若要設定叢集資源管理員的方式取決於特定的 Linux 散發套件。 請參閱下列連結以取得發佈的特定指示： 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >生產環境需要隔離代理程式，例如高可用性的 STONITH。 在本文件示範，請勿使用隔離代理程式。 示範適用於測試、 僅驗證。 
   
   >Linux 叢集會使用隔離，讓叢集回到已知狀態。 若要設定隔離的方式取決於發佈和環境。 目前，隔離不適用於某些雲端環境。 如需詳細資訊，請參閱 < [RHEL 的高可用性叢集-而虛擬化平台的支援原則](https://access.redhat.com/articles/29440)。
   
   >Sles，請參閱[SUSE Linux Enterprise 高可用性延伸](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)。

5. 新增 AG 為叢集中的資源。  

   新增 AG 為叢集中資源的方式取決於 Linux 散發套件。 請參閱下列連結以取得發佈的特定指示： 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>建立 AG

針對高可用性組態，以確保自動容錯移轉，AG 會需要至少三個複本。 下列設定其中一種方法可支援高可用性：

- [三個同步複本](sql-server-linux-availability-group-ha.md#threeSynch)

- [兩個同步複本，再加上設定複本](sql-server-linux-availability-group-ha.md#twoSynch)

如需資訊，請參閱[可用性群組組態的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。

>[!NOTE]
>可用性群組可以包含額外的同步或非同步複本。 

在 Linux 上建立高可用性的 AG。 使用[CREATE AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql)使用`CLUSTER_TYPE = EXTERNAL`。 

* 可用性群組-`CLUSTER_TYPE = EXTERNAL`指定外部叢集實體管理 AG。 Pacemaker 是外部叢集實體的範例。 當 AG 叢集類型是外部的 

* 設定主要和次要複本`FAILOVER_MODE = EXTERNAL`。 
   指定複本互動外部叢集管理員 中，例如 Pacemaker。 

下列 TRANSACT-SQL 指令碼會建立名為高可用性的 AG `ag1`。 該指令碼會將 AG 複本設定為 `SEEDING_MODE = AUTOMATIC`。 此設定會導致自動建立每個次要伺服器上的 資料庫的 SQL Server。 更新您環境中的下列指令碼。 取代`<node1>`， `<node2>`，或`<node3>`裝載複本的 SQL Server 執行個體名稱的值。 取代`<5022>`您為資料鏡像端點的連接埠設定。 若要建立 AG，請在裝載主要複本的 SQL Server 執行個體上執行下列的 TRANSACT-SQL。

執行**只有一個**下列指令碼： 

- [建立具有三個同步複本的可用性群組](#threeSynch)。
- [建立具有兩個同步複本，並設定複本的可用性群組](#configOnly)
- [建立具有兩個同步複本的可用性群組](#readScale)。

<a name="threeSynch"></a>

- 建立具有三個同步複本的 AG

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'<node1>' 
            WITH (
               ENDPOINT_URL = N'tcp://<node1>:<5022>',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node2>' 
            WITH ( 
               ENDPOINT_URL = N'tcp://<node2>:<5022>', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node3>'
           WITH( 
              ENDPOINT_URL = N'tcp://<node3>:<5022>', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >執行上述指令碼來建立具有三個同步複本的 AG 之後，無法執行下列指令碼：

- 建立具有兩個同步複本和設定複本的 AG:

   >[!IMPORTANT]
   >此架構可讓任何版本的 SQL Server 以裝載第三個複本。 比方說，第三個複本可裝載於 SQL Server Enterprise Edition。 在 Enterprise 版本中，唯一有效的端點類型是`WITNESS`。 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'<node1>' WITH ( 
          ENDPOINT_URL = N'tcp://<node1>:<5022>', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node2>' WITH (  
          ENDPOINT_URL = N'tcp://<node2>:<5022>',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node3>' WITH ( 
          ENDPOINT_URL = N'tcp://<node3>:<5022>', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- 建立具有兩個同步複本的 AG

   包含兩個複本與同步的可用性模式。 例如，下列指令碼會建立稱為 AG `ag1`。 `node1` 和`node2`裝載複本在同步模式中，使用自動植入和自動容錯移轉。

   >[!IMPORTANT]
   >只執行下列指令碼來建立具有兩個同步複本的 AG。 請勿執行下列指令碼，如果您執行上述指令碼。 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
      N'node1' WITH (
         ENDPOINT_URL = N'tcp://node1:5022',
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      ),
      N'node2' WITH ( 
         ENDPOINT_URL = N'tcp://node2:5022', 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```


您也可以設定與 AG`CLUSTER_TYPE=EXTERNAL`使用 SQL Server Management Studio 或 PowerShell。 

### <a name="join-secondary-replicas-to-the-ag"></a>將次要複本聯結至 AG

下列 TRANSACT-SQL 指令碼會加入名為 AG 中的 SQL Server 執行個體`ag1`。 更新您環境中的指令碼。 在裝載次要複本的每個 SQL Server 執行個體，執行下列 TRANSACT-SQL 將 AG。

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>建立 AG 之後，您必須設定與高可用性等 Pacemaker 叢集技術的整合。 讀取級別組態使用 Ag，開頭[!INCLUDE [SQL Server version](..\includes\sssqlv14-md.md)]，不需要設定叢集。

如果您遵循這份文件中的步驟，您有尚未進行叢集的 AG。 下一個步驟是新增叢集。 此設定適用於讀取級別/負載平衡的情況下，不是完整的高可用性。 如需高可用性，您要新增為叢集資源的 AG。 請參閱[後續步驟](#next-steps)如需相關指示。 

## <a name="notes"></a>注意

>[!IMPORTANT]
>在設定叢集，並新增為叢集資源的 AG 之後，您無法使用 TRANSACT-SQL 來容錯移轉 AG 資源。 在 Linux 上的 SQL Server 叢集資源未結合緊密與作業系統和它們在 Windows Server 容錯移轉叢集 (WSFC)。 SQL Server 服務並不知道叢集的目前狀態。 所有的協調流程是透過叢集管理工具。 在 RHEL 或 Ubuntu 使用`pcs`。 在 SLES 使用`crm`。 

>[!IMPORTANT]
>如果叢集資源為 AG，有強制容錯移轉至非同步複本遺失的資料不會無法運作的目前版本中是已知的問題。 這將會在即將推出的版本中修正。 同步複本的手動或自動容錯移轉會成功。 


## <a name="next-steps"></a>後續步驟

[設定 SQL Server 可用性群組叢集資源的 Red Hat Enterprise Linux 叢集](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 可用性群組叢集資源設定 SUSE Linux Enterprise Server 叢集](sql-server-linux-availability-group-cluster-sles.md)

[設定 SQL Server 可用性群組叢集資源的 Ubuntu 叢集](sql-server-linux-availability-group-cluster-ubuntu.md)
