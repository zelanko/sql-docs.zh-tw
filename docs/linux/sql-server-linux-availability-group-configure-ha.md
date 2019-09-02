---
title: 設定 SQL Server Always On 可用性群組以確保 Linux 上的高可用性
titleSuffix: SQL Server
description: 了解如何建立 SQL Server Always On 可用性群組 (AG) 以確保 Linux 上的高可用性。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 364ed5298c83319ab0915ffc04a393c9a9097bf0
ms.sourcegitcommit: 823d7bdfa01beee3cf984749a8c17888d4c04964
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/26/2019
ms.locfileid: "70030302"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>設定 SQL Server Always On 可用性群組以確保 Linux 上的高可用性

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文描述如何建立 SQL Server Always On 可用性群組 (AG) 以確保 Linux 上的高可用性。 AG 有兩種設定類型。 「高可用性」  設定會使用叢集管理員來確保商務持續性。 此設定也可以包含讀取級別複本。 本文件說明如何建立 AG 以確保高可用性。

您也可以建立用於「讀取級別」  的 AG，而不使用叢集管理員。 讀取級別 AG 只會提供用於效能縮放的唯讀複本。它不會提供高可用性。 若要建立用於讀取級別的 AG ，請參閱[設定 SQL Server 可用性群組供 Linux 上的讀取級別之用](sql-server-linux-availability-group-configure-rs.md)。

