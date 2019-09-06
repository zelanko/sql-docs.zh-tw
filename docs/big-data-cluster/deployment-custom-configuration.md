---
title: 設定部署
titleSuffix: SQL Server big data clusters
description: 了解如何搭配設定檔自訂巨量資料叢集部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a0da84d60a9513b0ca81a0256218928372882e72
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304823"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>設定叢集資源和服務的部署設定

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

從 azdata 管理工具內建的預先定義設定設定檔集合開始，您可以輕鬆地修改預設設定，使其更符合您的 BDC 工作負載需求。 從發行候選版本開始，已更新設定檔案的結構，讓您能夠針對資源的每個服務進行細微的更新設定。 

您也可以設定資源層級設定，或更新資源中所有服務的設定。 以下是**bdc json**結構的摘要：

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "BigDataCluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "resources": {
            "nmnode-0": {...
            },
            "sparkhead": {...
            },
            "zookeeper": {...
            },
            "gateway": {...
            },
            "appproxy": {...
            },
            "master": {...
            },
            "compute-0": {...
            },
            "data-0": {...
            },
            "storage-0": {...
        },
        "services": {
            "sql": {
                "resources": [
                    "master",
                    "compute-0",
                    "data-0",
                    "storage-0"
                ]
            },
            "hdfs": {
                "resources": [
                    "nmnode-0",
                    "zookeeper",
                    "storage-0",
                    "sparkhead"
                ],
                "settings": {...
            },
            "spark": {
                "resources": [
                    "sparkhead",
                    "storage-0"
                ],
                "settings": {...
            }
        }
    }
}
```

若要更新資源層級設定（例如集區中的實例），您將會更新資源規格。例如，若要更新計算集區中的實例數目，您將在**bdc. json**設定檔中修改此區段：
```json
"resources": {
    ...
    "compute-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Compute",
            "replicas": 4
        }
    }
    ...
}
``` 

類似于變更特定資源內單一服務的設定。 例如，如果您只想要針對存放集區中的 Spark 元件變更 Spark 記憶體設定，您將會在**bdc. json**設定檔中，使用**spark**服務的**設定**區段來更新**儲存體-0**資源.
```json
"resources":{
    ...
     "storage-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "settings": {
                "spark": {
                    "driverMemory": "2g",
                    "driverCores": "1",
                    "executorInstances": "3",
                    "executorMemory": "1536m",
                    "executorCores": "1"
                }
            }
        }
    }
    ...
}
```

如果您想要針對與多個資源相關聯的服務套用相同的設定，您將會更新 [**服務**] 區段中的對應**設定**。 例如，如果您想要在存放集區和 Spark 集區中同時設定 Spark 的相同設定，您將會更新**bdc json**設定檔中**spark**服務區段的 [**設定**] 區段。

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "driverMemory": "2g",
            "driverCores": "1",
            "executorInstances": "3",
            "executorMemory": "1536m",
            "executorCores": "1"
        }
    }
    ...
}
```


