---
title: 設定部署
titleSuffix: SQL Server big data clusters
description: 了解如何搭配設定檔自訂巨量資料叢集部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cae2c216245fdb6483b3ad07a88b3517c38550bd
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470746"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>針對巨量資料叢集設定部署設定

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

若要自訂您的叢集部署設定檔，您可以使用任何 JSON 格式編輯器，例如 VSCode。 若要針對自動化目的編寫這些編輯的指令碼，請使用 **azdata bdc config** 命令。 此文章說明如何透過修改部署設定檔來設定巨量資料叢集部署。 它會提供如何針對不同案例變更設定的範例。 如需設定檔如何用於部署中的詳細資訊，請參閱[部署指導](deployment-guidance.md#configfile)。

## <a name="prerequisites"></a>Prerequisites

- [安裝 azdata](deploy-install-azdata.md)。

- 本節中的每個範例皆假設您已建立其中一個標準設定的複本。 如需詳細資訊，請參閱[建立自訂設定](deployment-guidance.md#customconfig)。 例如，下列命令會建立名為 `custom` 的目錄，其中會根據預設的 **aks-dev-test**設定，包含兩個 JSON 部署設定檔 **cluster.json** 和 **control.json**：

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> 變更叢集名稱

叢集名稱同時是巨量資料叢集及將會在部署時建立的 Kubernetes 命名空間的名稱。 它會在 **cluster.json** 部署設定檔的下列部分中指定：

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

下列命令會將機碼值組傳送至 **--json-values** 參數，以將巨量資料叢集名稱變更為 **test-cluster**：

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 您巨量資料叢集的名稱只能由小寫的英數字元組成，不能有空格。 叢集的所有 Kubernetes 成品 (容器、Pod、具狀態集合、服務) 將會在具有和所指定叢集名稱相同名稱的命名空間中建立。

## <a id="ports"></a> 更新端點連接埠

端點會在 **control.json** 中針對控制器定義，並在 **cluster.json** 中相對應的區段中針對閘道和 SQL Server 主要執行個體定義。 **control.json** 設定檔的下列部分會顯示控制器的端點定義：

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
    }
]
```

下列範例會使用內嵌 JSON 來變更 **controller** 端點的連接埠：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 設定集區複本

每個集區的特性 (例如存放集區) 都是在 **cluster.json** 設定檔中定義。 例如，**cluster.json** 的下列部分會顯示存放集區定義：

```json
"pools": [
   {
       "metadata": {
           "kind": "Pool",
           "name": "default"
       },
       "spec": {
           "type": "Storage",
           "replicas": 2
       }
   }
]
```

您可以修改每個集區的 **replicas**值，來設定集區中的執行個體數目。 下列範例會使用內嵌 JSON 來將這些適用於儲存體和資料集區的值分別變更為 `10` 和 `4`：

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a> 設定儲存體

您也可以變更用於每個集區的儲存體類別和特性。 下列範例會將自訂儲存體類別指派至存放集區，並將儲存資料的持續性磁碟區宣告的大小更新為 100Gb。 先如下所示建立 patch.json 檔案，除了 *type* 和 *replicas* 區段之外，它還會包含新的 *storage* 區段

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
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
                },
        "type":"Storage",
        "replicas":2
      }
    }
  ]
}
```

您接著可以使用 **azdata bdc config patch** 命令來更新 **cluster.json** 設定檔。
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> 以 **kubeadm-dev-test** 為基礎的設定檔並不會有適用於每個集區的儲存體定義，但您可以視需要使用上述程序來新增它。

如需儲存體設定的詳細資訊，請參閱[在 Kubernetes 上使用 SQL Server 2019 巨量資料叢集的資料持續性](concept-data-persistence.md)。

## <a id="sparkstorage"></a> 設定不搭配 Spark 的存放集區

