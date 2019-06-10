---
title: 在 Kubernetes 上的資料持續性
titleSuffix: SQL Server big data clusters
description: 深入了解資料持續性中的 SQL Server 2019 巨量資料叢集的運作方式。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 24c90bfb8c99178e8ffa7822fba4bea709c536e1
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800723"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>在 Kubernetes 上的 SQL Server 巨量資料叢集使用的資料持續性

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[永續性磁碟區](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)提供在 Kubernetes 中的儲存體外掛程式模型。 從使用方式是抽離提供儲存體的方式。 因此，您可以將高度可用的儲存體，並插入 SQL Server 的巨量資料叢集。 這可讓您完整控制的儲存體、 可用性和效能，您需要的類型。 Kubernetes 支援多種不同的儲存體解決方案，包括 Azure 的磁碟檔案、 NFS、 本機儲存體，和更多功能。

## <a name="configure-persistent-volumes"></a>設定永續性磁碟區

SQL Server 的巨量資料叢集會取用這些永續性磁碟區的方式是使用[儲存類別](https://kubernetes.io/docs/concepts/storage/storage-classes/)。 您可以建立不同的儲存體類別，用於不同種類的儲存體，並在巨量資料叢集部署期間指定它們。 您可以設定哪一個儲存體類別和永續性磁碟區宣告大小，可用於在集區層級的用途。 SQL Server 的巨量資料叢集會建立[永續性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)需要永續性磁碟區每個元件的指定儲存體類別名稱。 然後，它會裝載 pod 中對應的永續性磁碟區。 

## <a name="configure-big-data-cluster-storage-settings"></a>巨量資料叢集儲存體設定

類似於其他自訂項目，您可以指定儲存體設定的叢集組態檔中在部署期間，每個集區和控制平面。 如果有任何儲存體組態設定，在集區規格中，則會使用控制平面儲存體設定。 這是您可以包含在規格中的儲存體組態區段的範例：

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

部署巨量資料叢集會使用永續性儲存體來儲存資料、 中繼資料和各種元件的記錄檔。 您可以自訂部署的過程中建立的永續性磁碟區宣告的大小。 最佳做法，我們建議使用儲存體類別*保留*[收回原則](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)。

> [!NOTE]
> 在 CTP 3.0 中，您無法修改儲存體組態設定後部署。 此外，只有`ReadWriteOnce`支援整個叢集的存取模式。

> [!WARNING]
> 執行而永續性儲存體不能在測試環境中，但它可能會導致非功能性的叢集。 在 pod 重新啟動時，叢集中繼資料及/或使用者資料會永久遺失。 我們不建議在此組態中執行。 

[設定儲存體](#config-samples)章節提供有關如何設定 SQL Server 的巨量資料叢集部署的儲存體設定的更多範例。

## <a name="aks-storage-classes"></a>AKS 儲存類別

AKS 隨附[兩個內建的儲存體類別](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)**預設**並**管理 premium**以及它們的動態佈建程式。 您可以指定這些，或建立您自己的儲存類別啟用永續性儲存體，以部署巨量資料叢集。 根據預設，內建在 aks 叢集組態檔*aks-dev-test.json*隨附應使用的永續性儲存體組態**預設**儲存類別。

> [!WARNING]
> 使用內建的儲存體類別建立永續性磁碟區**預設**並**管理 premium**擁有的收回原則*刪除*。 時，您可以刪除 SQL Server 巨量資料叢集，因此永續性磁碟區宣告會取得已刪除，然後永續性磁碟區。 您可以建立使用自訂的儲存體類別**azure 磁碟**使用 privioner*保留*收回原則中所示[這](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes)文章。


## <a name="minikube-storage-class"></a>Minikube 儲存類別

Minikube 隨附內建的儲存體類別，稱為**標準**以及它的動態佈建程式。 內建的組態檔。 minikube *minikube-dev-test.json*控制平面規格中有儲存體組態設定。相同的設定會套用至所有的集區規格中。 您也可以自訂此檔案的複本，並將它用於您的巨量資料叢集部署，在 minikube。 您可以手動編輯自訂檔案，並變更您想要執行的永續性磁碟區宣告以容納工作負載的特定集區的大小。 或者，請參閱[設定存放裝置](#config-samples)如需有關如何執行範例的區段可讓您編輯使用*mssqlctl*命令。

## <a name="kubeadm-storage-classes"></a>Kubeadm 儲存類別

Kubeadm 並未隨附於內建的儲存體類別。 您必須建立您自己的儲存體類別和永續性磁碟區，使用本機儲存體或您慣用的佈建程式，例如[城堡](https://github.com/rook/rook)。 在此情況下，您會設定**className**為您設定的儲存類別。 

> [!NOTE]
>  在 內建部署的組態檔中*kubeadm kubeadm 開發 test.json*沒有未指定的資料和記錄的儲存體的儲存體類別名稱。 再進行部署，您必須自訂設定檔，並設定的 className 否則將會失敗的部署前驗證的值。 部署也會有驗證步驟，以檢查存在的儲存體類別，而不是必要的永續性磁碟區。 您必須確定您建立足夠的磁碟區，視您的叢集的規模而定。 在 CTP 3.0 中，做為預設叢集大小您必須建立至少 23 的磁碟區。 [這裡](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)範例說明如何建立使用本機的佈建程式的永續性磁碟區。


## <a name="customize-storage-configurations-for-each-pool"></a>自訂每個集區的儲存體設定

對於所有的自訂項目，您必須先建立一份內建在您想要使用的組態檔中。 例如，下列命令會建立一份*aks-dev-test.json*目前目錄中的部署設定檔：

```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```

然後，您可以藉由手動編輯自訂組態檔，或者您可以使用*mssqlctl 叢集組態區段組*命令。 此 set 命令會使用一組 jsonpath 和 jsonpatch 程式庫提供的方式來編輯設定檔。

### <a name="configure-size"></a>設定大小

根據預設，每個叢集中佈建的 pod 佈建永續性磁碟區宣告的大小為 10 GB。 您可以更新此值可容納您正在叢集部署之前自訂的組態檔中的工作負載。

下列範例只會更新儲存在 100 Gi 儲存集區中資料的永續性磁碟區宣告的大小。 請注意儲存體 區段必須存在於存放集區的組態檔，然後再執行此命令：

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.size=100Gi"
```

下列範例會更新為 32 Gi 的永續性磁碟區宣告所有集區的大小：

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.storage.data.size=32Gi"
```

### <a id="config-samples"></a> 設定儲存體類別

下列範例示範如何修改控制平面的儲存體類別：

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.storage.data.className=<yourStorageClassName>"
```

另一個選項是手動編輯自訂組態檔，或在下列範例中，以變更存放集區的儲存體類別使用 jsonpatch 等。 建立*patch.json*使用此內容的檔案：

```json
{
  "patch": [
    {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage",
      "value": {
          "data": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
      }
  ]
}
```

套用修補檔案。 使用*mssqlctl 叢集組態區段組*命令，以套用 JSON 修補程式檔案中的變更。 下列範例適用於目標部署組態檔案 custom.json patch.json 檔案。

```bash
mssqlctl cluster config section set -c custom.json -p ./patch.json
```

## <a name="next-steps"></a>後續步驟

如需在 Kubernetes 中的磁碟區的完整文件，請參閱 <<c0> [ 磁碟區上的 Kubernetes 文件](https://kubernetes.io/docs/concepts/storage/volumes/)。

如需部署 SQL Server 的巨量資料叢集的詳細資訊，請參閱 <<c0> [ 如何部署巨量資料叢集的 Kubernetes 的 SQL Server](deployment-guidance.md)。

