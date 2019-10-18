---
title: 以高可用性部署 SQL Server Big Data 叢集
titleSuffix: Deploy SQL Server Big Data Cluster with high availability
description: 瞭解如何部署具有高可用性的 SQL Server Big Data 叢集。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 43d651c46282d7de0ffdd60f326740e7821b9bbe
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542166"
---
# <a name="deploy-sql-server-big-data-cluster-with-high-availability"></a>以高可用性部署 SQL Server Big Data 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在部署 big data cluster （BDC）時，您可以設定要在可用性群組設定中部署 SQL Server master。 這項設定可提高 SQL Server 主機的可靠性，以及其內建的健全狀況監視、失敗偵測和容錯移轉機制所提供的 Kubernetes 基礎結構。 可用性群組（AG）會將冗余新增至 SQL Server 實例。 在此設定中，監視、失敗偵測和容錯移轉工作是由 big data cluster management 服務（即控制服務）所管理。

此外，大型資料叢集平臺會提供其他管理工作，例如設定資料庫鏡像端點、建立可用性群組，以及將資料庫新增至可用性群組。

以下是可用性群組可啟用的部分功能：

1. 如果部署設定檔中指定了高可用性設定，就會建立名為 `containedag` 的單一可用性群組。 根據預設，`containedag` 有三個複本，包括 [主要]。 可用性群組的所有 CRUD 作業都是在內部進行管理。
1. 所有資料庫都會自動加入至可用性群組，包括 `master` 和 `msdb`。 Polybase 設定資料庫不會包含在可用性群組中，因為它們包含每個複本特有的實例層級中繼資料。
1. 系統會自動布建外部端點以連接到 AG 資料庫。 此端點 `master-svc-external` 扮演 AG 接聽程式的角色。
1. 第二個外部端點是針對次要複本的唯讀連接所布建。 


## <a name="deploy"></a>部署

若要在可用性群組中部署 SQL Server master：

1. 啟用 `hadr` 功能
1. 指定 AG 的複本數目（最小值為3）
1. 設定針對連接至唯讀次要複本所建立之第二個外部端點的詳細資料

下列步驟示範如何建立包含這些設定的修補檔案，以及如何將它套用至 `aks-dev-test` 或 `kubeadm-dev-test` 設定檔。 這些步驟會逐步解說如何修補 `aks-dev-test` 設定檔以新增 HA 屬性的範例。針對 kubeadm 叢集上的部署，將會套用類似的修補程式，但請確定您在 [**端點**] 區段中使用的是 [ **serviceType** ] *NodePort* 。

