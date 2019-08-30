---
title: Kubernetes 上的資料持續性
titleSuffix: SQL Server big data clusters
description: 了解資料持續性在 SQL Server 2019 巨量資料叢集中的運作方式。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7a12afd88f0eb83de7d5c5bd4a3735e71e037138
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155345"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>在 Kubernetes 上使用 SQL Server 2019 巨量資料叢集的資料持續性

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[永久性磁碟區](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) \(英文\) 提供外掛程式模型，可在 Kubernetes 中儲存。 提供儲存體的方式會從使用方式中擷取。 因此，您可以攜帶自己的高可用性儲存體，並將它插入 SQL Server 巨量資料叢集。 這可讓您完全掌控所需的儲存體類型、可用性和效能。 Kubernetes 支援各種類型的儲存體解決方案，包括 Azure 磁碟/檔案、NFS、本機儲存體等等。

## <a name="configure-persistent-volumes"></a>設定永久性磁碟區

SQL Server 巨量資料叢集耗用這些永久性磁碟區的方式是透過使用[儲存類別](https://kubernetes.io/docs/concepts/storage/storage-classes/) \(英文\)。 您可以針對不同類型的儲存體建立不同的儲存類別，並在巨量資料叢集部署時間指定它們。 您可以在集區層級設定要針對哪種目的使用的儲存類別和永久性磁碟區宣告大小。 SQL Server 巨量資料叢集會針對每個需要永久性磁碟區的元件，使用指定的儲存類別名稱建立[永久性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) \(英文\)。 然後，它會在 Pod 中裝載對應的永久性磁碟區。 

## <a name="configure-big-data-cluster-storage-settings"></a>設定巨量資料叢集儲存體設定

與其他自訂類似，您可以在部署時為每個集區和控制平面在叢集組態檔中指定儲存體設定。 如果集區規格中沒有任何儲存體組態設定，則會使用控制平面儲存體設定。 這是您可以包含在規格中的儲存體組態區段範例：

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

巨量資料叢集的部署將會使用永續性儲存體來儲存各種元件的資料、中繼資料和記錄。 您可以自訂在部署過程中建立的永久性磁碟區宣告大小。 建議的最佳做法是使用具有保留[回收原則](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy) \(英文\) 的儲存體類別。

> [!NOTE]
> 在 CTP 3.2 中，您無法修改部署後的儲存體組態設定。 此外，僅支援整個叢集的 `ReadWriteOnce` 存取模式。

> [!WARNING]
> 在沒有永續性儲存體的情況下執行可以在測試環境中運作，但是它可能會導致無法正常運作的叢集。 在 Pod 重新啟動時，叢集中繼資料和/或使用者資料將會永久遺失。 我們不建議您在此組態中執行。 

[設定儲存體](#config-samples)一節提供更多有關如何為您的 SQL Server 巨量資料叢集部署設定儲存體設定的範例。

## <a name="aks-storage-classes"></a>AKS 儲存體類別

AKS 隨附[兩個內建的儲存類別](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) \(部分機器翻譯\) **預設**和**受控 (進階)** ，以及適用於它們的動態佈建程式。 您可以指定其中一個，或建立您自己的儲存類別，以部署已啟用永續性儲存體的巨量資料叢集。 根據預設，aks *aks-dev-test* 的內建叢集組態檔會隨附永續性儲存體組態，以使用**預設**儲存類別。

> [!WARNING]
> 使用內建儲存類別**預設**和**受控 (進階)** 建立的永久性磁碟區具有「刪除」的回收原則。 因此，當您刪除 SQL Server 巨量資料叢集時，永久性磁碟區宣告也會遭到刪除，然後永久性磁碟區也是。 您可以使用 **azure-disk** 佈建程式搭配「保留」回收原則來建立自訂儲存類別，如[此文章](https://docs.microsoft.com/azure/aks/concepts-storage#storage-classes) \(英文\) 所示。


## <a name="minikube-storage-class"></a>Minikube 儲存類別

Minikube 隨附一個名為**標準**的內建儲存類別以及一個動態佈建程式。 Minikube *minikube-dev-test* 的內建組態檔具有控制平面規格中的儲存體組態設定。相同的設定將套用至所有集區規格。 您還可以自訂此檔案的複本，並將其用於 Minikube 上的巨量資料叢集部署。 您可以手動編輯自訂檔案，並變更特定集區的永久性磁碟區宣告大小，以配合您要執行的工作負載。 或者，如需如何使用 *azdata* 命令進行編輯的範例，請參閱[設定儲存體](#config-samples)一節。

## <a name="kubeadm-storage-classes"></a>Kubeadm 儲存體類別

Kubeadm 並未隨附內建的儲存類別。 您必須使用本機儲存體或偏好的佈建程式 (例如 [Rook](https://github.com/rook/rook)) 建立自己的儲存類別和永久性磁碟區。 在此情況下，您會將 **className** 設定為您所設定的儲存類別。 

> [!NOTE]
>  在 *kubeadm kubeadm-dev-test* 的內建部署組態檔中，不會為資料和記錄儲存體指定任何儲存類別名稱。 部署之前，您必須自訂組態檔並設定 className 的值，否則預先部署驗證將會失敗。 部署也具有驗證步驟，可檢查儲存類別是否存在，但不會針對必要的永久性磁碟區。 您必須確保根據叢集的規模建立足夠的磁碟區。 在 CTP 3.1 中，針對預設叢集大小，您必須建立至少 23 個磁碟區。 [以下](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)是如何使用本機佈建程式建立永久性磁碟區的範例。


## <a name="customize-storage-configurations-for-each-pool"></a>自訂每個集區的儲存體組態

針對所有自訂，您必須先建立您要使用的內建組態檔複本。 例如，下列命令在名為 `custom` 的子目錄中建立 *aks-dev-test* 部署組態檔的複本：

```bash
azdata bdc config init --source aks-dev-test --target custom
```

這會建立兩個檔案, 也就是可透過手動編輯來自訂的檔案 ( **bdc. json**和**control** ), 或者您可以使用**azdata bdc config**命令。 您可以使用 jsonpath 和 jsonpatch 程式庫的組合，以提供編輯組態檔的方式。


### <a id="config-samples"></a> 設定儲存類別名稱和/或宣告大小

根據預設，針對叢集中佈建的每個 Pod 所佈建的永久性磁碟區宣告大小為 10 GB。 在叢集部署之前，您可以更新此值，以容納您在自訂組態檔中執行的工作負載。

下列範例會將永久性磁碟區宣告大小的大小更新為 **control.jsaon** 中的 32Gi。 如果未在集區層級覆寫，則此設定將會套用至所有集區：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

下列範例顯示如何修改 **control.json** 檔案的儲存類別：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

另一個選項是手動編輯自訂組態檔，或使用 json 修補程式變更存放集區的儲存類別，如下列範例所示。 建立包含下列內容的 *patch.json* 檔案：

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

套用修補檔案。 使用 **azdata bdc config patch** 命令，將變更套用至 JSON 修補檔案。 下列範例會將 patch. json 檔案套用至目標部署組態檔自訂 json。

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>後續步驟

如需有關 Kubernetes 中磁碟區的完整文件，請參閱[磁碟區上的 Kubernetes 文件](https://kubernetes.io/docs/concepts/storage/volumes/) \(英文\)。

如需有關部署 SQL Server 巨量資料叢集的詳細資訊，請參閱[如何在 Kubernetes 上部署 SQL Server 巨量資料叢集](deployment-guidance.md)。

