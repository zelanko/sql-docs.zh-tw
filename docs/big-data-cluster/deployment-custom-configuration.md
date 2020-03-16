---
title: 設定部署
titleSuffix: SQL Server big data clusters
description: 了解如何搭配設定檔自訂巨量資料叢集部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0bed12749231eb9ca4c4398699d662666004613a
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79285852"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>設定叢集資源和服務的部署設定

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

從 `azdata` 管理工具內建的預先定義組態設定檔集合開始，您可以輕鬆地修改預設設定，使其更符合 BDC 工作負載需求。 設定檔結構可讓您針對資源的每項服務進行細微設定更新。

觀看這段 13 分鐘的影片，以取得巨量資料叢集設定的概觀：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Big-Data-Cluster-Configuration/player?WT.mc_id=dataexposed-c9-niner]

> [!TIP]
> 如需如何部署高可用性服務的詳細資料，請參閱有關如何針對任務關鍵性元件 (例如 [SQL Server 主要](deployment-high-availability.md)或 [HDFS 名稱節點](deployment-high-availability-hdfs-spark.md)) 設定**高可用性**的文章。

您也可以設定資源層級設定，或更新資源中所有服務的設定。 以下是 `bdc.json` 的結構摘要：

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

若要更新資源層級設定 (例如集區中的執行個體)，您會更新資源規格。例如，若要更新計算集區中的執行個體數目，您會在 `bdc.json` 設定檔中修改此區段：

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

變更特定資源中單一服務的設定也是如此。 例如，如果您只想要針對存放集區中的 Spark 元件變更 Spark 記憶體設定，您會在 `bdc.json` 設定檔中，使用 `spark` 服務的 `settings` 區段來更新 `storage-0` 資源。

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
                    "spark-defaults-conf.spark.driver.memory": "2g",
                    "spark-defaults-conf.spark.driver.cores": "1",
                    "spark-defaults-conf.spark.executor.instances": "3",
                    "spark-defaults-conf.spark.executor.memory": "1536m",
                    "spark-defaults-conf.spark.executor.cores": "1",
                    "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
                    "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
                    "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
                    "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
                    "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
                }
            }
        }
    }
    ...
}
```

如果您想要針對與多個資源建立關聯的服務套用相同設定，您會在 `services` 區段中更新對應的 `settings`。 例如，如果您想要針對存放集區和 Spark 集區中的 Spark 設定相同的設定，您會在 `bdc.json` 設定檔的 `spark` 服務區段中更新 `settings` 區段。

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "spark-defaults-conf.spark.driver.memory": "2g",
            "spark-defaults-conf.spark.driver.cores": "1",
            "spark-defaults-conf.spark.executor.instances": "3",
            "spark-defaults-conf.spark.executor.memory": "1536m",
            "spark-defaults-conf.spark.executor.cores": "1",
            "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
            "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
            "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
            "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
            "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
        }
    }
    ...
}
```

