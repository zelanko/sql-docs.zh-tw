---
title: 設定部署
titleSuffix: SQL Server big data clusters
description: 了解如何使用組態檔來自訂部署巨量資料叢集。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed86e7d293ba72eb178c65b53865b62ca419a6d2
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993992"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>設定部署巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

若要自訂叢集部署設定檔，您可以使用任何 json 格式之類的編輯器 VSCode。 對於指令碼用於自動化用途這些編輯，我們會提供**mssqlctl 叢集組態區段**命令。 這篇文章說明如何藉由修改部署組態檔案中設定的巨量資料叢集部署。 它會提供如何變更組態，針對不同案例的範例。 如需如何在部署中使用組態檔的詳細資訊，請參閱[部署指引](deployment-guidance.md#configfile)。

## <a name="prerequisites"></a>先決條件

- [安裝 mssqlctl](deploy-install-mssqlctl.md)。

- 每個在這一節中的範例假設您已建立的其中一個標準設定檔複本。 如需詳細資訊，請參閱 <<c0> [ 建立自訂的組態檔](deployment-guidance.md#customconfig)。 例如，下列命令會建立**custom.json**根據預設值的檔案**aks-dev-test.json**組態：

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

## <a id="clustername"></a> 變更叢集名稱

叢集名稱是巨量資料叢集，並會在部署中建立 Kubernetes 命名空間的名稱。 它會指定在部署設定檔的下列部分：

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

下列命令會傳送到索引鍵-值配對 **--json 值**若要變更的巨量資料叢集名稱的參數**測試叢集**:

```bash
mssqlctl cluster config section set -c custom.json -j ".metadata.name=test-cluster"
```

> [!IMPORTANT]
> 您名稱必須是叢集的只有大小寫英數字元，不含空格。 所有 Kubernetes 成品容器、 pod，具狀態設定 （服務） 叢集將會都建立與叢集名稱相同的命名空間中指定的名稱。

## <a id="ports"></a> 更新端點連接埠

端點定義也控制平面與個別的集區。 組態檔的下列部分顯示控制平面的端點定義：

```json
"endpoints": [
    {
        "name": "Controller",
        "serviceType": "LoadBalancer",
        "port": 30080
    },
    {
        "name": "ServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30777
    },
    {
        "name": "AppServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30778
    },
    {
        "name": "Knox",
        "serviceType": "LoadBalancer",
        "port": 30443
    }
]
```

下列範例會使用內嵌 JSON，若要變更的連接埠**控制器**端點：

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 設定集區的複本

在組態檔中定義，請在每個集區，例如儲存體集區的特性。 例如，下列的部分將顯示儲存體集區定義：

```json
"pools": [
    {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "storage": {
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
           },
        }
    }
]
```

您可以在集區中設定的執行個體數目，藉由修改**複本**每個集區的值。 下列範例會使用內嵌 JSON 來變更這些值的儲存體和資料集區`10`和`4`分別：

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4'
```

## <a id="storage"></a> 設定儲存體

您也可以變更用於每個集區的特性與儲存體類別。 下列範例會將自訂的儲存體類別指派給存放集區，並更新的永續性磁碟區宣告，針對儲存 100gb 的資料大小。 若要使用更新設定的組態檔中必須有這一節*mssqlctl 叢集組態組*命令，請參閱下列如何使用修補程式檔案來新增此區段：

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.className=storage-pool-class"
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.size=32Gi"
```

> [!NOTE]
> 組態檔將會根據**kubeadm-dev-test.json**沒有儲存體定義的每個集區，但這可以手動新增如有需要。

如需儲存體設定的詳細資訊，請參閱[巨量資料叢集的 Kubernetes 上的 SQL server 的資料持續性](concept-data-persistence.md)。

## <a id="podplacement"></a> 設定 pod 放置使用 Kubernetes 標籤

您可以控制在有特定的資源，以容納工作負載需求的各種類型的 Kubernetes 節點上的 pod 放置。 例如，您可能要確保儲存體集區的 pod 會放在更多的儲存體節點上，或 SQL Server 的主要執行個體放置具有較高的 CPU 和記憶體資源的節點上。 在此情況下，您需要先建立異質的 Kubernetes 叢集，與不同類型的硬體，然後[指派節點標籤](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)據此。 在部署巨量資料叢集時，您可以指定相同的標籤，在集區層級叢集部署的組態檔中。 Kubernetes 會接著負責的節點符合指定的標籤上的 pod，相似化。

下列範例示範如何編輯自訂的設定檔，以包含 SQL Server 的主要執行個體的節點標籤設定。 請注意，沒有任何*nodeLabel*的內建的組態，因此您必須以手動方式編輯自訂組態檔，或建立修補檔案，並將它套用至自訂組態檔中的索引鍵。

建立名為**patch.json**在您目前的目錄，使用下列內容：

```json
{
  "patch": [
     {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
      "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
mssqlctl cluster config section set -c custom.json -p ./patch.json
```

## <a id="jsonpatch"></a> JSON 修補程式檔案

JSON 修補檔案一次設定多個設定。 如需有關 JSON 修補程式的詳細資訊，請參閱[在 Python 中的 JSON 修補](https://github.com/stefankoegl/python-json-patch)並[JSONPath 線上評估工具](https://jsonpath.com/)。

下列**patch.json**檔案執行下列變更：

- 更新單一端點的連接埠。
- 更新所有端點 (**連接埠**並**serviceType**)。
- 更新控制項平面儲存體。 這些設定適用於所有叢集元件，除非在集區層級覆寫。
- 更新控制項平面儲存體中的儲存體類別名稱。
- 更新存放集區的集區儲存體設定。
- 更新存放集區的 Spark 設定。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.endpoints",
      "value": [
        {
          "serviceType": "LoadBalancer",
          "port": 30001,
          "name": "Controller"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "ServiceProxy"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "AppServiceProxy"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30443,
            "name": "Knox"
        }
      ]
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.controlPlane",
      "value": {
          "data": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage.data.className",
      "value": "managed-premium"
    },
    {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage",
      "value": {
          "data": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].hadoop.spark",
      "value": {
        "driverMemory": "2g",
        "driverCores": 1,
        "executorInstances": 3,
        "executorCores": 1,
        "executorMemory": "1536m"
      }
    }
  ]
}
```

> [!TIP]
> 如需有關結構及變更部署組態檔案的選項的詳細資訊，請參閱[巨量資料叢集的部署組態檔參考](reference-deployment-config.md)。

使用**mssqlctl 叢集組態區段組**套用 JSON 修補程式檔案中的變更。 下列範例會套用**patch.json**目標部署的組態檔的檔案**custom.json**。

```bash
mssqlctl cluster config section set -c custom.json -p ./patch.json
```

## <a name="next-steps"></a>後續步驟

如需使用組態檔中的巨量資料叢集部署的詳細資訊，請參閱[如何部署 SQL Server 的巨量資料叢集的 Kubernetes 上](deployment-guidance.md#configfile)。