您也可以設定存放集區以在不搭配 Spark 的情況下執行，並建立個別的 Spark 集區。 這可讓您在獨立於儲存體的情況下調整 Spark 計算能力。 若要查看設定 Spark 集區的方式，請參閱此文章結尾的 [JSON 修補檔範例](#jsonpatch)。



根據預設，存放集區的 **includeSpark** 設定會被設定為 True，因此您必須將 **includeSpark** 欄位新增至儲存體設定以進行變更。 下列 JSON 修補檔會示範如何新增它。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
       "type":"Storage",
       "replicas":2,
       "includeSpark":false
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

## <a id="podplacement"></a> 使用 Kubernetes 標籤設定 Pod 位置

您可以在具有特定資源以容納各種不同工作負載需求的 Kubernetes 節點上控制 Pod 位置。 例如，您可能會想確保存放集區 Pod 會被置於具有較多儲存體的節點上，或是將 SQL Server 主要執行個體置於具有較高 CPU 和記憶體資源的節點上。 在此情況下，您必須先建置具有不同硬體類型的異質 Kubernetes 叢集，然後相對應地[指派節點標籤](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) \(英文\)。 在部署巨量資料叢集時，您可以在叢集部署設定檔中於集區層級指定相同的標籤。 Kubernetes 接著將會處理在符合指定標籤的節點上關聯 Pod 的作業。

下列範例會示範如何編輯自訂設定檔，以包含適用於 SQL Server 主要執行個體的節點標籤設定。 請注意，內建設定中並沒有 *nodeLabel* 機碼，因此您必須手動編輯自訂設定檔，或是建立修補檔並將它套用到自訂設定檔。

搭配下列內容在您目前的目錄中建立名為 **patch.json** 的檔案：

```json
{
  "patch": [
     {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
    "type": "Master",
        "replicas": 1,
        "hadrEnabled": false,
        "endpoints": [
            {
             "name": "Master",
             "serviceType": "NodePort",
             "port": 31433
            }
          ],
        "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a> JSON 修補檔

JSON 修補檔會同時設定多個設定。 如需 JSON 修補的詳細資訊，請參閱 [Python 中的 JSON 修補](https://github.com/stefankoegl/python-json-patch) \(英文\) 及 [JSONPath 線上評估工具](https://jsonpath.com/) \(英文\)。

下列 **patch.json** 檔案會執行下列變更：

- 更新 **control.json** 中單一端點的連接埠。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.endpoints[?(@.name=='Controller')].port",
          "value": 30000
        }   
      ]
    }
    ```

- 更新 **control.json** 中的所有端點 (**port** 和 **serviceType**)。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.endpoints",
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
        }
          ]
        }
      ]
    }
    ```

- 更新 **control.json** 中的控制器儲存體設定。 這些設定適用於所有叢集元件，除非在集區層級覆寫它們。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.storage",
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
      ]
    }
    ```

- 更新 **control.json** 中的儲存體類別名稱。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.storage.data.className",
          "value": "managed-premium"
        }   
      ]
    }
    ```

- 更新 **cluster.json** 中適用於存放集區的集區儲存體設定。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
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

- 更新 **cluster.json** 中適用於存放集區的 Spark 設定。
    ```json
    {
      "patch": [
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

- 在 **cluster.json** 中建立具有 2 個執行個體的 Spark 集區。
    ```json
    {
      "patch": [
        {
          "op": "add",
          "path": "spec.pools/-",
          "value":
          {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        },
        "hadoop": {
          "yarn": {
            "nodeManager": {
              "memory": 12288,
              "vcores": 6
            },
            "schedulerMax": {
              "memory": 12288,
              "vcores": 6
            },
            "capacityScheduler": {
              "maxAmPercent": 0.3
            }
          },
          "spark": {
            "driverMemory": "2g",
            "driverCores": 1,
            "executorInstances": 2,
            "executorMemory": "2g",
            "executorCores": 1
          }
        }
          }
        } 
      ]
    }
    ```



> [!TIP]
> 如需適用於變更部署設定檔的結構和選項的詳細資訊，請參閱[適用於巨量資料叢集的部署設定檔參考](reference-deployment-config.md)。

使用 **azdata bdc config** 命令來在 JSON 修補檔中套用變更。 下列範例會將 **patch.json** 檔案套用至目標部署設定檔 **custom/cluster.json**。

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>後續步驟

如需在巨量資料叢集部署中使用設定檔的詳細資訊，請參閱[如何在 Kubernetes 上部署 SQL Server 巨量資料叢集](deployment-guidance.md#configfile)。