若要自訂您的叢集部署設定檔，您可以使用任何 JSON 格式編輯器，例如 VSCode。 若要針對自動化目的編寫這些編輯的指令碼，請使用 `azdata bdc config` 命令。 此文章說明如何透過修改部署設定檔來設定巨量資料叢集部署。 它會提供如何針對不同案例變更設定的範例。 如需設定檔如何用於部署中的詳細資訊，請參閱[部署指導](deployment-guidance.md#configfile)。

## <a name="prerequisites"></a>Prerequisites

- [安裝 azdata](deploy-install-azdata.md)。

- 本節中的每個範例皆假設您已建立其中一個標準設定的複本。 如需詳細資訊，請參閱[建立自訂設定](deployment-guidance.md#customconfig)。 例如，下列命令會建立稱為 `custom-bdc` 的目錄，其中會根據預設的 `aks-dev-test` 設定而包含兩個 JSON 部署設定檔：`bdc.json` 和 `control.json`：

   ```bash
   azdata bdc config init --source aks-dev-test --target custom-bdc
   ```

## <a id="docker"></a> 變更預設的 Docker 登錄、存放庫和映像標籤

內建設定檔 (特別是 control.json) 包含 `docker` 區段，其中已預先填入容器登錄、存放庫和映像標籤。 根據預設，巨量資料叢集所需的映像會位於 Microsoft 容器登錄 (`mcr.microsoft.com`) 的 `mssql/bdc` 存放庫中：

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "Cluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-GDR1-ubuntu-16.04",
            "imagePullPolicy": "Always"
        },
        ...
    }
}
```

部署之前，您可以直接編輯 `control.json` 設定檔或使用 `azdata bdc config` 命令來自訂 `docker` 設定。 例如，下列命令使用不同的 `<registry>`、`<repository>` 和 `<image_tag>` 來更新 `custom-bdc` control.json 設定檔：

```bash
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.registry=<registry>"
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.repository=<repository>"
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.imageTag=<image_tag>"
```

> [!TIP]
> 基於最佳做法，您必須使用版本特定的映像標籤，並避免使用 `latest` 映像標籤，因為這可能會導致版本不相符而造成叢集健全狀況問題。

> [!TIP]
> 巨量資料叢集部署必須能夠存取容器登錄和存放庫以從中提取容器映像。 如果您的環境無法存取預設 Microsoft 容器登錄，您可以執行離線安裝，先將所需的映像放入私人 Docker 存放庫。 如需離線安裝的詳細資訊，請參閱[執行 SQL Server 巨量資料叢集的離線部署](deploy-offline.md)。 請注意，您必須先設定 `DOCKER_USERNAME` 與 `DOCKER_PASSWORD` [環境變數](deployment-guidance.md#env)，然後發行部署，以確保部署工作流程能夠存取您的私人存放庫以從中提取映像。

## <a id="clustername"></a> 變更叢集名稱

叢集名稱同時是巨量資料叢集及將會在部署時建立的 Kubernetes 命名空間的名稱。 這會在 `bdc.json` 部署設定檔的下列部分中指定：

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

下列命令會將索引鍵/值組傳送至 `--json-values` 參數，以將巨量資料叢集名稱變更為 `test-cluster`：

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 您巨量資料叢集的名稱只能由小寫的英數字元組成，不能有空格。 叢集的所有 Kubernetes 成品 (容器、Pod、具狀態集合、服務) 將會在具有和所指定叢集名稱相同名稱的命名空間中建立。

## <a id="ports"></a> 更新端點連接埠

端點會在 `control.json` 中針對控制器定義，並在 `bdc.json` 的對應區段中針對閘道和 SQL Server 主要執行個體定義。 `control.json` 設定檔的下列部分會顯示控制器端點定義：

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

下列範例使用內嵌 JSON 來變更 `controller` 端點的連接埠：

```bash
azdata bdc config replace --config-file custom-bdc/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 設定規模

每個資源 (例如存放集區) 的設定都是在 `bdc.json` 設定檔中定義。 例如，`bdc.json` 的下列部分會顯示 `storage-0` 資源定義：

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
                "spark-defaults-conf.spark.driver.memory": "2g",
                "spark-defaults-conf.spark.driver.cores": "1",
                "spark-defaults-conf.spark.executor.instances": "3",
                "spark-defaults-conf.spark.executor.memory": "1536m",
                "spark-defaults-conf.spark.executor.cores": "1",
                "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
                "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
                "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
                "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
                "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
            }
        }
    }
}
```

您可以修改每個集區的 `replicas` 值來設定存放、計算及/或資料集區中執行個體數目。 下列範例使用內嵌 JSON 來將這些適用於存放、計算和資料集區的值分別變更為 `10`、`4` 和 `4`：

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.compute-0.spec.replicas=4"
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

> [!NOTE]
> 針對計算和資料集區所驗證的執行個體數目上限都是 `8`。 部署時不會強制執行此限制，但不建議您在生產環境部署中設定較高的規模。

## <a id="storage"></a> 設定儲存體

您也可以變更用於每個集區的儲存體類別和特性。 下列範例會將自訂儲存類別指派給存放和資料集區，並將儲存資料的持續性磁碟區宣告大小更新為 500 GB (HDFS/存放集區) 和 100 GB (資料集區)。 

> [!TIP]
> 如需儲存體設定的詳細資訊，請參閱[在 Kubernetes 上使用 SQL Server 2019 巨量資料叢集的資料持續性](concept-data-persistence.md)。

先如下所示建立 patch.json 檔案，除了 *type* 和 *replicas* 區段之外，它還會包含新的 *storage* 區段

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

您接著可以使用 `azdata bdc config patch` 命令來更新 `bdc.json` 設定檔。
```bash
azdata bdc config patch --config-file custom-bdc/bdc.json --patch ./patch.json
```

> [!NOTE]
> 以 `kubeadm-dev-test` 為基礎之設定檔沒有針對每個集區的儲存體定義，但您可以視需要使用上述程序來新增定義。

## <a id="sparkstorage"></a> 設定不搭配 Spark 的存放集區

您也可以設定存放集區以在不搭配 Spark 的情況下執行，並建立個別的 Spark 集區。 此設定可讓您在獨立於儲存體的情況下調整 Spark 計算能力。 若要了解如何設定 Spark 集區，請參閱本文中的[＜建立 Spark 集區＞](#sparkpool)一節。

> [!NOTE]
> 不支援在不使用 Spark 的情況下部署巨量資料叢集。 因此，您必須將 `includeSpark` 設定為 `true`，或必須建立至少具有一個執行個體的個別 [Spark 集區](#sparkpool)。 您也可以讓 Spark 同時在存放集區中執行 (`includeSpark` 為 `true`) 並具有個別的 Spark 集區。

根據預設，存放集區的 `includeSpark` 設定會設定為 true，因此您必須將 `includeSpark` 欄位編輯到儲存體設定中，以便進行變更。 下列範例示範如何使用內嵌 JSON 來編輯此值。

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a id="sparkpool"></a> 建立 Spark 集區

您可以建立 Spark 集區來搭配或取代存放集區中執行的 Spark 執行個體。 下列範例示範如何藉由修補 `bdc.json` 設定檔來建立具有兩個執行個體的 Spark 集區。 

首先，建立 `spark-pool-patch.json` 檔案，如下所示：

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
        }
    ]
}
```