您必須在設定中使用兩個或三個同步認可複本，才能保證高可用性和資料保護。 使用三個同步複本時，即使無法使用某部伺服器，AG 也可以自動復原。 如需詳細資訊，請參閱[可用性群組設定的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。 

所有伺服器都必須為實體或虛擬伺服器，而虛擬伺服器必須位於相同的虛擬化平台上。 由於隔離代理程式是平台特定的，因此會有這項需求。 請參閱[客體叢集的原則](https://access.redhat.com/articles/29440#guest_policies)。

## <a name="roadmap"></a>藍圖

在 Linux 伺服器上建立 AG 以確保高可用性的步驟，與 Windows Server 容錯移轉叢集上的步驟不同。 下列清單描述高階步驟： 

1. [在三個叢集伺服器上設定 SQL Server](sql-server-linux-setup.md)。

   >[!IMPORTANT]
   >AG 中所有三部伺服器都必須位於相同的平台上 (實體或虛擬)，因為 Linux 高可用性功能會使用隔離代理程式來隔離伺服器上的資源。 隔離代理程式是每個平台特定的。

2. 建立 AG。 目前的文章將涵蓋此步驟。 

3. 設定叢集資源管理員，例如 Pacemaker。
   
   設定叢集資源管理員的方式取決於特定 Linux 發行版本。 如需發行版本的特定指示，請參閱下列連結： 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >生產環境需要 STONITH 這類隔離代理程式來取得高可用性。 此文件的示範不會使用隔離代理程式。 這些示範僅適用於測試和驗證。 
   
   >Linux 叢集會使用隔離功能將叢集回復為已知的狀態。 設定隔離的方式取決於發行版本和環境。 目前，有些雲端環境無法使用隔離。 如需詳細資訊，請參閱 [Support Policies for RHEL High Availability Clusters - Virtualization Platforms](https://access.redhat.com/articles/29440) (RHEL 高可用性叢集的支援原則 - 虛擬化平台)。
   
   >針對 SLES，請參閱 [SUSE Linux Enterprise High Availability Extension](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing) (SUSE Linux Enterprise 高可用性延伸模組)。

5. 將 AG 新增為叢集中的資源。  

   將 AG 新增為叢集資源的方式取決於 Linux 發行版本。 如需發行版本的特定指示，請參閱下列連結： 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>建立 AG

本節中的範例說明如何使用 Transact-SQL 建立可用性群組。 您也可以使用 SQL Server Management Studio [可用性群組精靈]。 當您使用精靈建立 AG 時，它會在您將複本加入 AG 時傳回錯誤。 若要修正此問題，請將 `ALTER`、`CONTROL` 和 `VIEW DEFINITIONS` 授與所有複本 AG 上的 Pacemaker。 將權限授與主要複本之後，請透過精靈將節點加入 AG，但若要讓 HA 正常運作，請將權限授與所有複本。

如需可確保自動容錯移轉的高可用性設定，AG 需要至少三個複本。 下列任一項設定可支援高可用性：

- [三個同步複本](sql-server-linux-availability-group-ha.md#threeSynch)

- [兩個同步複本加上一個設定複本](sql-server-linux-availability-group-ha.md#twoSynch)

如需詳細資訊，請參閱[可用性群組設定的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。

>[!NOTE]
>可用性群組可包含額外的同步或非同步複本。 

建立 AG 以確保 Linux 上的高可用性。 搭配使用 [CREATE AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql) 與 `CLUSTER_TYPE = EXTERNAL`。 

* 可用性群組 - `CLUSTER_TYPE = EXTERNAL` 指定由外部叢集實體管理 AG。 Pacemaker 即為外部叢集實體的範例。 當 AG 叢集類型為外部時， 

* 將主要和次要複本設為 `FAILOVER_MODE = EXTERNAL`。 
   指定複本會與外部叢集管理員互動，例如 Pacemaker。 

下列 Transact-SQL 指令碼會建立名為 `ag1` 的高可用性 AG。 該指令碼會將 AG 複本設定為 `SEEDING_MODE = AUTOMATIC`。 此設定會導致 SQL Server 在每部次要伺服器上自動建立資料庫。 更新您環境中的下列指令碼。 將 `<node1>`、`<node2>` 或 `<node3>` 值取代為裝載複本的 SQL Server 執行個體名稱。 將 `<5022>` 取代為您為資料鏡像端點設定的連接埠。 若要建立 AG，請在裝載主要複本的 SQL Server 執行個體上執行下列 Transact-SQL。

執行下列指令碼**之一**： 

- [建立具有三個同步複本的可用性群組](#threeSynch)。
- [建立具有兩個同步複本和一個設定複本的可用性群組](#configOnly)
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
   >在您執行上述指令碼來建立具有三個同步複本的 AG 之後，請不要執行下列指令碼：

<a name="configOnly"></a>
- 建立具有兩個同步複本和一個設定複本的 AG：

   >[!IMPORTANT]
   >此結構可讓任何版本的 SQL Server 裝載第三個複本。 例如，您可以在 SQL Server Express Edition 上裝載第三個複本。 在 Express Edition 中，唯一有效的端點類型是 `WITNESS`。 

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

   包含兩個具有同步可用性模式的複本。 例如，下列指令碼會建立稱為 `ag1` 的 AG。 `node1` 和 `node2` 會以同步模式裝載複本，並提供自動植入和自動容錯移轉功能。

   >[!IMPORTANT]
   >僅執行下列指令碼，以建立具有兩個同步複本的 AG。 如果您已執行上述任一指令碼，請不要執行下列指令碼。 

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


您也可以使用 SQL Server Management Studio 或 PowerShell 來設定 `CLUSTER_TYPE=EXTERNAL` 的 AG。 

### <a name="join-secondary-replicas-to-the-ag"></a>將次要複本加入 AG

Pacemaker 使用者需具備所有複本上可用性群組的 `ALTER`、`VIEW DEFINITION` 和 `CONTROL` 權限。 若要授與權限，請在主要複本及每個次要複本上建立可用性群組，並將這些權限新增至可用性群組之後，立即執行下列 Transact-SQL 指令碼。 請將 `<pacemakerLogin>` 取代為 Pacemaker 使用者帳戶名稱，再執行指令碼。 如果您沒有 Pacemaker 的登入，請[建立 pacemaker 的 SQL Server 登入](sql-server-linux-availability-group-cluster-ubuntu.md#create-a-sql-server-login-for-pacemaker)。

```sql
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO <pacemakerLogin>
GRANT VIEW SERVER STATE TO <pacemakerLogin>
```

下列 Transact-SQL 指令碼會將 SQL Server 執行個體加入名為 `ag1` 的 AG。 更新您環境中的指令碼。 在每個裝載次要複本的 SQL Server 執行個體上，執行下列 Transact-SQL 以加入 AG。

```sql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>建立 AG 之後，您必須設定叢集技術 (例如 Pacemaker) 的整合，以確保高可用性。 針對使用 AG 的讀取級別設定，從 [!INCLUDE [SQL Server version](../includes/sssqlv14-md.md)] 開始，即已不需要設定叢集。

如果您遵循本文件的步驟，會產生尚未叢集化的 AG。 下一個步驟是新增叢集。 此設定適用於讀取級別/負載平衡案例，但需進一步完成才能確保高可用性。 如需高可用性，您必須將 AG 新增為叢集資源。 如需相關指示，請參閱[後續步驟](#next-steps)。 

## <a name="notes"></a>注意

>[!IMPORTANT]
>當您設定叢集並將 AG 新增為叢集資源之後，就無法使用 Transact-SQL 來容錯移轉 AG 資源。 Linux 上的 SQL Server 叢集資源不會與作業系統緊密結合，因為其位於 Windows Server 容錯移轉叢集 (WSFC) 上。 SQL Server 服務不知道叢集是否存在。 所有協調流程都會透過叢集管理工具來完成。 在 RHEL 或 Ubuntu 中，請使用 `pcs`。 在 SLES 中，請使用 `crm`。 

>[!IMPORTANT]
>如果 AG 是叢集資源，在目前的版本中有個已知問題：非同步複本的資料遺失強制容錯移轉無法運作。 即將推出的版本將會修正此問題。 同步複本的手動或自動容錯移轉會成功。


## <a name="next-steps"></a>後續步驟

[設定 Red Hat Enterprise Linux 叢集的 SQL Server 可用性群組叢集資源](sql-server-linux-availability-group-cluster-rhel.md)

[設定 SUSE Linux Enterprise Server 叢集的 SQL Server 可用性群組叢集資源](sql-server-linux-availability-group-cluster-sles.md)

[設定 Ubuntu 叢集的 SQL Server 可用性群組叢集資源](sql-server-linux-availability-group-cluster-ubuntu.md)
