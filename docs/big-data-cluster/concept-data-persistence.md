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
ms.openlocfilehash: 87f0e82d0e12656bb7a06be1951874b656dbf4b0
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532394"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>在 Kubernetes 上使用 SQL Server 2019 巨量資料叢集的資料持續性

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[永久性磁碟區](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) \(英文\) 提供外掛程式模型，可在 Kubernetes 中儲存。 提供儲存體的方式會從使用方式中擷取。 因此，您可以攜帶自己的高可用性儲存體，並將它插入 SQL Server 巨量資料叢集。 這可讓您完全掌控所需的儲存體類型、可用性和效能。 Kubernetes 支援各種類型的儲存體解決方案，包括 Azure 磁碟/檔案、NFS、本機儲存體等等。

## <a name="configure-persistent-volumes"></a>設定永久性磁碟區

SQL Server 巨量資料叢集耗用這些永久性磁碟區的方式是透過使用[儲存類別](https://kubernetes.io/docs/concepts/storage/storage-classes/) \(英文\)。 您可以針對不同類型的儲存體建立不同的儲存類別，並在巨量資料叢集部署時間指定它們。 您可以在集區層級設定要針對哪種目的使用的儲存類別和永久性磁碟區宣告大小。 SQL Server 巨量資料叢集會針對每個需要永久性磁碟區的元件，使用指定的儲存類別名稱建立[永久性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) \(英文\)。 然後，它會在 Pod 中裝載對應的永久性磁碟區。 

以下是當您為巨量資料叢集規劃儲存體設定時需考慮的一些重要層面：

- 若要成功部署巨量資料叢集，您必須確定有所需的永續性磁碟區數目可供使用。 如果您要在 AKS 叢集上部署，而且使用的是其中一個內建的儲存類別 (`default` 或 `managed-premium`)，則這些均支援針對永續性磁碟區進行動態佈建。 這表示您不需要預先建立永續性磁碟區，但必須確保 AKS 叢集中可用的背景工作節點，可連接與部署所需之永續性磁碟區一樣多的磁碟。 根據為背景工作節點指定的 [VM 大小](/azure/virtual-machines/linux/sizes/)，每個節點都可連接特定數目的磁碟。 針對預設大小叢集 (沒有高可用性)，最少需要 24 個磁碟。 如果您要啟用高可用性或相應增加任何集區，則不論您要相應增加的資源為何，都必須確保每個額外的複本最少有兩個永續性磁碟區。

- 如果您在設定中提供之儲存類別的儲存體佈建程式不支援動態佈建，您必須預先建立永續性磁碟區。 例如，`local-storage` 佈建程式不會啟用動態佈建。 請參閱此[範例指令碼](https://github.com/microsoft/sql-server-samples/tree/cu1-bdc/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) \(英文\)，以了解如何在使用 `kubeadm` 部署的 Kubernetes 叢集中執行此操作。

- 當您部署巨量資料叢集時，可以將相同的儲存類別設定為可供叢集中的所有元件使用。 但是，作為實際執行環境部署的最佳做法，各種元件都將需要不同的儲存體設定，以根據大小或輸送量來容納各種不同的工作負載。 您可以針對每個 SQL Server 主要執行個體、資料及存放集區，覆寫控制器中指定的預設儲存體設定。 此文章提供如何執行此操作的範例。

- 從 SQL Server 2019 CU1 版本開始，您無法修改部署後的儲存體組態設定。 這包括完全無法修改每個執行個體的永續性磁碟區宣告大小，而且也不支援部署後的範圍調整作業。 因此，請務必在巨量資料叢集之前規劃儲存配置。

- 藉由在 Kubernetes 上部署為容器化應用程式，以及使用具狀態集合和永續性儲存體等功能，Kubernetes 確保 Pod 會在發生健康情況問題時重新開機，並連接到相同的永續性儲存體。 但萬一節點失敗，而且必須在另一個節點上重新啟動 Pod，如果儲存體位於失敗節點的本機，則會提高無法使用的風險。 為了克服此風險，您必須設定額外的備援，並啟用[高可用性功能](deployment-high-availability.md)或使用遠端備援儲存體。 以下概述適用於巨量資料叢集中各種元件的儲存體選項。

| 資源 | 資料的儲存類型 | 記錄的儲存類型 |  注意 |
|---|---|---|--|
| SQL Server 主要執行個體 | 本機 (複本>=3) 或遠端備援儲存體 (複本=1) | 本機儲存體 | 以具狀態集合為基礎的實作，確保停留在節點上的 Pod 將會重新啟動，而暫時性失敗將不會造成資料遺失。 |
| 計算集區 | 本機儲存體* | 本機儲存體 | 未儲存任何使用者資料。 |
| 資料集區 | 本機/遠端備援儲存體 | 本機儲存體 | 如果無法從其他資料來源重建資料集區，請使用遠端備援儲存體。  |
| 存放集區 (HDFS) | 本機/遠端備援儲存體 | 本機儲存體 | 已啟用 HDFS 複寫。 |
| Spark 集區 | 本機儲存體* | 本機儲存體 | 未儲存任何使用者資料。 |
| 控制項 (controldb、metricsdb、logsdb)| 遠端備援儲存體 | 本機儲存體 | 針對巨量資料叢集中繼資料使用儲存體層級備援非常重要。 |

> [!IMPORTANT]
> 您必須確定控制項相關元件均位於遠端備援儲存體上。 `controldb-0` Pod 會裝載一個 SQL Server 執行個體，其中包含儲存所有叢集服務狀態、各種設定等相關中繼資料的資料庫。無法使用這個執行個體，將導致叢集中的其他相依服務發生健康情況問題。

## <a name="configure-big-data-cluster-storage-settings"></a>設定巨量資料叢集儲存體設定

與其他自訂類似，您可以在部署時，為 `bdc.json` 設定檔中的每個集區，以及 `control.json` 檔案中的控制項服務，在叢集設定檔中指定儲存體設定。 如果集區規格中沒有任何儲存體組態設定，則會將控制項儲存體設定用於所有其他元件，包括 SQL Server master (`master` 資源)、HDFS (`storage-0` 資源) 或資料集區。 這是您可以包含在規格中的儲存體組態區段範例：

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

巨量資料叢集的部署將會使用永續性儲存體來儲存各種元件的資料、中繼資料和記錄。 您可以自訂在部署過程中建立的永久性磁碟區宣告大小。 建議的最佳做法是使用具有保留  [回收原則](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy) \(英文\) 的儲存體類別。

> [!WARNING]
> 在沒有永續性儲存體的情況下執行可以在測試環境中運作，但是它可能會導致無法正常運作的叢集。 在 Pod 重新啟動時，叢集中繼資料和/或使用者資料將會永久遺失。 我們不建議您在此組態中執行。 

[設定儲存體](#config-samples)一節提供更多有關如何為您的 SQL Server 巨量資料叢集部署設定儲存體設定的範例。

## <a name="aks-storage-classes"></a>AKS 儲存體類別

AKS 隨附[兩個內建的儲存類別](/azure/aks/azure-disks-dynamic-pv/) `default` 和 `managed-premium`，以及適用於它們的動態佈建程式。 您可以指定其中一個，或建立您自己的儲存類別，以部署已啟用永續性儲存體的巨量資料叢集。 根據預設，aks `aks-dev-test` 的內建叢集設定檔會隨附永續性儲存體設定，以使用 `default` 儲存類別。

> [!WARNING]
> 使用內建儲存類別 `default` 和 `managed-premium` 建立的永續性磁碟區具有「刪除」  的回收原則。 因此，當您刪除 SQL Server 巨量資料叢集時，永久性磁碟區宣告也會遭到刪除，然後永久性磁碟區也是。 您可以使用 `azure-disk` 佈建程式搭配 `Retain` 回收原則來建立自訂儲存類別，如[此](/azure/aks/concepts-storage/#storage-classes)文章所示。

## <a name="storage-classes-for-kubeadm-clusters"></a>`kubeadm` 叢集的儲存類別 

使用 `kubeadm` 部署的 Kubernetes 叢集沒有內建的儲存類別。 您必須使用本機儲存體或偏好的佈建程式 (例如 [Rook](https://github.com/rook/rook)) 建立自己的儲存類別和永久性磁碟區。 在此情況下，您會將 `className` 設定為您所設定的儲存類別。 

> [!NOTE]
>  在適用於 kubeadm (`kubeadm-dev-test` 或 `kubeadm-prod`) 的內建部署設定檔中，不會為資料和記錄儲存體指定任何儲存類別名稱。 部署之前，您必須自訂組態檔並設定 className 的值，否則預先部署驗證將會失敗。 部署也具有驗證步驟，可檢查儲存類別是否存在，但不會針對必要的永久性磁碟區。 您必須確保根據叢集的規模建立足夠的磁碟區。 針對預設的最小叢集大小 (預設規模，沒有高可用性)，您至少必須建立 24 個永續性磁碟區。 [以下](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)是如何使用本機佈建程式建立永久性磁碟區的範例。


## <a name="customize-storage-configurations-for-each-pool"></a>自訂每個集區的儲存體組態

針對所有自訂，您必須先建立您要使用的內建組態檔複本。 例如，下列命令會在名為 `custom` 的子目錄中建立 `aks-dev-test` 部署設定檔的複本：

```bash
azdata bdc config init --source aks-dev-test --target custom
```

這會建立兩個檔案 `bdc.json` 和 `control.json`，您可以藉由手動編輯它們或使用 `azdata bdc config` 命令來自訂。 您可以使用 jsonpath 和 jsonpatch 程式庫的組合，以提供編輯組態檔的方式。


### <a id="config-samples"></a> 設定儲存類別名稱和/或宣告大小

根據預設，針對叢集中佈建的每個 Pod 所佈建的永久性磁碟區宣告大小為 10 GB。 在叢集部署之前，您可以更新此值，以容納您在自訂組態檔中執行的工作負載。

下列範例會在 `control.json` 中，將永續性磁碟區宣告大小的大小更新為 32Gi。 如果未在集區層級覆寫，則此設定將會套用至所有集區：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

下列範例示範如何修改 `control.json` 檔案的儲存類別：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

另一個選項是手動編輯自訂組態檔，或使用 json 修補程式變更存放集區的儲存類別，如下列範例所示。 建立包含下列內容的 `patch.json` 檔案：

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

套用修補檔案。 使用 `azdata bdc config patch` 命令，在 JSON 修補檔中套用變更。 下列範例會將 `patch.json` 檔案套用至目標部署設定檔 `custom.json`。

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>後續步驟

如需有關 Kubernetes 中磁碟區的完整文件，請參閱[磁碟區上的 Kubernetes 文件](https://kubernetes.io/docs/concepts/storage/volumes/) \(英文\)。

如需有關部署 SQL Server 巨量資料叢集的詳細資訊，請參閱[如何在 Kubernetes 上部署 SQL Server 巨量資料叢集](deployment-guidance.md)。