然後執行 `azdata bdc config patch` 命令：

```bash
azdata bdc config patch -c custom-bdc/bdc.json -p spark-pool-patch.json
```

## <a id="podplacement"></a> 使用 Kubernetes 標籤設定 Pod 位置

您可以在具有特定資源以容納各種不同工作負載需求的 Kubernetes 節點上控制 Pod 位置。 使用 Kubernetes 標籤，您可以自訂 Kubernetes 叢集中用於部署巨量資料叢集資源的節點，但也可以限制用於特定資源的節點。
例如，您可能會想確保存放集區資源 Pod 會置於具有較多儲存空間的節點上，而 SQL Server 主要執行個體則置於具有較高 CPU 和記憶體資源的節點上。 在此情況下，您必須先建置具有不同硬體類型的異質 Kubernetes 叢集，然後相對應地[指派節點標籤](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) \(英文\)。 在部署巨量資料叢集時，您可以在 `control.json` 檔案中使用 `clusterLabel` 屬性，在叢集層級指定相同標籤來指出用於巨量資料叢集的節點。 然後針對集區層級放置使用不同的標籤。 您可以使用 `nodeLabel` 屬性，在巨量資料叢集部署設定檔中指定這些標籤。 Kubernetes 會在符合指定標籤的節點上指派 Pod。 必須新增至 Kubernetes 叢集中節點的特定標籤索引鍵為 `mssql-cluster` (指出用於巨量資料叢集的節點) 和 `mssql-resource` (指出針對各項資源放置 Pod 的特定節點)。 這些標籤值可以是您選擇的任意字串。

> [!NOTE]
> 由於 Pod 的本質是執行節點層級計量集合，因此 `metricsdc` Pod 會部署在具有 `mssql-cluster` 標籤的所有節點上，且 `mssql-resource` 不會套用至這些 Pod。

下列範例示範如何編輯自訂設定檔，以包含節點標籤 `bdc` (用於整個巨量資料叢集)、標籤 `bdc-master` (用於將 SQL Server 主要執行個體 Pod 放在特定節點上)、`bdc-storage-pool` (用於存放集區資源)、`bdc-compute-pool` (用於計算集區和資料集區 Pod)，以及 `bdc-shared` (用於其餘資源)。 

首先為 Kubernetes 節點加上標籤：

```bash
kubectl label node <kubernetesNodeName1> mssql-cluster=bdc mssql-resource=bdc-shared --overwrite=true
kubectl label node <kubernetesNodeName2> mssql-cluster=bdc mssql-resource=bdc-master --overwrite=true
kubectl label node <kubernetesNodeName3> mssql-cluster=bdc mssql-resource=bdc-compute-pool --overwrite=true
kubectl label node <kubernetesNodeName4> mssql-cluster=bdc mssql-resource=bdc-compute-pool --overwrite=true
kubectl label node <kubernetesNodeName5> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName6> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName7> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName8> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
```

