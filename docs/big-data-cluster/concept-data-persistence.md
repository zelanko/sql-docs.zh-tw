---
title: Kubernetes 上的資料持續性
titleSuffix: SQL Server big data clusters
description: 瞭解資料持續性在 SQL Server 2019 big data 叢集中的運作方式。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9142836032acc5e302c947e1619d17b07faff683
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419467"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>在 Kubernetes 上使用 SQL Server big data cluster 的資料持續性

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[持續性磁片](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)區提供儲存在 Kubernetes 中的外掛程式模型。 提供儲存體的方式會從使用方式中抽象化。 因此, 您可以攜帶自己的高可用性儲存體, 並將它插入 SQL Server big data 叢集。 這可讓您完全掌控所需的儲存體、可用性和效能類型。 Kubernetes 支援各種類型的儲存體解決方案, 包括 Azure 磁片/檔案、NFS、本機儲存體等等。

## <a name="configure-persistent-volumes"></a>設定持續性磁片區

SQL Server big data 叢集耗用這些持續性磁片區的方式是使用[儲存類別](https://kubernetes.io/docs/concepts/storage/storage-classes/)。 您可以針對不同類型的儲存體建立不同的存放裝置類別, 並在 big data cluster 部署時間指定它們。 您可以設定要在集區層級使用哪個儲存類別和持續性磁片區宣告大小來做為目標。 SQL Server big data 叢集會針對每個需要持續性磁片區的元件, 建立具有指定之儲存類別名稱的[持續性磁片區宣告](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)。 然後, 它會在 pod 中掛接對應的持續性磁片區。 

## <a name="configure-big-data-cluster-storage-settings"></a>設定 big data 叢集儲存設定

類似于其他自訂專案, 您可以在部署期間, 針對每個集區和控制平面指定叢集設定檔中的存放裝置設定。 如果集區規格中沒有任何存放裝置設定, 則會使用控制平面儲存設定。 這是您可以包含在規格中的儲存體設定區段範例:

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

大型資料叢集的部署將會使用持續性儲存體來儲存各種元件的資料、中繼資料和記錄。 您可以自訂在部署過程中建立的持續性磁片區宣告大小。 建議的最佳作法是使用具有*保留*[回收原則](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)的儲存體類別。

> [!NOTE]
> 在 CTP 3.2 中, 您無法修改部署後的存放裝置設定。 此外, 只`ReadWriteOnce`支援整個叢集的存取模式。

> [!WARNING]
> 執行時若沒有持續性儲存區, 可以在測試環境中運作, 但可能會導致無法正常運作的叢集。 當 pod 重新開機時, 叢集中繼資料和/或使用者資料將會永久遺失。 我們不建議您在此設定中執行。 

[設定儲存體](#config-samples)一節提供更多有關如何為您的 SQL Server big data cluster 部署設定存放裝置設定的範例。

## <a name="aks-storage-classes"></a>AKS 儲存體類別

AKS 隨附[兩個內建的儲存類別](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)**預設**和**受控-premium** , 以及適用于它們的動態布建程式。 您可以指定其中一個, 或建立您自己的儲存體類別, 以部署已啟用持續性儲存區的 big data 叢集。 根據預設, aks *aks-開發/測試*的內建叢集設定檔會隨附持續性儲存體設定, 以使用**預設**儲存類別。

> [!WARNING]
> 使用內建存放裝置類別**預設**和**受控-premium**建立的持續性磁片區具有*刪除*的回收原則。 因此, 當您刪除 SQL Server big data 叢集時, 持續性磁片區宣告也會遭到刪除, 然後再進行永久磁片區。 您可以使用具有*保留*回收原則的**azure 磁片**privioner 來建立自訂儲存類別, 如[本文](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes)所示。


## <a name="minikube-storage-class"></a>Minikube 儲存類別

Minikube 隨附內建的儲存類別, 名為**standard** , 還有動態布建程式。 Minikube *minikube-開發/測試*的內建設定檔具有控制平面規格中的存放裝置設定。相同的設定將會套用至所有集區規格。 您也可以自訂此檔案的複本, 並在 minikube 上將它用於您的 big data cluster 部署。 您可以手動編輯自訂檔案, 並變更特定集區的持續性磁片區宣告大小, 以配合您要執行的工作負載。 或者, 如需如何使用*azdata*命令進行編輯的範例, 請參閱[設定儲存體](#config-samples)一節。

## <a name="kubeadm-storage-classes"></a>Kubeadm 儲存體類別

Kubeadm 並未隨附內建的儲存類別。 您必須使用本機儲存體或慣用的布建程式 (例如[城堡](https://github.com/rook/rook)) 來建立自己的儲存體類別和持續性磁片區。 在此情況下, 您會將**className**設定為您所設定的儲存類別。 

> [!NOTE]
>  在*kubeadm kubeadm*的內建部署設定檔案中, 不會為數據和記錄儲存體指定任何儲存類別名稱。 部署之前, 您必須自訂設定檔並設定 className 的值, 否則預先部署驗證將會失敗。 部署也具有驗證步驟, 可檢查儲存類別是否存在, 但不會針對必要的持續性磁片區。 您必須根據叢集的規模, 確保建立足夠的磁片區。 在 CTP 3.1 中, 針對預設叢集大小, 您必須建立至少23個磁片區。 [以下](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)是如何使用本機布建程式建立持續性磁片區的範例。


## <a name="customize-storage-configurations-for-each-pool"></a>自訂每個集區的存放裝置設定

針對所有自訂專案, 您必須先建立您要使用的內建設定檔案複本。 例如, 下列命令會在名為`custom`的子目錄中建立*aks-開發/測試*部署設定檔的複本:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

這會建立兩個檔案, 也就是可透過手動編輯來自訂的檔案, 也可以使用**azdata bdc config**命令。 您可以使用 jsonpath 和 jsonpatch 程式庫的組合, 以提供編輯設定檔的方式。


### <a id="config-samples"></a>設定存放裝置類別名稱和/或宣告大小

根據預設, 針對在叢集中布建的每個 pod 布建的持續性磁片區宣告大小為 10 GB。 在叢集部署之前, 您可以更新此值, 以容納您在自訂設定檔中執行的工作負載。

下列範例會將持續性磁片區宣告大小的大小更新為**jsaon**中的32Gi。 如果未在集區層級覆寫, 此設定將會套用至所有集區:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

下列範例顯示如何修改**control. json**檔案的儲存類別:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

另一個選項是手動編輯自訂設定檔, 或使用 json 修補程式, 如下列範例所示, 其中會變更存放集區的儲存類別。 建立包含下列內容的*patch. json*檔案:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage"
      "value": {
          "type":"Storage",
          "replicas":2,
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

套用修補檔案。 使用**azdata bdc 設定修補程式**命令, 將變更套用至 JSON 修補程式檔案。 下列範例會將 patch. json 檔案套用至目標部署設定檔自訂 json。

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>後續步驟

如需 Kubernetes 中磁片區的完整檔, 請參閱[磁片區上的 Kubernetes 檔](https://kubernetes.io/docs/concepts/storage/volumes/)。

如需有關部署 SQL Server big data 叢集的詳細資訊, 請參閱[如何在 Kubernetes 上部署 SQL Server big data](deployment-guidance.md)叢集。

