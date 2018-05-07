---
title: 設定 SQL Server Alwayson 可用性群組在 Linux 上的高可用性 |Microsoft 文件
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 02/14/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.openlocfilehash: f3de124b11a6093279fe01cb759ae87f39b93f46
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>設定 SQL Server Alwayson 可用性群組在 Linux 上的高可用性

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何在 Linux 上建立 SQL Server Alwayson 上可用性群組 (AG) 的高可用性。 有兩種 Ag 組態類型。 A*高可用性*組態會使用 「 叢集管理員提供業務續航力。 這項設定也可以包含向外延展讀取的複本。 本文件說明如何建立高可用性的 AG。

您也可以建立不含叢集 AG 管理員*向外延展讀取*。 讀取的標尺的 AG 只會提供向外延展效能的唯讀複本。它不提供高可用性。 若要建立的向外延展讀取 AG，請參閱[SQL Server 可用性群組設定為向外延展讀取 on Linux](sql-server-linux-availability-group-configure-rs.md)。

保證高可用性與資料保護的設定，都需要兩個或三個同步認可複本。 包含三個同步複本、 AG 才能自動復原即使如果一部伺服器無法使用。 如需詳細資訊，請參閱[可用性群組組態的高可用性與資料保護](sql-server-linux-availability-group-ha.md)。 