然後更新叢集部署設定檔以包含標籤值。 此範例假設您在 `custom-bdc` 設定檔 (Profile) 中自訂設定檔。 根據預設，內建設定中並沒有 `nodeLabel` 和 `clusterLabel` 索引鍵，因此您必須手動編輯自訂設定檔，或使用 `azdata bdc config add` 命令來進行必要的編輯。

```bash
azdata bdc config add -c custom-bdc/control.json -j "$.spec.clusterLabel=bdc"
azdata bdc config add -c custom-bdc/control.json -j "$.spec.nodeLabel=bdc-shared"

azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.master.spec.nodeLabel=bdc-master"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.compute-0.spec.nodeLabel=bdc-compute-pool"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.data-0.spec.nodeLabel=bdc-compute-pool"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.storage-0.spec.nodeLabel=bdc-storage-pool"

# below can be omitted in which case we will take the node label default from the control.json
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.nmnode-0.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.sparkhead.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.zookeeper.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.gateway.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.appproxy.spec.nodeLabel=bdc-shared"
```

## <a id="jsonpatch"></a> 使用 JSON 修補檔的其他自訂

JSON 修補檔會同時設定多個設定。 如需 JSON 修補的詳細資訊，請參閱 [Python 中的 JSON 修補](https://github.com/stefankoegl/python-json-patch) \(英文\) 及 [JSONPath 線上評估工具](https://jsonpath.com/) \(英文\)。

下列 `patch.json` 檔案會執行下列變更：

- 更新 `control.json` 中單一端點的連接埠。

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

- 更新 `control.json` 中的所有端點 (`port` 和 `serviceType`)。

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

- 更新 `control.json` 中的控制器儲存體設定。 這些設定適用於所有叢集元件，除非在集區層級覆寫它們。

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

- 更新 `control.json` 中的儲存類別名稱。

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

- 更新 `bdc.json` 中存放集區的集區儲存體設定。

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

- 更新 `bdc.json` 中存放集區的 Spark 設定。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
      "value": {
            "spark-defaults-conf.spark.driver.memory": "2g",
            "spark-defaults-conf.spark.driver.cores": "1",
            "spark-defaults-conf.spark.executor.instances": "3",
            "spark-defaults-conf.spark.executor.memory": "1536m",
            "spark-defaults-conf.spark.executor.cores": "1",
            "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
            "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
            "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
            "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
            "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
      }
    }
  ]
}
```

> [!TIP]
> 如需適用於變更部署設定檔的結構和選項的詳細資訊，請參閱[適用於巨量資料叢集的部署設定檔參考](reference-deployment-config.md)。

使用 `azdata bdc config` 命令在 JSON 修補檔中套用變更。 下列範例會將 `patch.json` 檔案套用至目標部署設定檔 `custom-bdc/bdc.json`。

```bash
azdata bdc config patch --config-file custom-bdc/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>停止 ElasticSearch 以特權模式執行

根據預設，ElasticSearch 容器會在巨量資料叢集中以特權模式執行。 此設定可確保在容器初始化時，容器具有足夠權限來更新 ElasticSearch 處理較高記錄量時所需主機上的設定。 如需此主題的詳細資訊，請參閱[本文](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)。 

若要停止執行 ElasticSearch 的容器以特權模式執行，您必須更新 `control.json` 中的 `settings` 區段，並將 `vm.max_map_count` 的值指定為 `-1`。 此區段看起來如下範例：

```json
{
    "apiVersion": "v1",
    "metadata": {...},
    "spec": {
        "docker": {...},
        "storage": {...},
        "endpoints": [...],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
            }
        }
    }
}
```

您可以手動編輯 `control.json`，並將上述區段新增至 `spec`，或可建立如下的修補檔 `elasticsearch-patch.json`，並使用 `azdata` CLI 來修補 `control.json` 檔案：

```json
{
  "patch": [
    {
      "op": "add",
      "path": "spec.settings",
      "value": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
        }
      }
    }
  ]
}
```

執行此命令來修補設定檔：

```bash
azdata bdc config patch --config-file custom-bdc/control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> 建議的最佳做法是依照[本文](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)中的指示，在 Kubernetes 叢集中每個主機上手動更新 `max_map_count` 設定。

## <a name="next-steps"></a>後續步驟

如需在巨量資料叢集部署中使用設定檔的詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md#configfile)。
