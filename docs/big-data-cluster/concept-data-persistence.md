---
title: Kubernetes 上的資料持續性
titleSuffix: SQL Server big data clusters
description: 了解資料持續性在 SQL Server 2019 巨量資料叢集中的運作方式。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8a3ca863818d11471b0ae6aadd38458faf8b9daf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85661073"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-in-kubernetes"></a>在 Kubernetes 上使用 SQL Server 巨量資料叢集的資料持續性

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[永久性磁碟區](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) \(英文\) 為 Kubernetes 中的儲存體提供外掛程式模型。 在此模型中，提供儲存體的方式會從取用方式擷取。 因此，您可以攜帶自己的高可用性儲存體，並將它插入 SQL Server 巨量資料叢集。 這可讓您完全掌控所需的儲存體類型、可用性與效能。 Kubernetes 支援[各種類型的儲存體解決方案](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner) \(英文\)，包括 Azure 磁碟與檔案、網路檔案系統 (NFS)、本機儲存體。

## <a name="configure-persistent-volumes"></a>設定永久性磁碟區

SQL Server 巨量資料叢集透過使用[儲存類別](https://kubernetes.io/docs/concepts/storage/storage-classes/) \(英文\) 取用這些永久性磁碟區。 您可以針對不同類型的儲存體建立不同的儲存類別，並在巨量資料叢集部署時加以指定。 您可以在集區層級設定要針對特定目的使用的儲存類別與永久性磁碟區宣告大小。 SQL Server 巨量資料叢集會透過為每個需要永久性磁碟區的元件使用指定的儲存類別名稱，以建立[永久性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) \(英文\)， 並接著在 Pod 中裝載對應的永久性磁碟區 (或多個磁碟區)。 

以下是當您為巨量資料叢集規劃儲存體設定時需考慮的一些重要層面：

- 若要成功部署巨量資料叢集，請確定您有所需的永久性磁碟區數目可供使用。 若要在 Azure Kubernetes Service (AKS) 叢集上部署，而且使用內建儲存類別 (`default` 或 `managed-premium`)，則此類別均支援永久性磁碟區的動態佈建。 因此，您不需要預先建立永久性磁碟區，但必須確保 AKS 叢集中可用的背景工作角色節點，可以連接部署所需的永久性磁碟區數目。 根據為背景工作節點指定的 [VM 大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes)，每個節點都可連接特定數目的磁碟。 針對預設大小叢集 (沒有高可用性)，最少需要 24 個磁碟。 如果您要啟用高可用性或相應增加任何集區，則不論您要相應增加的資源為何，請確保每個額外的複本都有至少兩個永久性磁碟區。

- 如果您在設定中提供之儲存類別的儲存體佈建程式不支援動態佈建，您必須預先建立永久性磁碟區。 例如，`local-storage` 佈建程式不會啟用動態佈建。 如需如何在使用 `kubeadm` 部署的 Kubernetes 叢集中繼續進行的指引，請參閱此[範例指令碼](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) \(英文\)。

- 當您部署巨量資料叢集時，可以將相同的儲存類別設定為可供叢集中的所有元件使用。 但是，作為實際執行環境部署的最佳做法，各種元件都將需要不同的儲存體設定，以根據大小或輸送量來容納各種不同的工作負載。 您可以針對每個 SQL Server 主要執行個體、資料集與存放集區，覆寫控制器中指定的預設儲存體設定。 此文章提供如何執行此操作的範例。

- 計算存放集區大小需求時，必須考慮用來設定 HDFS 的複寫因子。  複寫因子可在部署時於叢集部署組態檔中進行設定。 開發/測試設定檔 (例如 `aks-dev-test` 或 `kubeadm-dev-test`) 的預設值為 2，至於針對生產環境部署建議的設定檔 (例如 `kubeadm-prod`)，其預設值為 3。 基於最佳做法，建議使用至少為 3 的 HDFS 複寫因子來設定巨量資料叢集生產環境部署。 複寫因子值會影響存放集區中的執行個體數目：基本上，您必須部署至少與複寫因子值一樣多的存放集區執行個體。 此外，必須據此調整儲存體的大小，並將在 HDFS 中複寫資料的次數計為與複寫因子值一樣多次。 您可在[這裡](https://hadoop.apache.org/docs/r3.2.1/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Data_Replication)深入了解 HDFS 中的資料複寫。 

- 從 SQL Server 2019 CU1 版本開始，您就無法修改部署後的儲存體組態設定。 此限制不僅可以防止您在部署後修改每個執行個體的永久性磁碟區宣告大小，還可以防止您執行範圍調整作業。 因此，在部署巨量資料叢集之前，請務必先規劃儲存體配置。

- 透過在 Kubernetes 上部署為容器化應用程式，以及透過使用具狀態集合與永續性儲存體等功能，Kubernetes 可確保 Pod 會在發生健康情況問題時重新啟動，並連接到相同的永續性儲存體。 但萬一節點失敗，而且必須在另一個節點上重新啟動 Pod，如果儲存體位於失敗節點的本機，則會提高無法使用的風險。 為了降低此風險，您必須設定其他備援，並啟用[高可用性功能](deployment-high-availability.md)或使用遠端備援儲存體。 以下概觀適用於巨量資料叢集中各種元件的儲存體選項：

| 資源 | 資料的儲存類型 | 記錄的儲存類型 |  注意 |
|---|---|---|--|
| SQL Server 主要執行個體 | 本機 (複本>=3) 或遠端備援儲存體 (複本=1) | 本機儲存體 | 以具狀態集合為基礎的實作，其中繫結到節點的 Pod 可確保重新啟動，而且暫時性失敗將不會造成資料遺失。 |
| 計算集區 | 本機儲存體 | 本機儲存體 | 未儲存任何使用者資料。 |
| 資料集區 | 本機/遠端備援儲存體 | 本機儲存體 | 若無法從其他資料來源重建資料集區，請使用遠端備援儲存體。  |
| 存放集區 (HDFS) | 本機/遠端備援儲存體 | 本機儲存體 | 已啟用 HDFS 複寫。 |
| Spark 集區 | 本機儲存體 | 本機儲存體 | 未儲存任何使用者資料。 |
| 控制項 (controldb、metricsdb、logsdb)| 遠端備援儲存體 | 本機儲存體 | 針對巨量資料叢集中繼資料使用儲存體層級備援非常重要。 |

> [!IMPORTANT]
> 請確定控制項相關元件均位於遠端備援儲存體裝置上。 `controldb-0` Pod 會裝載 SQL Server 執行個體，該執行個體具有儲存下列項目的資料庫：與叢集服務狀態、各種設定以及其他相關資訊相關的所有中繼資料。 如果此執行個體變成無法使用，將導致叢集中的其他相依服務發生健康情況問題。

## <a name="configure-big-data-cluster-storage-settings"></a>設定巨量資料叢集儲存體設定

如同其他自訂，您可以在部署時為 `bdc.json` 設定檔中的每個集區，以及 `control.json` 檔案中的控制項服務，在叢集設定檔中指定儲存體設定。 若集區規格中沒有任何儲存體組態設定，則會將控制項儲存體設定用於所有其他元件，包括 SQL Server 主機 (`master` 資源)、HDFS (`storage-0` 資源) 與資料集區元件。 下列程式碼範例代表您可以包含在規格中的儲存體組態區段：

```json
    "storage": 
    {
      "data": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
    }
```

巨量資料叢集的部署會使用永續性儲存體來儲存各種元件的資料、中繼資料與記錄。 您可以自訂在部署過程中建立的永久性磁碟區宣告大小。 建議的最佳做法是使用具有保留  [回收原則](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy) \(英文\) 的儲存類別。

> [!WARNING]
> 在沒有永續性儲存體的情況下執行可以在測試環境中運作，但是它可能會導致無法正常運作的叢集。 在 Pod 重新啟動時，叢集中繼資料和/或使用者資料會永久遺失。 建議不要在此設定下執行。

[設定儲存體](#config-samples)一節提供更多有關如何為您的 SQL Server 巨量資料叢集部署設定儲存體設定的範例。

## <a name="aks-storage-classes"></a>AKS 儲存體類別

AKS 隨附[兩個內建的儲存類別](/azure/aks/azure-disks-dynamic-pv/) `default` 與 `managed-premium`，以及其所適用的動態佈建程式。 您可以指定其中一個，或建立您自己的儲存類別，以部署已啟用永續性儲存體的巨量資料叢集。 根據預設，AKS `aks-dev-test` 的內建叢集設定檔會隨附永續性儲存體設定，以使用 `default` 儲存類別。

> [!WARNING]
> 使用內建儲存類別 `default` 和 `managed-premium` 建立的永續性磁碟區具有「刪除」  的回收原則。 因此，當您刪除 SQL Server 巨量資料叢集時，永久性磁碟區宣告會遭到刪除，然後永久性磁碟區也是。 您可以透過使用 `azure-disk` 佈建程式搭配 `Retain` 回收原則來建立自訂儲存類別，如[概念儲存體](/azure/aks/concepts-storage/#storage-classes)中所述。

## <a name="storage-classes-for-kubeadm-clusters"></a>`kubeadm` 叢集的儲存類別 

使用 `kubeadm` 部署的 Kubernetes 叢集沒有內建的儲存類別。 您必須透過使用本機儲存體或您[偏好的儲存體佈建程式](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner) \(英文\) 建立自己的儲存類別與永久性磁碟區。 在該情況下，您會將 `className` 設定為您所設定的儲存類別。

> [!IMPORTANT]
>  在適用於 kubeadm (`kubeadm-dev-test` 與 `kubeadm-prod`) 的內建部署設定檔中，不會為資料與記錄儲存體指定任何儲存類別名稱。 部署之前，您必須自訂設定檔並設定 `className` 的值。 否則，部署前驗證將會失敗。 部署也具有驗證步驟，可檢查儲存類別是否存在，但不會針對必要的永久性磁碟區。 務必根據叢集規模建立足夠的磁碟區。 針對預設的最小叢集大小 (預設規模，沒有高可用性)，您至少必須建立 24 個永續性磁碟區。 如需如何使用本機佈建程式來建立永久性磁碟區的範例，請參閱[使用 Kubeadm 建立 Kubernetes 叢集](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) \(英文\)。

## <a name="customize-storage-configurations-for-each-pool"></a>自訂每個集區的儲存體組態

針對所有自訂，您必須先建立您要使用的內建設定檔複本。 例如，下列命令會在名為 `custom` 的子目錄中建立 `aks-dev-test` 部署設定檔的複本：

```bash
azdata bdc config init --source aks-dev-test --target custom
```

此程序會建立兩個檔案，`bdc.json` 和 `control.json`，您可以手動編輯它們或透過使用 `azdata bdc config` 命令來加以自訂。 您可以使用 jsonpath 和 jsonpatch 程式庫的組合，以提供編輯組態檔的方式。


### <a name="configure-storage-class-name-andor-claims-size"></a><a id="config-samples"></a> 設定儲存類別名稱和/或宣告大小

根據預設，針對叢集中佈建的每個 Pod 所佈建的永久性磁碟區宣告大小為 10 GB。 在部署叢集之前，您可以更新此值，以容納您在自訂設定檔中執行的工作負載。

在下列範例中，永久性磁碟區宣告的大小會在 `control.json` 中更新為 32 GB。 如果未在集區層級加以覆寫，則此設定將會套用至所有集區。

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

下列範例示範如何修改 `control.json` 檔案的儲存類別：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

您也可以選擇手動編輯自訂設定檔，或使用 json 修補程式變更存放集區的儲存類別，如下列範例所示：

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.resources.storage-0.spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
            "data":{
                    "size": "100Gi",
                    "className": "myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    },
            "logs":{
                    "size":"32Gi",
                    "className":"myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    }
                }
            }
        }
    ]
}
```

套用修補檔案。 使用 `azdata bdc config patch` 命令，在 .json 修補檔中套用變更。 下列範例會將 `patch.json` 檔案套用至目標部署設定檔 `custom.json`：

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>後續步驟

- 如需有關 Kubernetes 中磁碟區的完整文件，請參閱[Kubernetes 磁碟區文件](https://kubernetes.io/docs/concepts/storage/volumes/) \(英文\)。

- 如需有關部署 SQL Server 巨量資料叢集的詳細資訊，請參閱[如何在 Kubernetes 上部署 SQL Server 巨量資料叢集](deployment-guidance.md)。