若要自訂您的叢集部署設定檔，您可以使用任何 JSON 格式編輯器，例如 VSCode。 若要針對自動化目的編寫這些編輯的指令碼，請使用 **azdata bdc config** 命令。 此文章說明如何透過修改部署設定檔來設定巨量資料叢集部署。 它會提供如何針對不同案例變更設定的範例。 如需設定檔如何用於部署中的詳細資訊，請參閱[部署指導](deployment-guidance.md#configfile)。

## <a name="prerequisites"></a>必要條件

- [安裝 azdata](deploy-install-azdata.md)。

- 本節中的每個範例皆假設您已建立其中一個標準設定的複本。 如需詳細資訊，請參閱[建立自訂設定](deployment-guidance.md#customconfig)。 例如，下列命令會`custom`根據預設的**aks-開發/測試**設定，建立名為的目錄，其中包含兩個 json 部署設定檔（ **bdc. json**和**control. json**）：

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> 變更叢集名稱

叢集名稱同時是巨量資料叢集及將會在部署時建立的 Kubernetes 命名空間的名稱。 它是在**bdc json**部署設定檔的下列部分中指定：

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

下列命令會將機碼值組傳送至 **--json-values** 參數，以將巨量資料叢集名稱變更為 **test-cluster**：

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 您巨量資料叢集的名稱只能由小寫的英數字元組成，不能有空格。 叢集的所有 Kubernetes 成品 (容器、Pod、具狀態集合、服務) 將會在具有和所指定叢集名稱相同名稱的命名空間中建立。

## <a id="ports"></a> 更新端點連接埠

端點是針對控制項中的控制器以及在**bdc**的對應區段中的閘道和 SQL Server 主要實例定義的 **。** **control.json** 設定檔的下列部分會顯示控制器的端點定義：

```json
{
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
}
```

下列範例會使用內嵌 JSON 來變更 **controller** 端點的連接埠：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 設定集區複本

每個資源（例如存放集區）的設定都會定義在**bdc. json**設定檔中。 例如， **bdc**的下列部分會顯示**儲存體-0**資源定義：

```json
"storage-0": {
    "metadata": {
        "kind": "Pool",
        "name": "default"
    },
    "spec": {
        "type": "Storage",
        "replicas": 2,
        "settings": {
            "spark": {
                "driverMemory": "2g",
                "driverCores": "1",
                "executorInstances": "3",
                "executorMemory": "1536m",
                "executorCores": "1"
            }
        }
    }
}
```

您可以修改每個集區的 **replicas**值，來設定集區中的執行個體數目。 下列範例會使用內嵌 JSON 來將這些適用於儲存體和資料集區的值分別變更為 `10` 和 `4`：

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

## <a id="storage"></a> 設定儲存體

您也可以變更用於每個集區的儲存體類別和特性。 下列範例會將自訂儲存類別指派給儲存體和資料集區，並更新持續性磁片區宣告的大小，以便將資料儲存到 500 Gb （適用于 HDFS （儲存集區））和 100 Gb （適用于資料集區）。 先如下所示建立 patch.json 檔案，除了 *type* 和 *replicas* 區段之外，它還會包含新的 *storage* 區段

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "500Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

接著，您可以使用**azdata bdc 設定修補程式**命令來更新**bdc. json**設定檔。
```bash
azdata bdc config patch --config-file custom/bdc.json --patch ./patch.json
```

> [!NOTE]
> 以 **kubeadm-dev-test** 為基礎的設定檔並不會有適用於每個集區的儲存體定義，但您可以視需要使用上述程序來新增它。

如需儲存體設定的詳細資訊，請參閱[在 Kubernetes 上使用 SQL Server 2019 巨量資料叢集的資料持續性](concept-data-persistence.md)。

## <a id="sparkstorage"></a> 設定不搭配 Spark 的存放集區

您也可以設定存放集區以在不搭配 Spark 的情況下執行，並建立個別的 Spark 集區。 這可讓您在獨立於儲存體的情況下調整 Spark 計算能力。 若要查看設定 Spark 集區的方式，請參閱此文章結尾的 [JSON 修補檔範例](#jsonpatch)。


根據預設，存放集區資源的**includeSpark**設定會設定為 true，因此您必須將**includeSpark**欄位編輯為儲存體設定，才能進行變更。 下列命令會顯示如何使用內嵌 json 來編輯此值。

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a id="podplacement"></a> 使用 Kubernetes 標籤設定 Pod 位置

您可以在具有特定資源以容納各種不同工作負載需求的 Kubernetes 節點上控制 Pod 位置。 例如，您可能會想要確保存放集區資源 pod 放置在具有更多存放裝置的節點上，或將 SQL Server 的主要實例放在具有較高 CPU 和記憶體資源的節點上。 在此情況下，您必須先建置具有不同硬體類型的異質 Kubernetes 叢集，然後相對應地[指派節點標籤](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) \(英文\)。 在部署巨量資料叢集時，您可以在叢集部署設定檔中於集區層級指定相同的標籤。 Kubernetes 接著將會處理在符合指定標籤的節點上關聯 Pod 的作業。 需要新增至 kubernetes 叢集中節點的特定標籤索引鍵是以**mssql**為全叢集的。 此標籤本身的值可以是您選擇的任何字串。

下列範例顯示如何編輯自訂設定檔，以包含 SQL Server 主要實例、計算集區、資料集區 & 儲存集區的節點標籤設定。 內建設定中沒有*nodeLabel*金鑰，因此您必須手動編輯自訂設定檔，或建立修補檔案並將它套用至自訂設定檔。 SQL Server 的主要實例 pod 會部署在包含具有值**bdc-Master**的**標籤的節點**上。 計算集區和資料集區 pod 會部署在包含標籤為 [ **mssql-** 全叢集] 且值為 **[bdc-sql**] 的節點上。 存放集區 pod 會部署在包含標籤為**mssql-** 全叢集且值為**bdc 儲存體**的節點上。

搭配下列內容在您目前的目錄中建立名為 **patch.json** 的檔案：

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.master.spec",
      "value": {
        "type": "Master",
        "replicas": 1,
        "endpoints": [
          {
            "name": "Master",
            "serviceType": "NodePort",
            "port": 31433
          }
        ],
        "settings": {
          "sql": {
            "hadr.enabled": "false"
          }
        },
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.compute-0.spec",
      "value": {
        "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage",
        "settings": {
          "spark": {
            "includeSpark": "true"
          }
        }
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
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

- 在**bdc**中更新存放集區的集區儲存設定。
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

- 更新**bdc json**中存放集區的 Spark 設定。
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
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

- 在**bdc. json**中建立具有2個實例的 spark 集區。
```json
{
  "patch": [
    {
      "op": "add",
      "path": "spec.resources.spark-0",
      "value": {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        }
      }
    },
    {
      "op": "add",
      "path": "spec.services.spark.resources/-",
      "value": "spark-0"
    },
    {
      "op": "add",
      "path": "spec.services.hdfs.resources/-",
      "value": "spark-0"
    },
    {
      "op": "add",
      "path": "spec.services.spark.settings",
      "value": {
        "DriverMemory": "2g",
        "DriverCores": "1",
        "ExecutorInstances": "2",
        "ExecutorMemory": "2g",
        "ExecutorCores": "1"
      }
    }
  ]
}
```

> [!TIP]
> 如需適用於變更部署設定檔的結構和選項的詳細資訊，請參閱[適用於巨量資料叢集的部署設定檔參考](reference-deployment-config.md)。

使用 **azdata bdc config** 命令來在 JSON 修補檔中套用變更。 下列範例會將**patch. json**檔案套用至目標部署設定檔的**自訂/bdc json**。

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>停用 ElasticSearch 以在特殊許可權模式中執行
根據預設，ElasticSearch 容器會在大型資料叢集中以許可權模式執行。 這是為了確保在容器初始化時，容器具有足夠的許可權，可在 ElasticSearch 處理較高數量的記錄時，更新主機必要上的設定。 您可以在[本文](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)中找到有關此主題的詳細資訊。 

若要停用執行 ElasticSearch 的容器以特殊許可權模式執行，您必須更新**控制項**中的 [**設定**] 區段，並將 [ **vm 的最大 _map_count** ] 值指定為 **-1**。 以下是此區段外觀的範例：
```json
"settings": {
    "ElasticSearch": {
        "vm.max_map_count": "-1"
      }
}
```

您可以用手動方式編輯**控制項. json** ，並將上述區段新增至**規格**，或者您可以建立類似下面的 patch 檔案**elasticsearch** ，並使用**azdata** CLI 來修補**config.xml**檔案：

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec",
      "value": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-RC1-ubuntu",
            "imagePullPolicy": "Always"
        },
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
        ],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
             }
        }
       }
    }
  ]
}
```

執行此命令來修補設定檔案：
```
azdata bdc config patch --config-file control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> 建議您在 Kubernetes 叢集中的每個主機上手動手動更新**max_map_count**設定，[如本文中](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)的指示所述。
## <a name="next-steps"></a>後續步驟

如需在 big data cluster 部署中使用設定檔的詳細資訊，請參閱 how [to deploy [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] on Kubernetes](deployment-guidance.md#configfile)。