所有伺服器都必須都是實體或虛擬，以及虛擬伺服器必須都位於相同的虛擬化平台上。 這是因為圍欄代理程式都是特定的平台。 請參閱[客體叢集的原則](https://access.redhat.com/articles/29440#guest_policies)。

## <a name="roadmap"></a>藍圖

在高可用性的 Linux 伺服器上建立 AG 的步驟會與不同的 Windows Server 容錯移轉叢集的步驟。 下列清單描述的概要步驟： 

1. [三部叢集伺服器上設定 SQL Server](sql-server-linux-setup.md)。

   >[!IMPORTANT]
   >AG 中所有的三個伺服器必須在相同的平台的實體或虛擬的因為 Linux 高可用性使用圍欄代理程式來隔離伺服器上的資源。 圍欄代理程式會針對每個平台。

2. 建立 AG。 目前本文涵蓋這個步驟。 

3. 設定叢集資源管理員，例如 Pacemaker。
   
   設定叢集資源管理員的方式取決於特定 Linux 發佈。 請參閱下列連結以取得發佈的特定指示： 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >實際執行環境中需要隔離代理程式，例如 STONITH 高可用性。 在本文件示範請勿圍欄代理程式。 此示範的使用者是用於測試和驗證。 
   
   >Linux 叢集使用圍欄叢集回到已知狀態。 設定範圍的方式取決於分佈和環境。 目前，範圍不適用於某些雲端環境中。 如需詳細資訊，請參閱[RHEL 的高可用性叢集-而虛擬化平台的支援政策](https://access.redhat.com/articles/29440)。
   
   >SLES，請參閱[SUSE Linux Enterprise 高可用性延伸](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)。

5. 新增 AG 做為叢集中的資源。  

   新增 AG 為叢集中資源的方式取決於 Linux 散發套件。 請參閱下列連結以取得發佈的特定指示： 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>建立 AG

高可用性組態，以確保自動容錯移轉，AG 需要至少三個複本。 以下任一設定可以支援高可用性：

- [三個同步複本](sql-server-linux-availability-group-ha.md#threeSynch)

- [兩個同步複本，再加上設定複本](sql-server-linux-availability-group-ha.md#twoSynch)

如需資訊，請參閱[可用性群組組態的高可用性與資料保護](sql-server-linux-availability-group-ha.md)。

>[!NOTE]
>可用性群組可以包含其他同步或非同步複本。 

在 Linux 上建立高可用性的 AG。 使用[建立可用性群組](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-availability-group-transact-sql)與`CLUSTER_TYPE = EXTERNAL`。 

* 可用性群組-`CLUSTER_TYPE = EXTERNAL`指定外部叢集實體管理 AG。 Pacemaker 是外部叢集實體的範例。 當 AG 叢集類型是外部的 

* 設定主要和次要複本`FAILOVER_MODE = EXTERNAL`。 
   指定複本互動外部叢集管理員 中，例如 Pacemaker。 

下列的 TRANSACT-SQL 指令碼會建立名為高可用性的 AG `ag1`。 指令碼會設定 AG 複本`SEEDING_MODE = AUTOMATIC`。 此設定會自動在每個次要伺服器上建立資料庫的 SQL Server。 更新您的環境中的下列指令碼。 取代`<node1>`， `<node2>`，或`<node3>`裝載複本的 SQL Server 執行個體名稱的值。 取代`<5022>`您設定與連接埠鏡像端點的資料。 若要建立 AG，請在裝載主要複本的 SQL Server 執行個體上執行下列 TRANSACT-SQL。

執行**只有一個**下列指令碼： 

- [建立包含三個同步複本的可用性群組](#threeSynch)。
- [具有兩個同步複本及設定複本建立可用性群組](#configOnly)
- [建立具有兩個同步複本的可用性群組](#readScale)。

<a name="threeSynch"></a>

- 建立包含三個同步複本的 AG

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
   >執行上述指令碼來建立包含三個同步複本 AG 之後，無法執行下列指令碼：

- 具有兩個同步複本及設定複本建立 AG:

   >[!IMPORTANT]
   >此架構可讓任何版本的 SQL Server 以裝載第三個複本。 例如，第三個複本可以裝載於 SQL Server Enterprise Edition。 在 Enterprise 版本中，唯一有效的端點類型是`WITNESS`。 

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

- 建立包含兩個同步複本的 AG

   包含兩個複本與同步的可用性模式。 例如，下列指令碼會建立稱為 AG `ag1`。 `node1` 和`node2`裝載在同步模式中，使用自動植入和自動容錯移轉的複本。

   >[!IMPORTANT]
   >只能執行下列指令碼來建立兩個同步複本與 AG。 如果您執行上述指令碼無法執行下列指令碼。 

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

下列的 TRANSACT-SQL 指令碼會將 SQL Server 執行個體聯結至名為 AG `ag1`。 更新您的環境的指令碼。 在裝載次要複本的每個 SQL Server 執行個體，執行下列 TRANSACT-SQL 加入 AG。

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>建立 AG 之後，您必須設定整合與叢集技術，例如 Pacemaker 高可用性。 使用 Ag，開頭為向外延展讀取組態[!INCLUDE [SQL Server version](..\includes\sssqlv14-md.md)]，叢集就不需要設定。

如果您遵循本文件中的步驟，您有尚未進行叢集 AG。 將叢集新增為下一個步驟。 這項設定適用於讀取比例/負載平衡的情況下，不是完整高可用性。 高可用性，您要新增為叢集資源的 AG。 請參閱[後續步驟](#next-steps)如需相關指示。 

## <a name="notes"></a>注意

>[!IMPORTANT]
>您設定叢集，並新增為叢集資源的 AG 之後，您無法使用 Transact SQL 容錯移轉的 AG 資源。 在 Linux 上的 SQL Server 叢集資源不搭配嚴格作業系統和它們在 Windows Server 容錯移轉叢集 (WSFC)。 SQL Server 服務並不知道叢集的存在。 所有的協調流程會透過叢集管理工具。 在 RHEL 或 Ubuntu 使用`pcs`。 在 SLES 使用`crm`。 

>[!IMPORTANT]
>AG 是叢集資源，如果有強制容錯移轉至非同步複本遺失的資料不會無法運作的目前版本中是已知的問題。 這將在近期版本中修正。 同步複本的手動或自動容錯移轉成功。 


## <a name="next-steps"></a>後續的步驟

[設定 SQL Server 可用性群組的叢集資源的 Red Hat Enterprise Linux 叢集](sql-server-linux-availability-group-cluster-rhel.md)

[設定 SQL Server 可用性群組的叢集資源的 SUSE Linux Enterprise Server 叢集](sql-server-linux-availability-group-cluster-sles.md)

[Ubuntu Server 可用性群組的叢集資源的叢集設定](sql-server-linux-availability-group-cluster-ubuntu.md)
