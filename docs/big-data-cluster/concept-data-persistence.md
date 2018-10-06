---
title: 使用巨量資料叢集的 Kubernetes 的 SQL Server 的資料持續性 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 629d7fd887e96013b17a5686ce82eb966044f240
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48796204"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>在 Kubernetes 上的 SQL Server 巨量資料叢集使用的資料持續性

[永續性磁碟區](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)提供外掛程式模型，在其中儲存體提供的方式的 Kubernetes 中的儲存體便完成取自的使用方式。 因此，您可以將高度可用的儲存體，並插入 SQL Server 的巨量資料叢集叢集。 這可讓您完整控制的儲存體、 可用性和效能，您需要的類型。 Kubernetes 支援多種不同的儲存體解決方案，包括 Azure 的磁碟檔案、 NFS、 本機儲存體，和更多功能。

## <a name="configure-persistent-volumes"></a>設定永續性磁碟區

SQL Server 巨量資料叢集會使用這些永續性磁碟區的方式是使用[儲存類別](https://kubernetes.io/docs/concepts/storage/storage-classes/)。 您可以建立不同的儲存體類別，用於不同種類的儲存體，並在巨量資料叢集部署期間指定它們。 您可以設定的儲存體来使用類別用途 （集區）。 SQL Server 的巨量資料叢集會建立[永續性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)與每個 pod，需要永續性磁碟區的指定儲存體類別名稱。 然後，它會裝載 pod 中對應的永續性磁碟區。

> [!NOTE]
> CTP 2.0，只有`ReadWriteOnce`支援整個叢集的存取模式。

## <a name="deployment-settings"></a>部署設定

若要在部署期間使用永續性儲存體，請設定**USE_PERSISTENT_VOLUME**並**STORAGE_CLASS_NAME**環境變數，再執行`mssqlctl create cluster`命令。 **USE_PERSISTENT_VOLUME**設為`true`預設。 您可以覆寫預設值，並將它設定為`false`和巨量資料的 SQL Server 叢集在此情況下，使用 emptyDir 掛接。 

> [!WARNING]
> 執行而永續性儲存體不會導致非功能性的叢集。 在 pod 重新啟動時，叢集中繼資料及/或使用者資料會永久遺失。

如果您設定旗標設為 true 時，您也必須提供**STORAGE_CLASS_NAME**做為參數，在部署階段。

## <a name="aks-storage-classes"></a>AKS 儲存類別

AKS 隨附[兩個內建的儲存體類別](https://docs.microsoft.com/en-us/azure/aks/azure-disks-dynamic-pv)**預設**並**進階儲存體**以及它們的動態佈建程式。 您可以指定這些，或建立您自己的儲存類別啟用永續性儲存體，以部署巨量資料叢集。

## <a name="minikube-storage-class"></a>Minikube 儲存類別

Minikube 隨附內建的儲存體類別，稱為**標準**以及它的動態佈建程式。

## <a name="kubeadm"></a>Kubeadm

Kubeadm 並未隨附於內建的儲存體類別;因此，我們建立了指令碼，以設定永續性磁碟區和儲存體類別使用本機儲存體或[城堡](https://github.com/rook/rook)儲存體。

## <a name="on-premises-cluster"></a>在內部部署叢集

內部叢集顯然沒有任何內建的儲存體類別，因此您必須設定[永續性磁碟區](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)/[佈建](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/)事先，然後使用 對應SQL Server 的巨量資料叢集部署期間的儲存體類別。

# <a name="customize-storage-size-for-each-pool"></a>自訂每個集區的儲存體大小
根據預設，每個叢集中佈建的 pod 佈建永續性磁碟區的大小為 6 GB。 這是藉由設定環境變數可設定`STORAGE_SIZE`到不同的值。 例如，您可以執行下列命令來將值設為 10 GB，才能執行`mssqlctl create cluster command`。

```bash
export STORAGE_SIZE=10Gi
```

這類的儲存體類別名稱和叢集中不同的集區的永續性磁碟區大小，您也可以讓不同的永續性儲存體設定的組態。 例如，您可以設定部署儲存體集區，以使用不同的儲存類別，並以更高的容量低於設定環境變數在部署叢集之前的永續性磁碟區：

```bash
export STORAGE_POOL_USE_PERSISTENT_VOLUME=true
export STORAGE_POOL_STORAGE_CLASS_NAME=premium-storage
export STORAGE_POOL_STORAGE_SIZE=100Gi
```

以下是設定為 SQL Server 的巨量資料叢集的永續性儲存體相關的環境變數的完整清單：

| 環境變數 | 預設值 | 描述 |
|---|---|---|
| **USE_PERSISTENT_VOLUME** | true | `true` 若要使用 Kubernetes 永續性磁碟區宣告 pod 儲存體。 `false` 要用於 pod 儲存體中的暫時主機儲存體。 |
| **STORAGE_CLASS_NAME** | 預設 | 如果`USE_PERSISTENT_VOLUME`是`true`這表示 Kubernetes 儲存體類別使用的名稱。 |
| **STORAGE_SIZE** | 6 gi | 如果`USE_PERSISTENT_VOLUME`是`true`，這表示每個 pod 的永續性磁碟區大小。 |
| **DATA_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` 若要使用 Kubernetes 永續性磁碟區宣告的資料集區中的 pod。 `false` 若要使用暫時主機儲存體的資料集區的 pod。 |
| **DATA_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | 表示要用於永續性磁碟區相關聯的資料集區的 pod Kubernetes 儲存體類別的名稱。|
| **DATA_POOL_STORAGE_SIZE** | STORAGE_SIZE |表示資料集區中每個 pod 的永續性磁碟區大小。 |
| **STORAGE_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` 若要使用 Kubernetes 永續性磁碟區宣告的儲存體集區中的 pod。 `false` 若要使用暫時主機儲存體的儲存體集區的 pod。|
| **STORAGE_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | TIndicates Kubernetes 儲存體類別，要用於永續性儲存體集區的 pod 相關聯的磁碟區的名稱。 |
| **STORAGE_POOL_STORAGE_SIZE** | STORAGE_SIZE | 表示儲存體集區中每個 pod 的永續性磁碟區大小。 |

## <a name="next-steps"></a>後續步驟

如需在 Kubernetes 中的磁碟區的完整文件，請參閱 <<c0> [ 磁碟區上的 Kubernetes 文件](https://kubernetes.io/docs/concepts/storage/volumes/)。

如需部署巨量資料的 SQL Server 叢集的詳細資訊，請參閱 <<c0> [ 如何部署巨量資料叢集的 Kubernetes 的 SQL Server](deployment-guidance.md)。

