---
title: 設定部署
titleSuffix: SQL Server big data clusters
description: 瞭解如何使用設定檔來自訂 big data cluster 部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7559ecf9c7b17ca21c088ed531a347f88e89ee2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419443"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>設定 big data 叢集的部署設定

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

若要自訂您的叢集部署設定檔, 您可以使用任何 JSON 格式編輯器, 例如 VSCode。 若要針對自動化目的編寫這些編輯的腳本, 請使用**azdata bdc config**命令。 本文說明如何藉由修改部署設定檔來設定 big data cluster 部署。 其中提供如何變更不同案例設定的範例。 如需有關如何在部署中使用設定檔的詳細資訊, 請參閱[部署指引](deployment-guidance.md#configfile)。

## <a name="prerequisites"></a>先決條件

- [安裝 azdata](deploy-install-azdata.md)。

- 本節中的每個範例假設您已建立其中一個標準設定的複本。 如需詳細資訊, 請參閱[建立自訂](deployment-guidance.md#customconfig)設定。 例如, 下列命令會`custom`根據預設的**aks-開發/測試**設定, 建立名為的目錄, 其中包含兩個 json 部署設定檔 ( **cluster. json**和**control. json**):

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a>變更叢集名稱

叢集名稱是大型資料叢集的名稱, 以及將在部署時建立的 Kubernetes 命名空間。 它是在叢集的下列部分中指定 **。 json**部署設定檔案:

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

下列命令會將索引鍵/值組傳送至 **--json-values**參數, 以將 big data 叢集名稱變更為**測試**叢集:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 您的 big data 叢集名稱必須是小寫的英數位元, 且不能有空格。 叢集的所有 Kubernetes 成品 (容器、pod、具狀態集、服務) 都會建立在與指定的叢集名稱相同的命名空間中。

## <a id="ports"></a>更新端點埠

端點是針對**控制項**中的控制器定義, 而在**cluster**的對應區段中則是針對閘道和 SQL Server 的主要實例。 下列的**控制項 json**設定檔部分會顯示控制器的端點定義:

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

下列範例會使用內嵌 JSON 來變更**控制器**端點的埠:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a>設定集區複本

每個集區的特性 (例如, 存放集區) 都會定義于**cluster json**設定檔中。 例如, **cluster**的下列部分會顯示存放集區定義:

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

您可以藉由修改每個集區的**複本**值, 設定集區中的實例數目。 下列範例會使用內嵌 JSON, 將儲存體和資料集區的這些值分別`10`變更`4`為和:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a>設定儲存體

您也可以變更用於每個集區的儲存類別和特性。 下列範例會將自訂儲存類別指派給存放集區, 並更新將資料儲存至100Gb 的持續性磁片區宣告大小。 請先建立如下所示的 patch. json 檔案, 其中除了*類型*和*複本*之外, 還包含新的*儲存體*區段

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

接著, 您可以使用**azdata bdc 設定修補程式**命令來更新**cluster. json**設定檔。
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> 以**kubeadm**為基礎的設定檔不會有每個集區的儲存體定義, 但是您可以視需要使用上述進程來新增。

如需儲存體設定的詳細資訊, 請參閱[Kubernetes 上的資料持續性與 SQL Server big Data cluster](concept-data-persistence.md)。

## <a id="sparkstorage"></a>設定不含 spark 的存放集區

您也可以將存放集區設定為在不使用 spark 的情況下執行, 並建立個別的 spark 集區。 這可讓您調整與儲存體無關的 spark 計算能力。 若要瞭解如何設定 spark 集區, 請參閱本文結尾的[JSON patch 檔案範例](#jsonpatch)。



根據預設, 存放集區的**includeSpark**設定會設定為 true, 因此您必須將**includeSpark**欄位新增至儲存體設定, 才能進行變更。 下列 JSON 修補程式檔案會顯示如何新增此檔案。

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

## <a id="podplacement"></a>使用 Kubernetes 標籤設定 pod 位置

您可以在具有特定資源的 Kubernetes 節點上控制 pod 位置, 以容納各種類型的工作負載需求。 例如, 您可能會想要確保存放集區 pod 放置在具有更多存放裝置的節點上, 或將 SQL Server 的主要實例放在具有較高 CPU 和記憶體資源的節點上。 在此情況下, 您會先建立具有不同類型硬體的異類 Kubernetes 叢集, 然後據以[指派節點標籤](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)。 部署 big data 叢集時, 您可以在叢集部署設定檔案的集區層級指定相同的標籤。 然後, Kubernetes 會負責關聯符合指定標籤之節點上的 pod。

下列範例顯示如何編輯自訂設定檔, 以包含 SQL Server 主要實例的節點標籤設定。 請注意, 內建設定中沒有*nodeLabel*金鑰, 因此您必須手動編輯自訂設定檔, 或建立修補檔案並將它套用至自訂設定檔。

在您目前的目錄中, 使用下列內容建立名為**patch**的檔案:

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

## <a id="jsonpatch"></a>JSON 修補檔案

JSON 修補程式檔案會同時設定多個設定。 如需 JSON 修補程式的詳細資訊, 請參閱 Python 和[JSONPath Online 評估](https://jsonpath.com/)工具[中的 json 修補程式](https://github.com/stefankoegl/python-json-patch)。

下列**patch. json**檔案會執行下列變更:

- 更新**control. json**中單一端點的埠。
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

- 更新**control. json**中的所有端點 (**埠**和**serviceType**)。
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

- 更新**control. json**中的控制器存放裝置設定。 這些設定適用于所有叢集元件, 除非在集區層級覆寫。
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

- 更新**control. json**中的儲存類別名稱。
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

- 在**cluster**中更新存放集區的集區存放裝置設定。
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

- 更新**cluster**中存放集區的 Spark 設定。
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

- 在**cluster. json**中建立具有2個實例的 spark 集區。
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
> 如需有關變更部署設定檔之結構和選項的詳細資訊, 請參閱[big data 叢集的部署設定檔參考](reference-deployment-config.md)。

使用**azdata bdc config**命令, 將變更套用至 JSON 修補程式檔案。 下列範例會將**patch. json**檔案套用至目標部署設定檔**自訂/cluster. json**。

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>後續步驟

如需在 big data cluster 部署中使用設定檔的詳細資訊, 請參閱[如何在 Kubernetes 上部署 SQL Server big data](deployment-guidance.md#configfile)叢集。