1. 建立 `patch.json` 檔案

    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.resources.master.spec",
          "value": {
            "type": "Master",
            "replicas": 3,
            "endpoints": [
              {
                "name": "Master",
                "serviceType": "LoadBalancer",
                "port": 31433
              },
              {
                "name": "MasterSecondary",
                "serviceType": "LoadBalancer",
                "port": 31436
              }
            ],
            "settings": {
              "sql": {
                "hadr.enabled": "true"
              }
            }
          }
        }
      ]
    }
    ```

1. 複製您的目標設定檔

    ```bash
    azdata bdc config init --source aks-dev-test --target custom-aks
    ```

1. 將修補檔案套用至自訂設定檔

    ```bash
    azdata bdc config patch -c custom-aks/bdc.json --patch-file patch.json
    ```
1. 使用上面建立的叢集設定檔來啟動叢集部署

    ```bash
    azdata bdc create --config-profile custom-aks --accept-eula yes
    ```

## <a name="connect-to-sql-server-databases"></a>連接到 SQL Server 資料庫

視您想要針對 SQL Server master 執行的工作負載類型而定，您可以連線到主要複本以進行讀寫工作負載，或連接到次要複本中的資料庫，以進行唯讀類型的工作負載。 以下是每種連線類型的大綱：

### <a name="connect-to-databases-on-the-primary-replica"></a>連接到主要複本上的資料庫

若要連接到主要複本，請使用 `sql-server-master` 端點。 這個端點也是 AG 的接聽程式。 所有連接都在可用性群組的內容中。 例如，使用此端點的預設連接會導致連接到 AG 中的 `master` 資料庫，而不是 SQL Server 實例 `master` 資料庫。

```bash
azdata bdc endpoint list -e sql-server-master -o table
```

`Description                           Endpoint             Name               Protocol`
`------------------------------------  -------------------  -----------------  ----------`
`SQL Server Master Instance Front-End  13.64.235.192,31433  sql-server-master  tds`

> [!NOTE]
> 在從遠端資料源（例如 HDFS 或資料集區）存取資料的分散式查詢執行期間，可能會發生容錯移轉事件。 作為最佳作法，應用程式應該設計成在因容錯移轉而造成中斷連線時具有連接重試邏輯。  
>

### <a name="connect-to-databases-on-the-secondary-replicas"></a>連接到次要複本上的資料庫

如需次要複本中資料庫的唯讀連接，請使用 `sql-server-master-readonly` 端點。 此端點的作用就像是所有次要複本上的負載平衡器。 在連接字串中提供使用者資料庫內容。

```bash
azdata bdc endpoint list -e sql-server-master-readonly -o table
```

`Description                                    Endpoint            Name                        Protocol`
`---------------------------------------------  ------------------  --------------------------  ----------`
`SQL Server Master Readable Secondary Replicas  13.64.238.24,31436  sql-server-master-readonly  tds`

### <a id="instance-connect"></a>連接到 SQL Server 實例

針對某些作業，例如設定伺服器層級設定，或手動將資料庫加入至可用性群組（如果資料庫是使用還原工作流程所建立），您需要實例的連接。 若要提供此連接，請公開外部端點。 以下範例顯示如何公開此端點，然後將使用還原工作流程建立的資料庫加入至可用性群組。

- 藉由連接到 `sql-server-master` 端點並執行，判斷裝載主要複本的 pod：

    ```sql
    SELECT @@SERVERNAME
   ```

- 藉由建立新的 Kubernetes 服務來公開外部端點

    針對 kubeadm 叢集，請執行下列命令。 以`podName`上一個步驟所傳回的伺服器名稱取代， `serviceName`並以所建立的 Kubernetes 服務的慣用名稱取代`namespaceName`*，並以您的 BDC 叢集名稱取代 。

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=NodePort
    ```

    針對 aks 叢集執行，請執行相同的命令，但所建立的服務類型將會 `LoadBalancer`。 例如： 

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=LoadBalancer
    ```

    以下是針對 aks 執行此命令的範例，其中裝載主要的 pod `master-0`：

    ```bash
    kubectl -n mssql-cluster expose pod master-0 --port=1533  --name=master-sql-0 --type=LoadBalancer
    ```

    取得所建立之 Kubernetes 服務的 IP：

    ```bash
    kubectl get services -n <namespaceName>
    ```

> [!IMPORTANT]
> 最佳做法是，藉由執行下列命令來刪除上面所建立的 Kubernetes 服務，以進行清除：
>
>```bash
>kubectl delete svc master-sql-0 -n mssql-cluster
>```

- 將資料庫新增至可用性群組。

    對於要加入 AG 的資料庫，它必須以完整復原模式執行，而且必須執行記錄備份。 使用上述所建立之 Kubernetes 服務的 IP，然後連接到 SQL Server 實例，接著執行 TSQL 語句，如下所示。

    ```sql
    ALTER DATABASE <databaseName> SET RECOVERY FULL;
    BACKUP DATABASE <databaseName> TO DISK='<filePath>'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE <databaseName>
    ```

    下列範例會加入已在實例上還原之名為 `sales` 的資料庫：

    ```sql
    ALTER DATABASE sales SET RECOVERY FULL;
    BACKUP DATABASE sales TO DISK='/var/opt/mssql/data/sales.bak'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE sales
    ```

## <a name="known-limitations"></a>已知限制

這些是大型資料叢集中 SQL Server 主機之可用性群組的已知問題和限制：

- 建立為非 `CREATE DATABASE` （例如 `RESTORE` `CREATE DATABASE FROM SNAPSHOT`）工作流程結果的資料庫不會自動加入至可用性群組。 [連接到實例](#instance-connect)，並手動將資料庫加入至可用性群組。
- 某些作業（例如使用 `sp_configure` 執行伺服器設定設定）需要連接到主要實例。 您不能使用對應的主要端點。 遵循[指示](#instance-connect)連接到 SQL Server 實例，並執行 `sp_configure`。
- 部署 BDC 時，必須建立高可用性設定。 部署後，您無法啟用可用性群組的高可用性設定。

## <a name="next-steps"></a>後續的步驟

- 如需在 big data cluster 部署中使用設定檔的詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md#configfile)。
- 如需 SQL Server 之可用性群組功能的詳細資訊，請參閱[Always On 可用性群組的總覽（SQL Server）](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2017)。
